# Vision-based BRD-to-FSD automation starter

Target repository: `Vine521992/AI_BSA_Workflow_Builder3`

This package contains two n8n Cloud workflow exports and versioned GitHub configuration assets.

## Workflow 01 — Vision BRD to FSD draft
- GitHub Push trigger on `main`
- Watches `input/IMAGE/` for PDF, PNG, JPG and JPEG
- Loads universal brand, voice, BA standards, brand tokens, project config and FSD HTML template from GitHub
- Uploads the binary source to OpenAI Files API
- Calls OpenAI Responses API with `input_file` for PDF or `input_image` for image files
- Converts returned HTML to PDF using PDF.co
- Commits draft PDF and review manifest under `output/fsd/draft/`

## Workflow 02 — Publish BA-approved FSD
- Watches `input/APPROVAL/` for `.approve` files
- Reads the marker content as the exact draft PDF path
- Copies that PDF into `output/fsd/approved/`
- The marker commit is the explicit BA approval action. Restrict who can create approval markers.

## Setup
Read `docs/SETUP.md` before importing. Configure credentials in n8n; the JSON files contain credential placeholders only. Both workflows import inactive.

## Project selection
Drop `HUMANA__filename.pdf`, `CENTERWELL__filename.png`, `EISAI__filename.jpg`, or an unprefixed file into `input/IMAGE/`. Unprefixed/unknown project prefix selects `projects/UNIVERSAL/project_config.json`.

## Important
This is an importable starter package, not a deployment into the user's n8n workspace and not a verified live GitHub commit. Test with synthetic, non-confidential documents before activating. Review `docs/SETUP.md` for limitations and security requirements.
