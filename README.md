# Image Text Restore

A Codex skill for making AI-generated and text-heavy images clearer without silently changing their content.

It separates four problems that are often confused:

- adding pixels;
- sharpening visible edges;
- correcting unreadable or malformed text;
- giving dense layouts enough room.

The skill chooses between deterministic enlargement, local generative repair, neural super-resolution, and editable vector reconstruction. It treats model-generated detail as a reconstruction rather than recovered fact.

## Install

Ask Codex:

```text
Use $skill-installer to install the skill from
https://github.com/bosprimigenious/image-text-restore-skill
```

Or clone it manually:

```bash
git clone https://github.com/bosprimigenious/image-text-restore-skill.git \
  ~/.codex/skills/image-text-restore
```

Restart Codex after installing a new skill.

## Use

Attach or identify an image, then ask:

```text
Use $image-text-restore to enlarge this generated illustration to 4K. Preserve the
composition and identity, repair only malformed local details, and compare the result
with a deterministic upscale.
```

For images containing Chinese or dense text:

```text
Use $image-text-restore to make this diagram clearer. Keep every label exact, rebuild
unreadable text with real fonts, and verify the result at 100% zoom.
```

## Deterministic helper

The bundled helper uses Pillow for conventional Lanczos enlargement and restrained sharpening. It does not call an image model or invent missing detail.

```bash
python3 -m pip install Pillow
python3 scripts/enhance_raster.py input.png output.png --scale 2 --mode illustration
```

Available modes are `illustration`, `photo`, and `text`. Use `--dry-run` to inspect the output plan. Existing outputs, giant canvases, shrinking, and major aspect-ratio changes are rejected by default.

## Limits

- Enlarging dimensions alone cannot restore information absent from the source.
- Generative enhancement can invent texture, change identity, distort anatomy, or alter text.
- OCR is a draft transcription and must be checked for important text.
- Dense diagrams may require editable text and geometry rather than image-only enhancement.

See [SKILL.md](SKILL.md) for the workflow, [image-enhancement.md](references/image-enhancement.md) for generated artwork and photographs, and [diagram-restoration.md](references/diagram-restoration.md) for text-heavy layouts.

## License

MIT
