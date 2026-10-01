<div align="center">

# Reelwish

**One API gateway for video generation models.**

Create, route, price, and deliver video generation tasks through one stable API —
text-to-video, image-to-video, first-frame, last-frame, and reference workflows,
without exposing upstream providers.

[**Website**](https://reelwish.cc) · [**Live page**](https://panqian040312-droid.github.io/reelwish/) · [**Docs**](https://reelwish.cc/docs) · [**Model Square**](https://reelwish.cc/pricing) · [**Console**](https://reelwish.cc/dashboard)

![Base URL](https://img.shields.io/badge/base%20URL-reelwish.cc%2Fv1-2C2C2A?style=flat-square)
![Upstreams](https://img.shields.io/badge/upstream%20services-17%2B-2C2C2A?style=flat-square)
![Model billing](https://img.shields.io/badge/model%20billing-34%2B-2C2C2A?style=flat-square)
![Routes](https://img.shields.io/badge/compatible%20API%20routes-17%2B-2C2C2A?style=flat-square)

</div>

---

## Why Reelwish

Most teams end up building the same thing twice: one integration for the models they
launch with, and another for whichever model they switch to next. Reelwish sits in
between — a single gateway in front of the upstream video providers, so your
integration, your pricing view, and your task tracking all stay in one place.

| | |
|---|---|
| **One stable endpoint** | Point your client at `https://reelwish.cc/v1` and keep it there. Upstream endpoints and upstream credentials never enter your codebase. |
| **Routing you control** | Pick a published model and its supported generation mode per task. New models arrive through the same request shape — no re-write, no re-auth. |
| **Pricing you can query** | `GET /v1/video-prices` returns current USD customer prices. `POST /v1/video-prices/estimate` returns an exact price for the real parameters you are about to submit, before you spend anything. |
| **Built to survive launch day** | Load balancing, rate limiting, retries and cost tracking across 17+ upstream services, with per-task USD charges you can audit. |

Pay only for what you generate. No monthly subscription.

---

## Two ways to use it

### For developers — the API

Sign in, create an API key, and send your first task in minutes. Same key, same
request shape, every generation mode.

```bash
# 1. List the models currently available to your key
curl https://reelwish.cc/v1/models \
  -H "Authorization: Bearer sk-your-api-key"

# 2. Check the current site prices
curl https://reelwish.cc/v1/video-prices \
  -H "Authorization: Bearer sk-your-api-key"

# 3. Submit an asynchronous video task
curl -X POST https://reelwish.cc/v1/videos \
  -H "Authorization: Bearer sk-your-api-key" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "your-video-model",
    "prompt": "A cinematic sunrise over the ocean",
    "mode": "text_to_video",
    "seconds": "5",
    "aspect_ratio": "16:9",
    "resolution": "720p"
  }'

# 4. Poll the task until it finishes (every 3–10 seconds is fine)
curl https://reelwish.cc/v1/videos/task_example \
  -H "Authorization: Bearer sk-your-api-key"

# 5. Download the finished video
curl -L https://reelwish.cc/v1/videos/task_example/content \
  -H "Authorization: Bearer sk-your-api-key" \
  -o result.mp4
```

Add `X-Request-ID` with your own unique value on submission to make timeouts and
support traces easy to follow.

### Endpoints

| Method | Path | Purpose |
|---|---|---|
| `GET` | `/v1/models` | List currently available models |
| `GET` | `/v1/video-prices` | Retrieve current site USD customer prices |
| `POST` | `/v1/video-prices/estimate` | Get an exact price for real parameters, with an optional lane |
| `POST` | `/v1/videos` | Create an asynchronous video task |
| `GET` | `/v1/videos/{task_id}` | Retrieve task status and result |
| `GET` | `/v1/videos/{task_id}/content` | Download a site-hosted result |

Base URL: `https://reelwish.cc/v1` · Auth: `Authorization: Bearer sk-your-api-key`

### For creators — the Studio

No code, no docs, no upstream accounts. Open the [Console](https://reelwish.cc/dashboard),
pick a model, describe what you want, choose the mode and resolution, and generate.
Same gateway underneath, same USD pricing, same task history — you just work in a
browser instead of a terminal.

---

## Generation modes

`text_to_video` · `image_to_video` · first-frame · last-frame · reference video

## Gateway capabilities

- **Load balancing** across upstream services
- **Rate limiting** and retry handling
- **Cost tracking** — real-time usage monitoring and per-task USD charges
- **Multi-region deployment** for stable global access
- **Team collaboration** — multi-user management with permission allocation
- **Compatible API routes** for common AI application workflows

---

## Links

| | |
|---|---|
| Website | https://reelwish.cc |
| API documentation | https://reelwish.cc/docs |
| Model Square & pricing | https://reelwish.cc/pricing |
| Console | https://reelwish.cc/dashboard |
| Model rankings | https://reelwish.cc/rankings |
| About | https://reelwish.cc/about |

---

<div align="center">

© 2026 Reelwish — Affordable, high-quality AI video generation for creators worldwide.

</div>
