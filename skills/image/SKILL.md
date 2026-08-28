---
name: image
description: Generates marketing images using the mcp-image MCP server. Reads brand guidelines for style consistency. Supports social posts, blog headers, ads, and presentation visuals.
autoload: false
---

# Marketing Image Generator

This skill generates images for marketing assets using the `mcp__mcp-image__generate_image` MCP tool. It reads brand guidelines to maintain visual consistency and constructs optimized prompts for each use case.

## Prerequisites

**Required:** The `mcp-image` MCP server must be configured and running.

---

## Step 1: Check Brand Guidelines

Before generating any images, read `docs/inputs/brand_guidelines.md`.

**If it exists and is filled in:** Extract visual style, color palette, mood, motifs, composition preferences, and restrictions. Use these to constrain every prompt.

**If it exists but is still a template (placeholder values):** Tell the user:

> "Your brand guidelines at `docs/inputs/brand_guidelines.md` are still the default template. I can generate images without them, but results will be generic. Would you like to fill in the guidelines first?"

If the user wants to proceed without guidelines, use sensible defaults: clean, minimal, professional, tech-focused.

---

## Step 2: Gather Inputs

Ask the user:

1. **What is this image for?**
   - Social media post (LinkedIn, Twitter)
   - Blog featured image
   - Ad creative
   - Presentation slide
   - Other (describe)

2. **Source content** — What should the image represent?
   - File path to the content it accompanies
   - Description of the concept
   - Or let the skill extract the concept from context (if already in a content generation flow)

3. **Reference image** — (Optional) Do you have a reference image for style matching?
   - If yes, provide the absolute file path

Wait for answers before proceeding.

---

## Step 3: Select Format

Based on the use case, select the appropriate aspect ratio and resolution:

| Use Case | Aspect Ratio | Resolution | Notes |
|----------|-------------|------------|-------|
| LinkedIn post | 16:9 | 2K | Horizontal, feed-optimized |
| Twitter post | 16:9 | 2K | Horizontal, timeline-optimized |
| Blog featured image | 16:9 | 2K | Standard blog header |
| LinkedIn ad | 1:1 | 2K | Square format for sponsored content |
| Meta ad | 4:5 | 2K | Vertical, mobile feed-optimized |
| Presentation slide | 16:9 | 2K | Horizontal, projector-friendly |
| Instagram post | 1:1 | 2K | Square format |

Confirm the format with the user before generating. If the user requests a custom aspect ratio, use the closest supported option from the tool (1:1, 2:3, 3:2, 3:4, 4:3, 4:5, 5:4, 9:16, 16:9, 21:9).

---

## Step 4: Construct the Prompt

Build the prompt in three layers:

### Layer 1: Style (from brand guidelines)

Extract from `docs/inputs/brand_guidelines.md`:
- Visual style (e.g., "minimalist tech illustration")
- Color palette (e.g., "dark navy background, electric blue and white accents")
- Mood (e.g., "professional, innovative, bold")
- Visual motifs (e.g., "geometric shapes, abstract connections")

### Layer 2: Concept (from source content)

Derive the visual concept from the source content. Rules:
- Abstract over literal. Represent the concept, not a screenshot of the product.
- One focal point. Do not try to illustrate every idea in the content.
- Pick the single most visually interesting element from the source.

### Layer 3: Restrictions (fixed + brand guidelines)

Always include:
- "No text, no words, no letters, no labels, no typography"
- "No photorealistic human faces"
- "Clean composition with clear focal point"
- Any brand-specific restrictions from guidelines

### Prompt Template

```
[Style: visual style, color palette, mood from brand guidelines]

[Concept: single visual idea derived from source content]

[Composition: layout guidance based on use case]

No text, no words, no letters, no labels, no typography. No photorealistic human faces. Clean composition with clear focal point. [Additional brand restrictions]
```

**Prompt rules:**
- Keep prompts under 200 words. Shorter prompts produce more coherent images.
- Use concrete visual descriptions, not abstract marketing language.
- Specify colors by name and relationship ("dark navy background with electric blue accent lines"), not hex codes.
- Describe spatial relationships ("left side", "center", "flowing from left to right").
- Include lighting direction if relevant ("backlit", "soft ambient glow").

---

## Step 5: Generate

Call the MCP tool with the constructed parameters:

```
mcp__mcp-image__generate_image(
  prompt: [constructed prompt],
  aspectRatio: [from format table],
  imageSize: [from format table],
  purpose: [use case description],
  quality: "quality",
  fileName: [descriptive file name]
)
```

**File naming:** `[context]-[concept]-[use-case]` (e.g., `beyond-identity-agent-governance-linkedin`, `ceros-credential-flow-blog-header`)

**If a reference image was provided:** Include `inputImagePath` with the absolute path.

After generation, read the output image and present it to the user.

---

## Step 6: Review and Refine

After presenting the image, ask:

> "Want to iterate on this, or is it good?"

### Refinement

If the user wants changes, adjust the prompt based on their feedback. Common adjustments:

| Feedback | Prompt Adjustment |
|----------|-------------------|
| "Too busy / complicated" | Reduce elements, add "minimal, sparse, lots of negative space" |
| "Too dark" | Shift to "light background, bright, well-lit" |
| "Too generic" | Add more specific visual motifs from the source content |
| "Wrong colors" | Explicitly name the desired colors |
| "Too many words/labels" | Strengthen the no-text restriction: "absolutely no text, no labels, no annotations, no typography of any kind" |
| "Not abstract enough" | Remove concrete objects, add "abstract, geometric, flowing shapes" |

**Maximum 5 refinement rounds.** After 5 attempts:

> "We've done 5 rounds. To get closer to what you want, I'd recommend:"
>
> 1. Providing a reference image that captures the style you're after
> 2. Updating brand guidelines with more specific visual direction
> 3. Trying a completely different visual concept

---

## Output

Images are saved to `output/images/` automatically by the MCP tool.

After the image is approved, provide:

```
Image: output/images/[filename].jpg
Dimensions: [aspect ratio] at [resolution]
Prompt: [the prompt used, for future reference]
Alt text: [SEO-friendly description, under 125 characters]
```

### Alt Text Rules

- Describe what is visually in the image, not the topic of the content
- 125 characters or fewer
- No "image of" or "picture of" prefix
- Include key visual elements and colors

---

## Multi-Image Generation

When generating images for a set of assets (e.g., a blog post + social posts promoting it), maintain visual consistency:

1. Use the same style layer across all prompts
2. Vary the concept layer to match each asset's focus
3. Keep the color palette consistent
4. Adjust only the aspect ratio and composition per format

---

## Adaptation Notes

- **When brand guidelines are sparse:** Default to clean, minimal, dark backgrounds with blue/white accents. Flag that results will improve with specific guidelines.
- **When source content is highly technical:** Focus on abstract representations. Do not try to literally illustrate architecture diagrams or code flows.
- **When the tool generates text despite instructions:** This is a known limitation of image generation models. Strengthen the no-text restriction and simplify the prompt. If text persists, note that the user can crop or overlay in post-production.
- **When used alongside other skills:** If called after `/social-posts`, `/blog`, or `/ads`, extract the concept directly from the generated content without re-asking the user.
