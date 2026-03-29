---
description: Generate a Boom Tech x NDR mascot character image using Nano Banana MCP. Supports casual and action (bazooka) variants.
---

## User Input

```text
$ARGUMENTS
```

## Instructions

Generate a Boom Tech x NDR mascot character image using the Nano Banana MCP (`user-nanobanana` server).

Before generating, read the character specification rule at `.cursor/rules/boom-tech-character.mdc` for the canonical character design, colors, and badge requirements.

### Determine Variant

From the user input, determine which variant to generate:

- If input contains "casual", "standing", "no weapon", "no bazooka", or "relaxed": generate the **casual** variant (no weapon)
- If input contains "action", "bazooka", "rocket", "weapon", or "battle": generate the **action** variant (with rocket launcher)
- If unclear, default to **casual**

### Determine Context

From the user input, extract:

- **Scene or context**: what the character is doing or what diagram/slide they appear in
- **Aspect ratio**: default to `16:9` unless user specifies otherwise
- **Output path**: save to the `images/character/` directory with a descriptive filename

### Build the Prompt

Construct the Nano Banana prompt following this template. Replace bracketed items based on user input and variant:

```
Create a [ASPECT_RATIO] anime/manga cel-shaded illustration of the Boom Tech mascot character.
The character has bright spiky red hair swept upward with a red headband, and steampunk-style
goggles with navy blue frames pushed up on their forehead. They wear a flowing white labcoat
with red accent trim along the collar and cuffs, open in front showing a red necktie over a
dark shirt. Black fitted pants and dark navy combat boots with red laces. A single lanyard
employee badge hangs around their neck — the badge shows only the NDR shield logo: a navy
blue (#1F2147) shield shape with a red (#A31921) flag/banner accent and small decorative
stars on a white card. No text on the badge, no duplicate badges.

[VARIANT_DESCRIPTION]

[SCENE_CONTEXT]

White background. Color palette: deep navy blue (#1F2147) and flag red (#A31921).
Clean anime cel-shaded style. [ADDITIONAL_INSTRUCTIONS]
```

**Variant descriptions:**

- Casual: "The character stands in a confident relaxed pose — [specific pose from user input or default: one hand adjusting goggles, other on hip, confident smirk]. No weapon."
- Action: "The character is in a dynamic action pose, slightly crouched, carrying a large dark metallic rocket launcher over one shoulder with red accent highlights. Labcoat billowing behind them. Determined, focused expression."

### Call Nano Banana

Use `CallMcpTool` with server `user-nanobanana` and tool `gemini_generate_image`:

- `prompt`: the constructed prompt above
- `aspect_ratio`: from user input or `"16:9"`
- `conversation_id`: `"pm-demo-char"`
- `use_image_history`: `true`
- `reference_images`: always include both:
  - `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/LOGO_DESIGN.3b081599.png`
  - `/Users/kelly.cruz/Documents/devRoot/BTNDRMASTER/NDR-FRONTENDS/BTAssist/PMDEMOASSIST/brandguide/registered-trademark-shield-ndr.svg`
- `output_path`: the determined output path

### Post-Generation

After generation, confirm:
- Character matches the canonical specification
- Only ONE lanyard badge is visible with the shield logo only (no wordmark text)
- Correct variant was generated (casual vs action)
- NDR brand colors are present
