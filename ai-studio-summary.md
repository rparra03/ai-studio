# AI Studio — video-generator.html

Single-file HTML app that uses OpenRouter and fal.ai to generate images and videos with AI.

---

## Image Tab

- Image generation from text via OpenRouter `/api/v1/chat/completions` with `modalities: ["image"]`
- 10 available models: Flux.2 Pro / Max / Flex / Klein, GPT-5 Image / Mini, Gemini 2.5 / 3.1 Flash Image, Seedream 4.5, Recraft V3
- AI prompt enhancement (Claude Sonnet)
- 7 visual style presets: Auto, Cinematic, Anime, Realistic, 3D Render, Painterly, Dark Fantasy — automatically injected into the prompt
- Manual negative prompt
- **Character composition**: upload up to 4 reference photos → two options:
  - **Build prompt** (2-step pipeline): Gemini Vision describes each face → Claude builds a composition prompt → user clicks Generate
  - **Generate scene direct**: sends reference photos directly to a selectable model (GPT-5 Image recommended for real people — avoids Gemini's IMAGE_SAFETY block)

---

## Video Tab

- Image-to-video generation via OpenRouter `/api/v1/videos` with polling
- 10 available models: Veo 3.1 Fast / Lite, Kling 3.0 Pro / Std / O1, Seedance 2.0 / Fast, Wan 2.7 / 2.6, Hailuo 2.3
- Dynamic cost estimate (price/s × duration)
- Upload initial image or use image generated in the Image tab
- AI prompt enhancement
- 7 visual style presets (same system as Image tab)
- **12 camera motion controls**: Static, Dolly In/Out, Zoom In/Out, Pan Right/Left, Tilt Up/Down, Orbit, Handheld, Drone — with intensity slider (Soft / Normal / Dramatic)
- Style + camera phrases are concatenated to the prompt automatically before sending
- **Optional audio via MMAudio v2** (fal.ai): uploads video to fal storage via signed PUT URL, then generates synchronized audio
- Native audio support for models that include it (Veo, Seedance)
- Image is uploaded to imgbb to get a public URL before sending to OpenRouter

---

## Infrastructure / API Keys

| Key | Used for |
|---|---|
| OpenRouter API key | Image + video generation, prompt enhancement |
| fal.ai API key | MMAudio audio generation |
| imgbb API key | Image hosting for video generation |

OpenRouter account balance is displayed in the header.

---

## Current State

- Debug console logs active on: fal storage upload (PUT), MMAudio polling, video generation pipeline
- Deployed at: `https://rparra03.github.io/ai-studio/video-generator.html`

---

## Planned Features (next steps)

- Voice cloning + TTS narration (fal-ai/f5-tts, Kokoro)
- Lip sync (fal-ai/lipsync)
- Music generation (fal-ai/stable-audio)
- Sound effects (fal-ai/sound-effects)
- **AI UI Prototyper** (separate app): upload Salesforce screenshots → describe UI changes in text → GPT-5 Image modifies the screenshot → iterate → generate step-by-step video tutorial with narration
- Python backend (FastAPI) for video assembly with FFmpeg server-side
