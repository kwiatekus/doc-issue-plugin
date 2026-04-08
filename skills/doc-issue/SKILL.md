---
name: doc-issue
description: Write user documentation for a given GitHub issue URL, following Kyma content guidelines (style, formatting, terminology, topic types).
argument-hint: [github-issue-url]
allowed-tools: Read Glob Grep WebFetch Write Edit
---

# Write Documentation for a GitHub Issue

You are writing user-facing documentation for one of the the Kyma modules. Your output must follow the Kyma content guidelines exactly as defined below.
Do not suggest any code, configuration, dockerfile changes.
Only content in .md format is allowed.


## Step 1 — Understand the issue

Fetch the GitHub issue at `$ARGUMENTS` using WebFetch. Extract:
- What feature or change is being documented
- The acceptance criteria (these define scope)
- Any linked PRs or code references

## Step 2 — Determine the document type

Choose the correct topic type based on the issue content:

| Type | When to use | Title style |
|---|---|---|
| **Concept** | Explains what something is, background knowledge | Noun: "Network Policies" |
| **Task** | Step-by-step instructions for a single procedure | Imperative verb: "Configure X", "Enable Y" |
| **Reference** | Tables of parameters, CRD fields, role lists | Noun: "Cluster Roles" |
| **Troubleshooting** | Symptom → cause → solution | Symptom as title: "Cannot access..." |

## Step 3 — Read existing docs for context

Before writing, run:
- `Glob docs/user/**/*.md` — understand existing structure and naming
- Read 2–3 nearby docs to match established tone and section style
- Read `docs/user/_sidebar.ts` to determine where the new doc fits

## Step 4 — Write the document

Save the file to `docs/user/` following the `NN-NN-kebab-title.md` naming convention used by existing files.


### Topic Types and Templates

#### Concept Topics
- Answer "what-is" questions with background information
- Use nominal style titles (e.g., "Security Concept")
- No instructions or reference tables
- Link to related task and reference topics

#### Task Topics
- Provide "how-to" instructions for specific procedures
- Use imperative titles describing the task (e.g., "Define Resource Consumption")
- Structure: intro paragraph → prerequisites → numbered steps (5-9 ideal) → expected result
- Use present tense action verbs in titles

#### Custom Resource Topics
- Document CRs with sample YAML and field descriptions
- Filename: `{RESOURCE_NAME}.md`
- Title: CamelCase resource name (e.g., "LogPipeline")
- Consider autogeneration from code for easier maintenance

#### Troubleshooting Topics
- Title mentions symptom or error message, not cause
- Structure: Condition → Cause → Solution
- Use numbered lists for multi-step solutions


## Step 5 — Update the sidebar

Add the new document to `docs/user/_sidebar.ts` in the appropriate position. Match the existing entry format exactly.

---

## Kyma Writing Rules (apply to every word you write)


### Formatting Standards

#### Code Font vs Bold Font

**Use bold for:**
- Parameters
- HTTP headers
- Events
- Roles
- UI elements
- Variables and placeholders

**Use code font for:**
- Code examples and commands
- Values and endpoints
- File names, extensions, paths
- Repository names
- Status and error codes
- Flags
- Custom resources (when referring to code)

#### Lists
- Make content consistent in structure
- Punctuate consistently (periods for sentences, none for fragments)
- Avoid semicolons or commas at end of bullets
- Capitalize first letter consistently
- Use ordered lists for sequential steps
- Bold terms when defining them, followed by hyphen or sentence

#### Tables
- Centralize columns with choice-type values (Yes/No, true/false)
- Write "None" for parameters with no default values
- Avoid overly long tables that require excessive scrolling

#### Headings
- Write in title case (e.g., "Expose a Service")
- Use action verbs and present tense
- Avoid gerunds in headings (use "Create" not "Creating")
- No stacked headings without body content between
- Use H1 for title, H2 and H3 for organization (avoid H4+)
- Keep headings concise, fitting in one line

#### Panels
Use VitePress customized alerts:
- `[!NOTE]` (blue): Point to specific information
- `[!WARNING]` (orange): Critical information about inoperable behavior
- `[!TIP]` (green): Helpful advice or shortcuts


### Terminology — always use the left column

| Use | Never use |
|---|---|
| `must` | have to, need to, should |
| `can` | it is possible to, allows you to, there is the possibility to |
| `use` | utilize |
| `run` | execute |
| `using` / `with` | via |
| `repository` | repo |
| `for example` / `such as` | e.g. |
| `that is` | i.e. |
| `the following` | below, this, the described |
| `must` / `can` | should |
| `email` | e-mail |
| `frontend` / `backend` | front end, front-end, back end, back-end |
| American English spelling | British English |
| YAML | yaml (unless file extension: `.yaml`) |
| `-n` | `--namespace` (use short flags) |

### Style and Grammar

#### Voice and Tone
- Use active voice (not passive)
- Use semi-formal style and imperative mood
- Use present tense
- Use second person ("you", "your")
- Avoid "please", "remember", unnecessary "can"
- Contractions are okay but don't overuse

#### Punctuation
- Use serial commas
- Use colons sparingly to introduce lists
- Avoid parentheses; use lists for clarity

#### Articles
- Verify use of "a", "an", "the"
- Don't use articles before Kyma or component names
  - ✅ "Kyma is awesome"
  - ⛔️ "The Kyma is awesome"

