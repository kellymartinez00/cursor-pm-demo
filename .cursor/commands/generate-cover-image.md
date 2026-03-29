---
description: Generate an NDR-branded demo cover slide image using Nano Banana MCP. Uses the casual Boom Tech mascot, official NDR logos, and brand guidelines.
---

## User Input

```text
$ARGUMENTS
```

## Instructions

Generate a polished, branded cover slide image using the Nano Banana MCP (`user-nanobanana` server).

Before generating, read:
- `.cursor/rules/boom-tech-character.mdc` for the canonical character design
- Brand color reference: Deep Navy Blue `#1F2147`, Flag Red `#A31921`, white `#FFFFFF`

### Logo and Typography Rules

The NDR logo MUST NOT be invented or approximated. Always pass the actual logo files as `reference_images` so Gemini reproduces them accurately:

- **Full wordmark logo**: `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/brandguide/ndrlogo.svg`
  - Contains: "NATIONAL DEBT RELIEF" wordmark in navy `#1F2147`, red flag/banner element in `#A31921`, decorative stars, horizontal rule, and "DEBT RELIEF" subtitle
- **Shield logo**: `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/brandguide/registered-trademark-shield-ndr.svg`
  - Contains: shield shape in navy `#1F2147` with red `#A31921` flag accent and decorative stars. Registered trademark symbol.

Do NOT describe the logo from memory. Instead, instruct the prompt to "reproduce the NDR logo exactly as provided in the reference images" and rely on the reference_images to carry the visual.

### Typography

- Font: Avenir Next (the NDR brand typeface)
- Headings: bold, navy `#1F2147`
- Subtitles: medium weight, navy `#1F2147` or gray `#667085`
- Never use serif fonts or handwritten styles

### Build the Cover Prompt

Extract from user input:
- **Title**: default "Cursor for Product Managers" unless user specifies otherwise
- **Subtitle/date**: default "March 30, 2026 | PM Onboarding Session"
- **Style notes**: any user preferences for layout or energy level

Construct the prompt:

```
Create a visually rich 16:9 presentation cover slide. The design should feel polished,
energetic, and professional — not plain or minimal.

TOP SECTION: Reproduce the NDR logo exactly as shown in the reference images — the full
'NATIONAL DEBT RELIEF' wordmark with the shield element, stars, and red flag/banner accent.
Place it prominently at the top left or top center. Do not invent or approximate the logo.

TITLE: Below the logo, display '[TITLE]' in bold navy blue (#1F2147) text, large and
prominent. Use clean sans-serif typography (Avenir Next style).

VISUAL ENERGY: Add depth to the composition with:
- A subtle gradient or geometric pattern background using light blue (#D1E9FF) to white,
  or a faint tech-grid/circuit pattern in very light navy
- Floating translucent tool icons (Jira board, Confluence page, code brackets, Slack bubble,
  GitHub octocat silhouette) arranged in a flowing arc or constellation pattern
- Soft glowing connection lines between the icons suggesting integration
- Subtle particle/dot effects for a modern tech feel

CHARACTER: On the right third of the image, the Boom Tech mascot character in the casual
pose. Character details: bright spiky red hair with red headband, steampunk goggles with
navy blue frames on forehead, white labcoat with red accent trim open showing red necktie
over dark shirt, black pants, navy combat boots with red laces. Single lanyard employee
badge around neck showing only the NDR shield logo (no text on badge, just the shield).
No duplicate badges. No weapon. Confident stance, welcoming gesture (thumbs up or open
hand). The character should feel integrated into the design, not pasted on.

FOOTER: Small text at bottom: '[SUBTITLE_DATE]' in gray (#667085).

Color palette: deep navy blue (#1F2147), flag red (#A31921), light blue (#D1E9FF),
white (#FFFFFF). The overall feel should be a premium SaaS product launch slide
blended with the anime character personality.
```

### Call Nano Banana

Use `CallMcpTool` with server `user-nanobanana` and tool `gemini_generate_image`:

- `prompt`: the constructed prompt
- `aspect_ratio`: `"16:9"`
- `conversation_id`: `"pm-demo-char"`
- `use_image_history`: `true`
- `reference_images`: always include ALL FOUR:
  - `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/artifactgen/images/character/00-boom-tech-ndr-mascot-casual.png`
  - `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/LOGO_DESIGN.3b081599.png`
  - `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/brandguide/ndrlogo.svg`
  - `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/brandguide/registered-trademark-shield-ndr.svg`
- `output_path`: `images/00-demo-cover.png`

### Post-Generation

Verify:
- NDR logo matches the reference (shield + wordmark + stars + flag accent)
- Logo is NOT invented or approximated — it must come from the reference images
- Character matches canonical casual design (single lanyard shield badge, no weapon)
- Composition has visual energy (not a flat plain white slide)
- Typography is clean sans-serif, navy and gray
- NDR brand colors present throughout
