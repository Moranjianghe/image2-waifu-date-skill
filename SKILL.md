---
name: image2-waifu-date
description: Create and iterate image 2 prompts for consistent waifu, coser, girlfriend, dating, shopping, restaurant, street-snap, first-person POV, and romantic companion scenes. Use when Codex needs to preserve the same character across image generations, combine character/outfit/location reference images, draft bilingual prompts for user confirmation, or generate realistic phone-photo style date images with controlled props, motion blur, brand signage, and scene continuity.
---

# Image 2 Waifu Date

Use this skill for image 2 date-scene generations where the user cares about a recurring companion character, a specific outfit/reference image, and realistic phone-photo composition.

## Core Rules

- Speak Chinese to the user when the surrounding task is Chinese.
- Always confirm the exact prompt before generating unless the user explicitly says to generate immediately.
- Never put API keys, endpoint keys, or user secrets into skill files, prompts, logs, or final responses.
- Prefer reference images over long textual costume descriptions when the user has a specific image.
- Use detailed prompts for continuity, exact outfits, real locations, and multi-prop date scenes. Do not use one-sentence prompts for these tasks unless the user explicitly asks for a controlled comparison experiment.
- Preserve safety by keeping romantic/date scenes non-explicit and avoiding childlike framing.

## Workflow

1. Identify inputs:
   - Character identity reference: previous generated image or user-supplied person/coser image.
   - Outfit/design reference: character sheet, costume image, or clothing image.
   - Scene/location reference: real place photo, storefront, restaurant, street, or mall.
   - Continuity requirements: same person, same outfit, same props, same relationship POV.
2. Summarize what each image controls:
   - Identity continuity controls face, vibe, hair, body proportions, and prior styling.
   - Outfit reference controls costume and accessories.
   - Scene reference controls architecture, lighting, crowd density, and local details.
3. Draft the prompt in English for image 2, then provide a Chinese translation or Chinese summary for the user.
4. Ask for confirmation before the API call.
5. Generate with all relevant reference images if the image endpoint supports edits/multi-image inputs.
6. Save each result with a semantic filename. Do not overwrite prior generations unless asked.
7. Report saved path, size, model, and any fallback behavior.

For API execution, follow the download and `response_format="b64_json"` policy in `$image2-general-generator`. Compatible endpoints may return signed URLs that fail with 403 or timeout; prefer base64 responses when possible.

## Prompt Length Policy

For waifu/date continuity tasks, default to a structured detailed prompt. Prior testing showed that a one-sentence prompt can under-specify character continuity, outfit fidelity, location details, props, and camera behavior, even when reference images are supplied.

Use a one-sentence prompt only when:

- The user explicitly requests a minimal-prompt comparison.
- The task is a loose brainstorming draft where continuity and exact scene matching do not matter.
- You clearly label it as experimental and ask before generating.

## Prompt Structure

Use this order for detailed prompts:

```text
Reference roles:
Use <identity image> as identity and continuity reference.
Use <outfit image> as exact clothing/design reference.
Use <scene image> as architectural/location reference.

Primary scene:
<date scenario, date/time, city, season, activity>

Character:
<same person/coser, pose, expression, relation to photographer>

Outfit:
<specific reference outfit instructions; do not use generic/classic alternate versions>

Location:
<real-place features from scene reference>

Action and POV:
<first-person phone photo, hand-holding, walking, looking back, table POV, etc.>

Camera realism:
<vertical smartphone photo, HDR, auto white balance, wide-angle perspective, low-light noise, motion blur>

Props:
<bag, phone, bouquet, food, shopping bags; natural placement>

Avoid:
<wrong outfit, wrong location, empty scene, anime/CGI, deformed hands, watermark, unwanted text/logo rules>
```

## Continuity Checklist

For "same person" requests, include:

- Same face and overall appearance from the prior image.
- Same hair color, hairstyle, ornaments, and body proportions.
- Same outfit direction unless the user asks to change clothes.
- Same relationship POV if established, such as dinner date, walking together, or being led by hand.
- A realistic transition between scenes, such as "after dinner" or "later that evening".

For a specific outfit reference, say:

```text
Use the input image as the exact clothing design reference. Do not use a generic or classic version of the character. Keep the real outfit recognizable as a commissioned cosplay version of this reference.
```

## Phone Photo Realism

Add only the realism cues needed for the scene:

- Vertical first-person smartphone snapshot.
- Casual handheld framing, slight tilt, mild wide-angle perspective.
- Phone HDR, auto white balance, compressed dynamic range.
- Low-light noise and small highlight trails at night.
- Motion blur when walking: background pedestrians blurred, lights streaked, moving arms/hair/ribbons slightly blurred, face still recognizable.
- Realistic imperfect composition. Avoid studio/fashion editorial language unless the user asks.

## Date Scene Patterns

### Restaurant

Use table foreground, partial photographer hand or phone edge, food close to lens, companion across the table. For American steakhouse food, prefer thick ribeye/T-bone, charred grill marks, compound butter, mashed potatoes, fries, creamed spinach, mac and cheese, onion rings, roasted mushrooms. Avoid salad if the user disliked repetition.

### Shopping District

Use walking POV, companion ahead holding photographer's hand, looking back toward camera. Include crowd density, couples, flowers, shopping bags, seasonal weather, storefront lighting, reflections, and location-specific architecture.

### Location Reference

When a scene photo is provided, describe concrete architecture rather than just the place name. Example for Hubin Yintai in77:

```text
Match the night plaza, tall illuminated glass-grid building, white sculptural luxury storefront cube, broad open stone-paved square, circular paving lines, embedded ground lights, and people walking around the plaza.
```

## Brand and Logo Handling

Ask the user whether to preserve real storefront logos if the scene reference contains them.

- Conservative default: avoid readable logos and brand text to reduce garbling.
- If the user wants the real logo: explicitly preserve only the real signage from the reference and remove "avoid readable logos" constraints.

Example:

```text
Keep the Louis Vuitton storefront cube from the reference image recognizable, including the illuminated LV monogram and Louis Vuitton signage as part of the real location background.
```

## Reference Examples

Read [examples.md](references/examples.md) when you need reusable prompt templates for:

- A detailed restaurant date prompt.
- A detailed in77 520 walking prompt.
- A deprecated minimal prompt note explaining why it should usually be avoided.