### Capitalization Rules

#### Sentence Case
Use for standard sentences

#### Title Case
Use for:
- Kyma component names (e.g., Application Connector, API Gateway Controller)
- Headings

#### CamelCase
Use for:
- Kubernetes resources
- Custom resources
- Add "s" for plurals
- Add spaces in titles/navigation for readability
- Use lowercase when not referring to Kubernetes resources

**Never capitalize "namespace"**

### Terminology Standards

| ✅ Use | ⛔️ Avoid |
|--------|---------|
| ID | id |
| and | +, & |
| backend | back end, back-end |
| connect, connection | integrate, integration |
| custom resource | Custom Resource, CustomResource |
| document | doc |
| email | e-mail |
| fill in | complete |
| frontend | front end, front-end |
| key-value | key/value, key:value |
| micro frontend | microfrontend, micro front-end |
| must | have to, need to |
| or | / |
| repository | repo |
| run | execute |
| typically | usually |
| use | utilize |
| using, with | via |
| YAML | yaml (except in filenames: `.yaml`) |
| must, can | should (use "must" if mandatory, "can" if optional) |
| (you) can | it is possible to, allows you to |
| that is | i.e. |
| for example, such as | e.g. |
| cloud-native (adjective) | cloud native |
| application | app (except "Application" for external solutions via Application Connector) |
| the following | below, this |
| the previous, earlier | above, this |

**Command line arguments**: Use short forms when possible (`-n` not `--namespace`), but explain context if tools differ.

### Links Best Practices

- Use **relative links** for same repository
- Use **absolute links** for other repos and external sources
- Choose descriptive link text (avoid "here", "this", "click here")
- Link to headings: `[text](./file.md#heading-name)`
- Don't overlink; link strategically

### Screenshots Guidelines

**Use screenshots sparingly:**
- They become outdated quickly
- Not accessible for screen readers
- Cannot be translated

**When using screenshots:**
- Complement text, don't replace instructions
- Always add alt text describing content/function
- Use SVG, PNG, or JPG (max 1MB, use TinyPNG to compress)
- Include gray border (HEX: #D2D5D9, 1pt)
- Use blue stamps (HEX: #0A6ED1) for steps
- Use red indicators (HEX: #EF2727, 10pt) sparingly
- Prefer Simplified User Interfaces (SUI) - blur non-essential elements
- Don't include browser toolbars or mouse pointer (unless showing function)

### Tabs and Toggles

Use tabs and toggles to present multiple versions of content (e.g., different OS instructions, installation methods):

**Customized Tabs:**
- Use VitePress syntax: `<!-- tabs:start -->` and `<!-- tabs:end -->`
- Each tab defined with `#### **Tab Name**`
- Renders as tabs on kyma-project.io, as sections in GitHub

**Documentation Toggles:**
- Start set with `<div tabs name="{unique-id}">` and end with `</div>`
- Each toggle wrapped in `<details>` and `</details>` tags
- Title between `<summary>` and `</summary>` tags
- Leave blank line after `</summary>` for proper rendering
- Use proper indentation: no spaces for div (regular section), 2 spaces for other elements; 4 spaces for div (under list), 6 spaces for other elements
- For grouped toggles: add `group` attribute to div and `label` attribute to summary

### Diagrams

Use diagrams to visualize complex concepts, workflows, and architectures:

**Best Practices:**
- Don't drop diagrams without context; explain their purpose
- Everything meaning the same should look the same
- Limit visual noise and keep it simple but descriptive
- Follow left-to-right direction for workflows
- Always add descriptive alt text

**Formatting Standards:**
- Tool: Use [drawio](https://www.drawio.com/), export as SVG
- Background: White (HEX: #FFFFFF) with rounded secondary backgrounds (mild blue #F0F6FF for main environment, mint green #DEF2DD for subsidiary environments)
- Shapes: Rounded rectangles with white fill, gray outlines (HEX: #666666, 1pt)
- Actors: Blue fill (HEX: #0A6EC7), no outline
- Text: Black, Helvetica font (15pt bold for headings, 13pt for primary text, 12pt for secondary text)
- Steps: Blue round stamps (HEX: #0A6EC7) with white numbers, explained in ordered list below
- Connectors: 1pt rounded gray lines (HEX: #666666)
- Size: Maximum width 860px on website, keep reasonable and legible

### Release Notes

When writing or reviewing release notes:

**Content Focus:**
- Write from user's perspective, not developer's perspective
- Answer: What changed? How was it different before? UI/functionality changes? Error messages?
- Use "known issue" and "resolved issue" (not "bug")

**Structure:**
- Headlines in sentence case
- New features: Write enticing paragraphs (not just bullet lists)
- Known/resolved issues: Bulleted lists okay if descriptions make sense
- Use consistent sentence structure in bulleted lists

**Migration Guides:**
- Provide when manual steps required for upgrade
- Clearly list all necessary steps
- Don't describe new features in migration guide (use release notes instead)

### UI Elements Guidelines

For UI documentation:
- Use active voice and action-oriented language
- Use title case for short labels/headings
- Use sentence case for messages
- Use plural for object names
- Use plain, natural language
- Omit punctuation in labels
- Make button labels clear and specific (avoid generic "Yes"/"No")
