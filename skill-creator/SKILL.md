---
name: skill-creator
description: Guide for creating effective skills. This skill should be used when users want to create a new skill (or update an existing skill) that extends Claude's capabilities with specialized knowledge, workflows, or tool integrations.
version: 1.2.0
# No API keys required - procedural guidance skill
---

# Skill Creator

This skill provides guidance for creating effective skills.

## About Skills

Skills are modular, self-contained packages that extend Claude's capabilities by providing
specialized knowledge, workflows, and tools. Think of them as "onboarding guides" for specific
domains or tasks—they transform Claude from a general-purpose agent into a specialized agent
equipped with procedural knowledge that no model can fully possess.

### What Skills Provide

1. Specialized workflows - Multi-step procedures for specific domains
2. Tool integrations - Instructions for working with specific file formats or APIs
3. Domain expertise - Company-specific knowledge, schemas, business logic
4. Bundled resources - Scripts, references, and assets for complex and repetitive tasks

## Core Principles

### Concise is Key

The context window is a public good. Skills share the context window with everything else Claude needs: system prompt, conversation history, other Skills' metadata, and the actual user request.

**Default assumption: Claude is already very smart.** Only add context Claude doesn't already have. Challenge each piece of information: "Does Claude really need this explanation?" and "Does this paragraph justify its token cost?"

Prefer concise examples over verbose explanations.

### Set Appropriate Degrees of Freedom

Match the level of specificity to the task's fragility and variability:

**High freedom (text-based instructions)**: Use when multiple approaches are valid, decisions depend on context, or heuristics guide the approach.

**Medium freedom (pseudocode or scripts with parameters)**: Use when a preferred pattern exists, some variation is acceptable, or configuration affects behavior.

**Low freedom (specific scripts, few parameters)**: Use when operations are fragile and error-prone, consistency is critical, or a specific sequence must be followed.

Think of Claude as exploring a path: a narrow bridge with cliffs needs specific guardrails (low freedom), while an open field allows many routes (high freedom).

### Anatomy of a Skill

Every skill consists of a required SKILL.md file and optional bundled resources:

```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter metadata (required)
│   │   ├── name: (required)
│   │   ├── description: (required)
│   │   ├── version: (required for distribution)
│   │   └── requires_secrets: (if skill uses external APIs)
│   └── Markdown instructions (required)
└── Bundled Resources (optional)
    ├── scripts/          - Executable code (Python/Bash/etc.)
    ├── references/       - Documentation intended to be loaded into context as needed
    └── assets/           - Files used in output (templates, icons, fonts, etc.)
```

#### SKILL.md (required)

Every SKILL.md consists of:

- **Frontmatter** (YAML): Contains `name` and `description` fields. These are the only fields that Claude reads to determine when the skill gets used, thus it is very important to be clear and comprehensive in describing what the skill is, and when it should be used.
- **Body** (Markdown): Instructions and guidance for using the skill. Only loaded AFTER the skill triggers (if at all).

#### Bundled Resources (optional)

##### Scripts (`scripts/`)

Executable code (Python/Bash/etc.) for tasks that require deterministic reliability or are repeatedly rewritten.

- **When to include**: When the same code is being rewritten repeatedly or deterministic reliability is needed
- **Example**: `scripts/rotate_pdf.py` for PDF rotation tasks
- **Benefits**: Token efficient, deterministic, may be executed without loading into context
- **Note**: Scripts may still need to be read by Claude for patching or environment-specific adjustments

**Loading API Keys in Scripts:**

Scripts that need API keys should include an inline `load_env()` function that reads from the project's `.env` file. This keeps skills self-contained—no external dependencies required.

```python
#!/usr/bin/env python3
import os
import sys
from pathlib import Path

def load_env():
    """Load environment variables from .env file."""
    current = Path(__file__).resolve()
    for _ in range(10):
        current = current.parent
        env_path = current / ".env"
        if env_path.exists():
            try:
                with open(env_path) as f:
                    for line in f:
                        line = line.strip()
                        if line and not line.startswith("#") and "=" in line:
                            key, value = line.split("=", 1)
                            os.environ.setdefault(key.strip(), value.strip().strip('"\''))
                return True
            except Exception:
                continue
    return False

# Load .env and get API key
load_env()
api_key = os.environ.get("GEMINI_API_KEY")
if not api_key:
    print("Missing GEMINI_API_KEY in .env file", file=sys.stderr)
    sys.exit(1)
```

