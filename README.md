# Video to Audio API

Generate synchronized sound from silent video or create sound from a text prompt. This guide focuses on the video-to-audio workflow and its duration controls.

[Muapi Video to Audio API landing page](https://muapi.ai/video-to-audio) · [API reference](https://muapi.ai/docs/api-reference) · [Create an API key](https://muapi.ai/access-keys)

## Related Projects

- [Video-Upscaler-API](https://github.com/Anil-matcha/Video-Upscaler-API)
- [AI-Music-API](https://github.com/Anil-matcha/AI-Music-API)

## What this API covers

Use the endpoint that matches the task and input media. The routes below are enabled Muapi model IDs checked against the current model catalog; availability, request fields, and pricing can change, so verify the linked landing page and endpoint schema before production use.

| Endpoint | Purpose | Category |
|---|---|---|
| `mmaudio-v2-video-to-video` | v2 Video to Video | `Video to Video` |
| `mmaudio-v2-text-to-audio` | v2 Text to Audio | `Text to Audio` |

## Quick start

Muapi uses an asynchronous REST contract. Submit a JSON request with your API key, save the returned `request_id`, then poll the result endpoint. Replace sample URLs with files you control and fields with values supported by the selected endpoint.

```bash
curl -X POST https://api.muapi.ai/api/v1/mmaudio-v2-video-to-video \
  -H "Content-Type: application/json" \
  -H "x-api-key: $MUAPI_API_KEY" \
  -d '{
    "prompt": "Indian holy music",
    "video_url": "https://example.com/replace-with-your-file"
  }'
```

### Request fields in this example

| Field | Requirement | Notes |
|---|---|---|
| `prompt` | Required | The prompt to generate the audio for. |
| `video_url` | Required | The URL of the video to generate the audio for. |

### Poll for the result

```bash
curl "https://api.muapi.ai/api/v1/predictions/$REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_API_KEY"
```

Poll until the task status is `completed` or `failed`. Read the response’s output URLs on completion; download outputs you need to retain, since provider-hosted URLs may expire.

## Choosing an endpoint

Compare supported inputs and output behavior first, then resolution, duration, quality controls, latency, and price for your use case. Similar names do not guarantee interchangeable request schemas. This repository lists representative routes; the [landing page](https://muapi.ai/video-to-audio) contains the current task-specific explanation, examples, and pricing context.

## Errors and production notes

- Keep the API key in an environment variable; do not commit credentials.
- Validate inputs against the selected endpoint’s current schema.
- Handle non-success HTTP responses and failed task states explicitly.
- Retry only when appropriate for the error; avoid submitting duplicate billable jobs after a timeout without checking the original `request_id`.
- Confirm current pricing and availability on the Muapi page before estimating production cost.

## Links

- [Muapi Video to Audio API](https://muapi.ai/video-to-audio)
- [API reference](https://muapi.ai/docs/api-reference)
- [Playground](https://muapi.ai/playground)
- [API key setup](https://muapi.ai/access-keys)
