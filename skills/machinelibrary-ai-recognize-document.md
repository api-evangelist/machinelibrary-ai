---
name: machinelibrary-ai-recognize-document
description: Submit your own document to the asynchronous recognition API, poll the job, then fetch the Markdown result and the quality report.
api: openapi/machinelibrary-ai-openapi.yml
operations: [create_recognition, get_recognition, get_recognition_result, get_recognition_report]
generated: '2026-09-19'
method: generated
---

# Recognize a PDF/EPUB/DJVU into Markdown

Base URL `https://api.machinelibrary.ai` (the standalone Recognition spec names `https://api.spacefrontiers.org`, which still works). Authenticate with `X-Api-Key` or a Bearer token. Each accepted submission is billed at the `ocr` price published by `GET /v1/pricing` ($0.01 per submitted document on 2026-09-19); **resubmitting identical content is idempotent and free** (provider statement, Recognition API `info.description`).

## Steps

1. **Submit** — `create_recognition`: `POST /v1/recognitions` as `multipart/form-data` with field `file` (PDF, EPUB or DJVU, up to 100 MB; format is detected from bytes). Expect `202` with a `RecognitionSubmission` body (`{"id": "<uuid>", "status": "pending"}`) and a `Location` header to poll.
2. **Poll** — `get_recognition`: `GET /v1/recognitions/{id}`. The `RecognitionJobStatus` carries `status`, `input_format`, `languages[]`, `created_at` / `started_at` / `completed_at`, `has_result`, `result_url`, `report_url`, and `error_class` on failure. Poll at a modest interval; the job is asynchronous.
3. **Fetch the Markdown** — `get_recognition_result`: `GET /v1/recognitions/{id}/result` returns `text/markdown`. `404` means no such job for this account, or no result yet.
4. **Fetch the quality report** — `get_recognition_report`: `GET /v1/recognitions/{id}/report` returns a JSON object describing recognition quality.

## Errors to handle

- `413` file exceeds the upload limit; `422` unsupported or invalid document (`RecognitionError` envelope `{detail, status: "error"}`); `402` insufficient balance; `429` active-job limit reached — wait for a running job to finish before submitting another (the limit count is not published).
- Because identical resubmissions are free and idempotent, retrying a `create_recognition` after a network failure is safe.