**Only include this pattern if your skill needs API keys.** Pure utility scripts don't need it.

This pattern ensures:
- Keys load from the project's `.env` file (git-ignored)
- Skills are completely self-contained
- Missing keys produce clear error messages

##### References (`references/`)

Documentation and reference material intended to be loaded as needed into context to inform Claude's process and thinking.

- **When to include**: For documentation that Claude should reference while working
- **Examples**: `references/finance.md` for financial schemas, `references/mnda.md` for company NDA template, `references/policies.md` for company policies, `references/api_docs.md` for API specifications
- **Use cases**: Database schemas, API documentation, domain knowledge, company policies, detailed workflow guides
- **Benefits**: Keeps SKILL.md lean, loaded only when Claude determines it's needed
- **Best practice**: If files are large (>10k words), include grep search patterns in SKILL.md
- **Avoid duplication**: Information should live in either SKILL.md or references files, not both. Prefer references files for detailed information unless it's truly core to the skill—this keeps SKILL.md lean while making information discoverable without hogging the context window. Keep only essential procedural instructions and workflow guidance in SKILL.md; move detailed reference material, schemas, and examples to references files.

##### Assets (`assets/`)

Files not intended to be loaded into context, but rather used within the output Claude produces.

- **When to include**: When the skill needs files that will be used in the final output
- **Examples**: `assets/logo.png` for brand assets, `assets/slides.pptx` for PowerPoint templates, `assets/frontend-template/` for HTML/React boilerplate, `assets/font.ttf` for typography
- **Use cases**: Templates, images, icons, boilerplate code, fonts, sample documents that get copied or modified
- **Benefits**: Separates output resources from documentation, enables Claude to use files without loading them into context

#### What to Not Include in a Skill

A skill should only contain essential files that directly support its functionality. Do NOT create extraneous documentation or auxiliary files, including:

- README.md
- INSTALLATION_GUIDE.md
- QUICK_REFERENCE.md
- CHANGELOG.md
- etc.

The skill should only contain the information needed for an AI agent to do the job at hand. It should not contain auxilary context about the process that went into creating it, setup and testing procedures, user-facing documentation, etc. Creating additional documentation files just adds clutter and confusion.

### Progressive Disclosure Design Principle

Skills use a three-level loading system to manage context efficiently:

1. **Metadata (name + description)** - Always in context (~100 words)
2. **SKILL.md body** - When skill triggers (<5k words)
3. **Bundled resources** - As needed by Claude (Unlimited because scripts can be executed without reading into context window)

#### Progressive Disclosure Patterns

Keep SKILL.md body to the essentials and under 500 lines to minimize context bloat. Split content into separate files when approaching this limit. When splitting out content into other files, it is very important to reference them from SKILL.md and describe clearly when to read them, to ensure the reader of the skill knows they exist and when to use them.

**Key principle:** When a skill supports multiple variations, frameworks, or options, keep only the core workflow and selection guidance in SKILL.md. Move variant-specific details (patterns, examples, configuration) into separate reference files.

**Pattern 1: High-level guide with references**

```markdown
# PDF Processing

## Quick start

Extract text with pdfplumber:
[code example]

## Advanced features

- **Form filling**: See [FORMS.md](FORMS.md) for complete guide
- **API reference**: See [REFERENCE.md](REFERENCE.md) for all methods
- **Examples**: See [EXAMPLES.md](EXAMPLES.md) for common patterns
```

Claude loads FORMS.md, REFERENCE.md, or EXAMPLES.md only when needed.

**Pattern 2: Domain-specific organization**

For Skills with multiple domains, organize content by domain to avoid loading irrelevant context:

```
bigquery-skill/
├── SKILL.md (overview and navigation)
└── reference/
    ├── finance.md (revenue, billing metrics)
    ├── sales.md (opportunities, pipeline)
    ├── product.md (API usage, features)
    └── marketing.md (campaigns, attribution)
```

When a user asks about sales metrics, Claude only reads sales.md.

Similarly, for skills supporting multiple frameworks or variants, organize by variant:

```
cloud-deploy/
├── SKILL.md (workflow + provider selection)
└── references/
    ├── aws.md (AWS deployment patterns)
    ├── gcp.md (GCP deployment patterns)
    └── azure.md (Azure deployment patterns)
```

When the user chooses AWS, Claude only reads aws.md.

**Pattern 3: Conditional details**

Show basic content, link to advanced content:

