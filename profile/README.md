<div align="center">

<a href="https://devupai.com">
  <img src="https://devupai.com/image/devu.png" alt="DEVUP AI" width="200" />
</a>

# DEVUP AI

### AI infrastructure, built for Algeria.

<a href="https://devupai.com">
  <img src="https://readme-typing-svg.demolab.com?font=Inter&weight=600&size=20&duration=2800&pause=900&color=F97316&center=true&vCenter=true&width=620&lines=200%2B+AI+models+through+one+API;Cloud+GPU+%26+CPU+with+per-second+billing;OpenAI+and+Anthropic+compatible;Billed+in+Algerian+Dinar" alt="200+ AI models through one API · Cloud GPU and CPU with per-second billing · OpenAI and Anthropic compatible · Billed in Algerian Dinar" />
</a>

<br />

<a href="https://devupai.com/models"><img src="https://img.shields.io/badge/AI_Models-200%2B-F97316?style=for-the-badge" alt="200+ AI models" /></a>
<a href="https://devupai.com/compute"><img src="https://img.shields.io/badge/Compute-GPU_%26_CPU-2563EB?style=for-the-badge" alt="Cloud GPU and CPU" /></a>
<img src="https://img.shields.io/badge/Billing-DZD-10B981?style=for-the-badge" alt="Billing in Algerian Dinar" />
<img src="https://img.shields.io/badge/API-OpenAI_Compatible-7C3AED?style=for-the-badge" alt="OpenAI-compatible API" />

<a href="https://www.npmjs.com/package/devupai"><img src="https://img.shields.io/npm/v/devupai?style=flat-square&label=devupai&color=CB3837&logo=npm" alt="devupai on npm" /></a>
<a href="https://github.com/devupai-platform/devupai-node/actions"><img src="https://img.shields.io/github/actions/workflow/status/devupai-platform/devupai-node/ci.yml?branch=main&style=flat-square&label=SDK%20CI&logo=github" alt="Node.js SDK CI" /></a>
<img src="https://img.shields.io/node/v/devupai?style=flat-square&label=Node.js&logo=nodedotjs&logoColor=white" alt="Supported Node.js versions" />
<a href="https://status.devupai.com"><img src="https://img.shields.io/badge/status-live-10B981?style=flat-square" alt="System status" /></a>

