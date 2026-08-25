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