```markdown
# DOCX Processing

## Creating documents

Use docx-js for new documents. See [DOCX-JS.md](DOCX-JS.md).

## Editing documents

For simple edits, modify the XML directly.

**For tracked changes**: See [REDLINING.md](REDLINING.md)
**For OOXML details**: See [OOXML.md](OOXML.md)
```

Claude reads REDLINING.md or OOXML.md only when the user needs those features.

**Important guidelines:**

- **Avoid deeply nested references** - Keep references one level deep from SKILL.md. All reference files should link directly from SKILL.md.
- **Structure longer reference files** - For files longer than 100 lines, include a table of contents at the top so Claude can see the full scope when previewing.

## Skill Creation Process

Skill creation involves these steps:

1. Understand the skill with concrete examples
2. Plan reusable skill contents (scripts, references, assets)
3. Create the skill directory and SKILL.md
4. Edit the skill (implement resources and write SKILL.md)
5. Validate and install the skill
6. Iterate based on real usage

Follow these steps in order, skipping only if there is a clear reason why they are not applicable.

### Step 1: Understanding the Skill with Concrete Examples

Skip this step only when the skill's usage patterns are already clearly understood. It remains valuable even when working with an existing skill.

To create an effective skill, clearly understand concrete examples of how the skill will be used. This understanding can come from either direct user examples or generated examples that are validated with user feedback.

For example, when building an image-editor skill, relevant questions include:

- "What functionality should the image-editor skill support? Editing, rotating, anything else?"
- "Can you give some examples of how this skill would be used?"
- "I can imagine users asking for things like 'Remove the red-eye from this image' or 'Rotate this image'. Are there other ways you imagine this skill being used?"
- "What would a user say that should trigger this skill?"

To avoid overwhelming users, avoid asking too many questions in a single message. Start with the most important questions and follow up as needed for better effectiveness.

Conclude this step when there is a clear sense of the functionality the skill should support.

### Step 2: Planning the Reusable Skill Contents

To turn concrete examples into an effective skill, analyze each example by:

1. Considering how to execute on the example from scratch
2. Identifying what scripts, references, and assets would be helpful when executing these workflows repeatedly

Example: When building a `pdf-editor` skill to handle queries like "Help me rotate this PDF," the analysis shows:

1. Rotating a PDF requires re-writing the same code each time
2. A `scripts/rotate_pdf.py` script would be helpful to store in the skill

Example: When designing a `frontend-webapp-builder` skill for queries like "Build me a todo app" or "Build me a dashboard to track my steps," the analysis shows:

1. Writing a frontend webapp requires the same boilerplate HTML/React each time
2. An `assets/hello-world/` template containing the boilerplate HTML/React project files would be helpful to store in the skill

Example: When building a `big-query` skill to handle queries like "How many users have logged in today?" the analysis shows:

1. Querying BigQuery requires re-discovering the table schemas and relationships each time
2. A `references/schema.md` file documenting the table schemas would be helpful to store in the skill

To establish the skill's contents, analyze each concrete example to create a list of the reusable resources to include: scripts, references, and assets.

### Step 3: Initializing the Skill

At this point, it is time to actually create the skill.

Skip this step only if the skill being developed already exists, and iteration or packaging is needed. In this case, continue to the next step.

When creating a new skill from scratch, create the directory and a SKILL.md with valid frontmatter.

```bash
mkdir -p <path>/<skill-name>
```

Then write `<path>/<skill-name>/SKILL.md` starting with YAML frontmatter:

```yaml
---
name: <skill-name>
description: <what it does + when to use it, written for the model deciding whether to load it>
---
```

**The directory name MUST match the `name` field exactly**, or the skill will not load.

Add `scripts/`, `references/`, or `assets/` subdirectories only if the skill actually needs them. A skill that is purely procedural guidance needs nothing but SKILL.md.

Structure the body around what the model needs at runtime:

- **Multi-step processes**: lay out the sequence explicitly, with the decision points named
- **Specific output formats or quality standards**: show a template or a worked example rather than describing it

These files contain established best practices for effective skill design.

#### Start with Reusable Skill Contents

To begin implementation, start with the reusable resources identified above: `scripts/`, `references/`, and `assets/` files. Note that this step may require user input. For example, when implementing a `brand-guidelines` skill, the user may need to provide brand assets or templates to store in `assets/`, or documentation to store in `references/`.

Added scripts must be tested by actually running them to ensure there are no bugs and that the output matches what is expected. If there are many similar scripts, only a representative sample needs to be tested to ensure confidence that they all work while balancing time to completion.

