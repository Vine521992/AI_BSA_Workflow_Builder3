# Setup guide — Vision BRD-to-FSD for n8n Cloud

Repository: `Vine521992/AI_BSA_Workflow_Builder3`
Branch: `main`
Input: `input/IMAGE/` (PDF, PNG, JPG, JPEG)
Draft output: `output/fsd/draft/`
Approved output: `output/fsd/approved/`

## 1. GitHub preparation
1. Make the repository private before using real client documents.
2. Ensure folders/config files from this package are committed to `main`.
3. Create a fine-grained PAT limited to this repository. Grant Metadata read, Contents read/write, and Webhooks read/write.
4. In n8n create a GitHub API credential for the GitHub Trigger.
5. Create an HTTP Header Auth credential named `GitHub REST API`: header `Authorization`, value `Bearer <PAT>`.
6. Add `Accept: application/vnd.github+json` and `X-GitHub-Api-Version: 2022-11-28` as node headers.

## 2. OpenAI credential
Create an HTTP Header Auth credential named `OpenAI API`: header `Authorization`, value `Bearer <OPENAI_API_KEY>`. The workflow uses OpenAI Files API and Responses API. Configure this credential on both OpenAI HTTP Request nodes. The selected model in the workflow is `gpt-4.1`; change it to a vision-capable model available to your account if necessary.

## 3. PDF conversion credential
Create an HTTP Header Auth credential named `PDF.co API`: header `x-api-key`, value `<PDFCO_API_KEY>`. Attach it to the HTML-to-PDF HTTP Request node. Check your organization's approval to send documents to this processor.

## 4. Import workflows
Import both JSON files from `workflows/`. Set credentials on the trigger and relevant HTTP Request nodes. The exported workflows contain credential placeholders only; credentials are never included.

## 5. Configure GitHub Trigger
Both workflows listen for Push events on `Vine521992/AI_BSA_Workflow_Builder3`. Ensure the trigger webhook is created successfully. Use the `main` branch.

## 6. Source naming and project selection
Drop supported files in `input/IMAGE/`. To select a project, prefix the filename, e.g. `HUMANA__Eligibility_BRD.pdf`, `CENTERWELL__Roles_BRD.png`, or `EISAI__HCP_Engagement_BRD.jpg`. The starter workflow currently records the project prefix and applies universal instructions; project-specific JSON files are included as governed reference configuration and must be wired into the prompt loader before relying on them for production decisions.

## 7. Draft then approve
Workflow 01 creates a PDF and review manifest in `output/fsd/draft/`. Review the draft. To approve, create a `.approve` file under `input/APPROVAL/` containing the exact draft PDF path, then commit. Workflow 02 copies that PDF to `output/fsd/approved/`. A marker commit is the approval action; restrict repository write access so only authorized BA reviewers can create markers.

## 8. Test plan
- Use synthetic/non-confidential PDF, PNG and JPG samples.
- Test a searchable PDF, a scanned PDF, an image containing a table and an image containing a flowchart.
- Confirm the OpenAI upload response includes a file ID.
- Confirm Responses API returns `output_text` HTML.
- Confirm PDF.co returns a PDF URL and binary download succeeds.
- Confirm draft appears only in `output/fsd/draft/`.
- Confirm no approved file appears until an authorized marker is committed.
- Test duplicate pushes, multi-file pushes, deleted files and unsupported file extensions.

## 9. Important limitations in this starter
- GitHub push events are commit-based. A push can contain multiple changed files; test multi-file handling.
- Project configuration files are dynamically retrieved, but verify that each project JSON contains only approved, current rules before production. The starter project files are conservative examples, not authoritative client specifications.
- A full production implementation should add retry/backoff, file size limits, idempotency, deletion handling, structured requirement extraction, quality review, source-page citations, and execution audit records.
- PDF/image size and OpenAI Files API limits apply. Confirm current API limits and model availability in your account.
- This workflow is a starter export, not a deployed or tested workflow in your n8n account.

## Security
Keep repository private. Store API keys only in n8n credentials. Avoid logging binary contents, prompts containing sensitive information, or PHI/PII. Confirm OpenAI and PDF processor data-processing terms with your organization before production use.