**[Platform](https://devupai.com)** ·
**[Docs](https://docs.devupai.com)** ·
**[API Reference](https://api-reference.devupai.com)** ·
**[Models](https://devupai.com/models)** ·
**[Compute](https://devupai.com/compute)** ·
**[Integrations](https://devupai.com/integrations)** ·
**[Status](https://status.devupai.com)**

</div>

---

## Why DEVUP AI

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>🔑 One key, every model</h3>
      Chat, reasoning, vision, embeddings, reranking, speech, images and
      video from one API key and one balance. Switch models by changing one
      string.
    </td>
    <td width="33%" valign="top">
      <h3>🇩🇿 Paid locally</h3>
      Fund AI and compute in Algerian Dinar. API responses report their cost
      in DZD, and the dashboard shows usage per request.
    </td>
    <td width="33%" valign="top">
      <h3>🧩 Drop-in compatible</h3>
      Keep your OpenAI or Anthropic SDK: change the base URL and the key.
      Or use the official, fully typed <code>devupai</code> SDK.
    </td>
  </tr>
  <tr>
    <td width="33%" valign="top">
      <h3>⚡ GPU &amp; CPU on demand</h3>
      Launch containers in seconds with SSH, JupyterLab, Network Volumes
      and per-second billing.
    </td>
    <td width="33%" valign="top">
      <h3>🔍 Built to be traced</h3>
      A request id on every API response, notices when a request was
      adjusted, and one dashboard for keys, usage and billing.
    </td>
    <td width="33%" valign="top">
      <h3>🔒 Your data stays yours</h3>
      DEVUP AI never uses your prompts or completions to train any
      model, and does not store them.
    </td>
  </tr>
</table>

---

## Quick Start

**1.** Create an API key in the [dashboard](https://devupai.com/dashboard/api-keys).
**2.** Install the SDK and send your first request:

```bash
npm install devupai
```

```typescript
import DevupAI from "devupai";

const client = new DevupAI({ apiKey: process.env.DEVUP_API_KEY! });

const response = await client.chat.completions.create({
  model: "deepseek-ai/DeepSeek-V4.1-Flash-1017",
  messages: [{ role: "user", content: "Explain artificial intelligence in one paragraph." }],
});

console.log(response.choices[0]?.message?.content);
console.log("Cost:", response._devup?.cost_dzd, "DZD");
```

<details>
<summary><b>Streaming</b></summary>

<br />

```typescript
const stream = await client.chat.completions.create({
  model: "deepseek-ai/DeepSeek-V4.1-Flash-1017",
  messages: [{ role: "user", content: "Write a haiku about Algiers." }],
  stream: true,
  stream_options: { include_usage: true },
});

for await (const chunk of stream) {
  process.stdout.write(chunk.choices[0]?.delta?.content ?? "");
  if (chunk.usage) console.log("\nTokens:", chunk.usage.total_tokens);
}
```

</details>

<details>
<summary><b>Vercel AI SDK</b></summary>

<br />

```bash
npm install devupai ai @ai-sdk/openai-compatible @ai-sdk/provider
```

```typescript
import { generateText } from "ai";
import { createDevupAI } from "devupai/ai";

const devupai = createDevupAI({ apiKey: process.env.DEVUP_API_KEY! });

const { text, usage } = await generateText({
  model: devupai("deepseek-ai/DeepSeek-V4.1-Flash-1017"),
  prompt: "Explain neural networks in simple terms.",
});

console.log(text, usage.totalTokens);
```

</details>

<details>
<summary><b>Python (OpenAI SDK)</b></summary>

<br />

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.environ["DEVUP_API_KEY"],
    base_url="https://api.devupai.com/v1",
)

response = client.chat.completions.create(
    model="deepseek-ai/DeepSeek-V4.1-Flash-1017",
    messages=[{"role": "user", "content": "Hello from Algeria!"}],
)

print(response.choices[0].message.content)
```

</details>

<details>
<summary><b>cURL</b></summary>

<br />

```bash
curl https://api.devupai.com/v1/chat/completions \
  -H "Authorization: Bearer $DEVUP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-ai/DeepSeek-V4.1-Flash-1017",
    "messages": [{ "role": "user", "content": "Hello from Algeria!" }],
    "max_tokens": 256
  }'
```

</details>

| API | Base URL |
|---|---|
| OpenAI-compatible | `https://api.devupai.com/v1` |
| Anthropic Messages | `https://api.devupai.com/anthropic` |

Every model id is listed at [devupai.com/models](https://devupai.com/models),
or with `GET /v1/models` and your key.

> [!IMPORTANT]
> Keep API keys on the server. Never commit them, show them in screenshots, or
> ship them in browser bundles or client-side environment variables.

---

## What You Can Build

| | Capability | Use it for |
|:---:|---|---|
| 💬 | **Language models** | Chat, reasoning, coding, structured output, tool calling, agents |
| 👁️ | **Vision** | Image understanding, visual question answering, OCR |
| 🧭 | **Embeddings** | Semantic search, retrieval, clustering, RAG |
| 📊 | **Reranking** | Sharper search results and retrieval |
| 🎙️ | **Speech recognition** | Multilingual transcription |
| 🔊 | **Text-to-speech** | Multilingual, expressive voices |
| 🎨 | **Images** | Text-to-image generation and image editing |
| 🎬 | **Video** | Text-to-video, image-to-video and video editing |
| 🧪 | **Native inference** | Image classification and other model-specific tasks |

<div align="center">

**[Browse the live model catalog →](https://devupai.com/models)**

</div>

---

## Cloud GPU &amp; CPU Compute

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>🖥️ GPU instances</h3>
      LLM inference, training, fine-tuning and LoRA, image and video
      generation, computer vision, 3D rendering and scientific computing.
    </td>
    <td width="50%" valign="top">
      <h3>⚙️ CPU instances</h3>
      APIs, microservices, agent orchestration, background workers, data
      processing, automation, CI/CD and development environments.
    </td>
  </tr>
</table>

| ⏱️ Per-second billing | 🚀 Starts in seconds | 🔐 SSH access | 📓 JupyterLab | 💾 Network Volumes |
|:---:|:---:|:---:|:---:|:---:|
| Pay for the runtime you use | Containers ready fast | Your key, full admin access | Ready-to-use ML notebooks | Data that survives redeploys |

<details>
<summary><b>GPU classes</b></summary>

<br />

| GPU class | Memory | Suited for |
|---|---:|---|
| **NVIDIA B300** | 288 GB HBM3e | Frontier training, large-scale inference |
| **NVIDIA B200** | 180 GB | Large models, multimodal inference, HPC |
| **NVIDIA H200** | 141 GB | LLM inference, fine-tuning, memory-heavy AI |
| **NVIDIA H100** | Up to 94 GB | Inference, training, accelerated computing |
| **NVIDIA A100** | Up to 80 GB | Training, inference, research, data science |
| **NVIDIA L40S** | 48 GB | Generative AI, rendering, inference |
| **RTX 6000 Ada** | 48 GB | Professional AI and rendering |
| **RTX 5090** | 32 GB | Inference and generative AI |
| **RTX 4090** | 24 GB | Image generation, inference, development |

Availability changes with live inventory. Current options are on
[devupai.com/compute](https://devupai.com/compute).

</details>

<div align="center">

**[Deploy GPU &amp; CPU →](https://devupai.com/compute)**

</div>

---

## The `devupai` SDK

<a href="https://www.npmjs.com/package/devupai"><img src="https://img.shields.io/npm/v/devupai?style=flat-square&label=npm&color=CB3837&logo=npm" alt="npm version" /></a>
<img src="https://img.shields.io/badge/types-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
<img src="https://img.shields.io/badge/runtime_deps-0-10B981?style=flat-square" alt="Zero runtime dependencies" />

<table>
  <tr>
    <td width="50%" valign="top">
      <b>Every endpoint</b><br />
      Chat and streaming, Responses, images, embeddings, reranking, speech,
      transcription, video, native inference, models and balance.
    </td>
    <td width="50%" valign="top">
      <b>Production-ready</b><br />
      Automatic retries with backoff for 429, 502, 503, 504 and network
      errors. Timeouts, cancellation and typed error classes.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <b>Full visibility</b><br />
      <code>.withResponse()</code> returns the request id, notices and raw
      response with every result.
    </td>
    <td width="50%" valign="top">
      <b>Vercel AI SDK 7</b><br />
      <code>devupai/ai</code> plugs DEVUP AI into <code>generateText</code>,
      <code>streamText</code> and Next.js route handlers.
    </td>
  </tr>
</table>

Types are generated from the DEVUP AI OpenAPI specification. Requires
Node.js 22.12 or later. Upgrading from 3.x? Read the
**[migration guide](https://github.com/devupai-platform/devupai-node/blob/main/MIGRATION_V3_TO_V4.md)**.

---

## Works With Your Stack

<div align="center">

<img src="https://img.shields.io/badge/OpenAI_SDK-412991?style=flat-square&logo=openai&logoColor=white" alt="OpenAI SDK" />
<img src="https://img.shields.io/badge/Anthropic_SDK-191919?style=flat-square&logo=anthropic&logoColor=white" alt="Anthropic SDK" />
<img src="https://img.shields.io/badge/Vercel_AI_SDK-000000?style=flat-square&logo=vercel&logoColor=white" alt="Vercel AI SDK" />
<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white" alt="LangChain" />
<img src="https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langgraph&logoColor=white" alt="LangGraph" />
<img src="https://img.shields.io/badge/LlamaIndex-6B46C1?style=flat-square" alt="LlamaIndex" />
<img src="https://img.shields.io/badge/CrewAI-FF5A50?style=flat-square&logo=crewai&logoColor=white" alt="CrewAI" />
<img src="https://img.shields.io/badge/AutoGen-0078D4?style=flat-square" alt="AutoGen" />
<img src="https://img.shields.io/badge/Mastra-111827?style=flat-square" alt="Mastra" />
<img src="https://img.shields.io/badge/Pydantic_AI-E92063?style=flat-square&logo=pydantic&logoColor=white" alt="Pydantic AI" />
<img src="https://img.shields.io/badge/LiteLLM-2563EB?style=flat-square" alt="LiteLLM" />
<br />
<img src="https://img.shields.io/badge/n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white" alt="n8n" />
<img src="https://img.shields.io/badge/Dify-1C64F2?style=flat-square" alt="Dify" />
<img src="https://img.shields.io/badge/Flowise-4F46E5?style=flat-square" alt="Flowise" />
<img src="https://img.shields.io/badge/Open_WebUI-111827?style=flat-square" alt="Open WebUI" />
<img src="https://img.shields.io/badge/Cursor-000000?style=flat-square&logo=cursor&logoColor=white" alt="Cursor" />
<img src="https://img.shields.io/badge/Cline-111827?style=flat-square" alt="Cline" />
<img src="https://img.shields.io/badge/Continue-111827?style=flat-square" alt="Continue" />
<img src="https://img.shields.io/badge/Zed-084CCF?style=flat-square&logo=zedindustries&logoColor=white" alt="Zed" />
<img src="https://img.shields.io/badge/Aider-14B014?style=flat-square" alt="Aider" />
<img src="https://img.shields.io/badge/Codex_CLI-412991?style=flat-square&logo=openai&logoColor=white" alt="Codex CLI" />

**30+ step-by-step guides · [Browse all integrations →](https://devupai.com/integrations)**

</div>

> [!TIP]
> **DEVUP Code** brings DEVUP AI models into VS Code, Cursor and Antigravity.
> [Learn more →](https://devupai.com/code)

---

## Repositories

| Repository | Description | |
|---|---|---|
| [**devupai-node**](https://github.com/devupai-platform/devupai-node) | Official Node.js and TypeScript SDK | <a href="https://www.npmjs.com/package/devupai"><img src="https://img.shields.io/npm/v/devupai?style=flat-square&label=npm&color=CB3837" alt="npm" /></a> |
| [**devupai-python**](https://github.com/devupai-platform/devupai-python) | Official Python SDK | <img src="https://img.shields.io/badge/status-in_development-F59E0B?style=flat-square" alt="In development" /> |
| [**.github**](https://github.com/devupai-platform/.github) | Organization profile | |

---

## Privacy

- DEVUP AI **never uses your prompts or completions to train any model**.
- Open-weight models are served under terms that do not allow training on
  your content. For proprietary models, the model provider's data-use policy
  also applies.
- DEVUP AI does not store prompts or completions.
- Usage metadata is recorded for billing and operations: time, model, token
  counts, latency and cost. It does not include prompt or completion content.
- Prompt caching may keep a prompt for a short time to answer repeated
  prompts faster. See
  [Prompt Caching](https://docs.devupai.com/docs/prompt-caching).

Read the full policies before processing regulated or highly sensitive data:
**[Privacy](https://devupai.com/privacy)** ·
**[Security](https://devupai.com/security)** ·
**[Subprocessors](https://devupai.com/subprocessors)** ·
**[Terms](https://devupai.com/terms)**

---

## Resources

| | |
|---|---|
| 📚 **Documentation** | [docs.devupai.com](https://docs.devupai.com) |
| 🧾 **API reference** | [api-reference.devupai.com](https://api-reference.devupai.com) |
| 🗂️ **Model catalog** | [devupai.com/models](https://devupai.com/models) |
| 🔗 **Integrations** | [devupai.com/integrations](https://devupai.com/integrations) |
| 📝 **Changelog** | [docs.devupai.com/docs/changelog](https://docs.devupai.com/docs/changelog) |
| 🟢 **System status** | [status.devupai.com](https://status.devupai.com) |
| ✉️ **Support** | [support@devupai.com](mailto:support@devupai.com) |

---

<div align="center">

### Start building today

<a href="https://devupai.com/dashboard"><img src="https://img.shields.io/badge/Get_your_API_key-Open_Dashboard-7C3AED?style=for-the-badge" alt="Get your API key" /></a>
<a href="https://devupai.com/compute"><img src="https://img.shields.io/badge/Deploy-GPU_%26_CPU-2563EB?style=for-the-badge" alt="Deploy GPU and CPU compute" /></a>
<a href="https://docs.devupai.com/docs/quickstart"><img src="https://img.shields.io/badge/Read-Quickstart-F97316?style=for-the-badge" alt="Read the quickstart" /></a>

<br /><br />

**Built in Algeria 🇩🇿 Connected to the global AI ecosystem.**

<sub>© DEVUP AI. All rights reserved.</sub>

</div>