Any example files and directories not needed for the skill should be deleted. The initialization script creates example files in `scripts/`, `references/`, and `assets/` to demonstrate structure, but most skills won't need all of them.

#### Update SKILL.md

**Writing Guidelines:** Always use imperative/infinitive form.

##### Frontmatter

Write the YAML frontmatter with required and optional fields:

**Required fields:**

- `name`: The skill name (hyphen-case, matches directory name)
- `description`: Primary triggering mechanism. Include what the skill does AND specific triggers/contexts for when to use it. Include all "when to use" info here—not in the body, which loads only after triggering.
- `version`: Semantic version (e.g., "1.0.0"). Required for distribution via `/export-skill`.

**Optional fields:**

- `requires_secrets`: Declares API keys the skill needs (for skills using external APIs). Enables `/install-skill` to guide users through configuration.
- `agent`: Specifies which subagent to use (`general-purpose`, `Explore`, `Plan`, `Bash`). Protects main context by running skill in isolated agent.
- `model`: Model to use for the subagent (`sonnet`, `opus`, `haiku`). Defaults to parent model if not specified.
- `context`: How context is passed to subagent. Use `fork` to run in parallel with full current context, or omit for fresh context.
- `user-invocable`: Set to `false` to prevent users from invoking with slash commands (default: `true`).
- `disable-model-invocation`: Set to `true` to prevent Claude from auto-triggering the skill (default: `false`).

**Example frontmatter with API keys:**

```yaml
---
name: video-thumbnail
description: Generate YouTube thumbnails using AI image generation. Use when user asks to create thumbnails, YouTube thumbnails, or video cover images.
version: 1.0.0
requires_secrets:
  - key: GEMINI_API_KEY
    service: Google AI Studio
    url: https://aistudio.google.com/apikey
    description: API key for Gemini image generation
    hint: "Starts with 'AIza', 39 characters total"
    instructions: |
      1. Go to aistudio.google.com/apikey
      2. Sign in with your Google account
      3. Click "Create API Key"
      4. Select "Create API key in new project"
      5. Copy the key that appears
    required: true
  - key: CLOUDFLARE_IMAGES_TOKEN
    service: Cloudflare Images
    url: https://dash.cloudflare.com/images
    description: For uploading generated images (optional)
    instructions: |
      1. Go to dash.cloudflare.com
      2. Select Images from the sidebar
      3. Go to Overview → API Tokens
      4. Create a token with Images permissions
    required: false
---
```

The `instructions` field provides step-by-step guidance shown to users during `/install-skill`.

**Example frontmatter without API keys:**

```yaml
---
name: prompt-engineering
description: Expert guidance for crafting LLM prompts. Use when user asks about prompt design, system prompts, or agentic patterns.
version: 1.0.0
# No external APIs needed
---
```

**Example frontmatter with subagent configuration:**

```yaml
---
name: task
description: Manage Notion Tasks DB operations. Use when user asks to create tasks, list tasks, or update task status.
version: 1.0.0
agent: general-purpose
model: sonnet
context: fork
---
```

The subagent configuration (`agent`, `model`, `context`) protects the main conversation from verbose API operations while allowing the skill to run with full context.

##### Body

Write instructions for using the skill and its bundled resources.

### Step 5: Packaging a Skill

Once the skill is written, validate it before relying on it:

**Manual validation checklist:**

- [ ] `SKILL.md` exists and opens with valid YAML frontmatter between `---` fences
- [ ] `name` matches the directory name exactly
- [ ] `description` states both WHAT the skill does and WHEN to use it. This is the only part the model sees when deciding whether to load the skill, so a vague description means the skill never triggers.
- [ ] Every file the SKILL.md tells the user to run or read actually exists in the skill directory
- [ ] Any scripts are executable and their paths are correct relative to the skill root
- [ ] No secrets, API keys, absolute paths from your own machine, or references to private files

**To install it:** copy the folder into `~/.claude/skills/` for every project, or `.claude/skills/` inside a single project. Restart Claude Code and run `/skills` to confirm it loaded.

**To share it:** the folder is the skill. Zip it, commit it to a repo, or hand it over as-is. There is no build step.

---

## Attribution

This skill is derived from Anthropic's `skill-creator`, licensed under Apache License 2.0. It has been modified: the packaging and initialization steps were rewritten as manual instructions so the skill is self-contained with no bundled scripts.
