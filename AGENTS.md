# Image Generation

For image generation, use the `baseurl` and `apikey` environment variables by default, and send requests in the OpenAI-compatible API format.

## Asset Organization

Follow these rules for every image-generation task in this workspace:

1. Create one top-level folder per referenced person or subject, using the person's or subject's name, for example `Ally/`.
2. Use `1-原图参考/` inside the subject folder for all original reference images.
3. Create every generation batch folder directly inside the subject folder, alongside `1-原图参考/`. Name it with the current Asia/Shanghai date and time in sortable `YYYYMMDD-HHMMSS` format, for example `Ally/20260825-145423/`. Do not add an intermediate generated-images folder.
4. Save the complete prompt for that batch as `提示词.md` inside the batch folder. It must include:
   - the user's original prompt verbatim;
   - the final production prompt actually sent for each generated variant;
   - the model, API mode, image size, quality, and reference image used.
5. Save every final generated image in the same batch folder. Prefix filenames with two-digit sequence numbers such as `01-` and `02-` so they sort in generation order.
6. Keep reference images only in `1-原图参考/`. Do not leave final generated images in temporary or generic `output/` folders after archiving.
7. Never overwrite an existing reference, batch folder, prompt record, or generated image. Create a new timestamped batch for every new request.
8. Load connection settings from the workspace `.env` before generation. Treat `OPENAI_BASE_URL`/`OPENAI_API_KEY` as the standard equivalents of `baseurl`/`apikey`, and never print secret values.

## Facial Identity Preservation

These rules are mandatory for every generation involving a referenced person:

1. Always use the person's original image from `1-原图参考/` as the authoritative facial identity reference for every generation request. Never use a previously generated image as the identity source.
2. Facial identity has higher priority than hairstyle, expression, makeup, pose, clothing, camera angle, lens distortion, aesthetic style, ethnicity descriptors, or influencer/idol styling.
3. Preserve the original facial landmarks and proportions: eye shape and spacing, eyebrows, nose bridge and tip, lips, cheeks, jawline, face width, skin tone, and natural age appearance.
4. Do not beautify, slim the face, enlarge the eyes, create a V-line jaw, change ethnicity or age, or replace the face with a generic influencer, model, or idol face.
5. For difficult angles, wide-angle perspectives, or major hairstyle changes, provide an additional close facial detail derived from the same original reference when supported by the generation workflow. The original full image must remain the primary reference.
6. Visually compare every generated face with the original reference before delivery. If the identity has noticeably drifted, reject and regenerate the result; do not archive or present it as final.
