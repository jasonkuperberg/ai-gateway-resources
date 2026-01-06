# AI Gateway Resources

A comprehensive guide to AI gateways and unified LLM API platforms for developers. Compare top AI gateway solutions, explore integration examples, and simplify your multi-model LLM infrastructure.

---

## What Is an AI Gateway?

An **AI gateway** (also called an **LLM gateway** or **LLM proxy**) is a unified API layer that sits between your application and multiple large language model providers. Instead of integrating separately with OpenAI, Anthropic, Google, Mistral, and others, an AI gateway provides a single endpoint to access all of them.

**Key benefits of using an AI gateway:**

- **Unified API** — One SDK and consistent request format across all LLM providers
- **Model Fallbacks** — Automatically route to backup models when primary providers fail
- **Cost Optimization** — Compare pricing and route requests to the most cost-effective LLM
- **Load Balancing** — Distribute traffic across providers to avoid rate limits
- **Observability** — Centralized logging, monitoring, and analytics for all LLM calls
- **Caching** — Reduce costs and latency with semantic caching of responses

---

## Best AI Gateway Platforms

| Platform | Open Source | Key Strength | Best For |
|----------|-------------|--------------|----------|
| [OpenRouter](#openrouter) | No | 300+ models, pay-per-use | Startups, indie devs |
| [Vercel AI SDK](#vercel-ai-sdk) | Yes | Next.js integration, streaming | Frontend developers |
| [Portkey](#portkey) | Partial | Observability, enterprise features | Production teams |
| [LiteLLM](#litellm) | Yes | Self-hosted, 100+ providers | Cost-conscious teams |
| [Kong AI Gateway](#kong-ai-gateway) | Partial | Enterprise API management | Large organizations |
| [Cloudflare AI Gateway](#cloudflare-ai-gateway) | No | Edge caching, global network | Performance-focused apps |

---

## [OpenRouter](https://openrouter.ai)

**OpenRouter** is a unified LLM gateway that provides access to 500+ models from OpenAI, Anthropic, Google, Meta, Mistral, and open-source providers through a single API. It offers pay-as-you-go pricing with no monthly minimums, and even provides access to [free AI models](https://openrouter.ai/collections/free-models) for experimentation and development.

### OpenRouter Integration

> Code adapted from [OpenRouter Quickstart Documentation](https://openrouter.ai/docs/quickstart)

```python
import openai

client = openai.OpenAI(
    base_url="https://openrouter.ai/api/v1",
    api_key="your-openrouter-api-key",
)

response = client.chat.completions.create(
    model="google/gemini-3-flash-preview",
    messages=[
        {"role": "user", "content": "How do I integrate OpenRouter with my Python application?"}
    ]
)

print(response.choices[0].message.content)
```

### OpenRouter Resources

- [OpenRouter Documentation](https://openrouter.ai/docs/quickstart)
- [Model List & Pricing](https://openrouter.ai/models)
- [API Reference](https://openrouter.ai/docs/api-reference/overview)

---

## [Vercel AI SDK](https://sdk.vercel.ai)

The **Vercel AI SDK** is an open-source TypeScript toolkit for building AI-powered applications and agents. It provides a unified interface for streaming text, generating structured data, and integrating with React, Next.js, Vue, Svelte, and Node.js—making it easy to switch between LLM providers with minimal code changes.

### Vercel AI SDK Integration

> Code adapted from [Vercel AI SDK Documentation](https://ai-sdk.dev/docs/ai-sdk-core/generating-text)

```typescript
import { generateText } from 'ai';
import { anthropic } from '@ai-sdk/anthropic';

const { text } = await generateText({
  model: anthropic('claude-sonnet-4-5-20250929'),
  prompt: 'How do I integrate the Vercel AI SDK with Next.js?',
});

console.log(text);
```

### Vercel AI SDK Resources

- [Vercel AI SDK Documentation](https://sdk.vercel.ai/docs/introduction)
- [Supported Providers](https://sdk.vercel.ai/providers)
- [GitHub Repository](https://github.com/vercel/ai)

---

## [Portkey](https://portkey.ai)

**Portkey** is an AI gateway built for production LLM applications. It offers advanced features like automatic retries, fallbacks, load balancing, and detailed observability—all through an OpenAI-compatible API. Portkey connects to 1,600+ models across 45+ providers and includes enterprise features like guardrails and governance.

### Portkey Integration

> Code adapted from [Portkey Getting Started Documentation](https://portkey.ai/docs/guides/getting-started/getting-started-with-ai-gateway)

```python
from portkey_ai import Portkey

client = Portkey(
    api_key="your-portkey-api-key",
    virtual_key="your-anthropic-virtual-key"
)

response = client.chat.completions.create(
    model="claude-sonnet-4-5-20250929",
    messages=[
        {"role": "user", "content": "How do I integrate Portkey with my existing OpenAI code?"}
    ]
)

print(response.choices[0].message.content)
```

### Portkey Resources

- [Portkey Documentation](https://portkey.ai/docs)
- [AI Gateway Features](https://portkey.ai/features/ai-gateway)
- [GitHub Repository](https://github.com/Portkey-AI/gateway)

---

## [LiteLLM](https://litellm.ai)

**LiteLLM** is an open-source LLM gateway that provides a unified interface for 100+ LLM providers. It can be used as a Python SDK or self-hosted as a proxy server, making it ideal for teams that need full control over their AI infrastructure with features like cost tracking, guardrails, and load balancing.

### LiteLLM Integration

> Code adapted from [LiteLLM Getting Started Documentation](https://docs.litellm.ai/docs/)

```python
from litellm import completion

response = completion(
    model="gpt-5.2",
    messages=[
        {"role": "user", "content": "How do I integrate LiteLLM as a proxy server?"}
    ],
    fallbacks=["anthropic/claude-sonnet-4-5-20250929"]
)

print(response.choices[0].message.content)
```

### LiteLLM Proxy Server

> Code adapted from [LiteLLM Proxy Documentation](https://github.com/BerriAI/litellm)

```bash
# Start the LLM proxy server
litellm --model gpt-5.2

# Now use it as an OpenAI-compatible endpoint
curl http://localhost:4000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-5.2", "messages": [{"role": "user", "content": "Hello"}]}'
```

### LiteLLM Resources

- [LiteLLM Documentation](https://docs.litellm.ai)
- [Supported Providers](https://docs.litellm.ai/docs/providers)
- [GitHub Repository](https://github.com/BerriAI/litellm)

---

## [Kong AI Gateway](https://konghq.com/products/kong-ai-gateway)

**Kong AI Gateway** extends Kong's enterprise API management platform with AI-specific features. It provides a Universal LLM API to route across multiple providers like OpenAI, Anthropic, Google Gemini, AWS Bedrock, and more—with traffic control, security, governance, and 15+ AI plugins for observability, semantic caching, and prompt guards.

### Kong AI Gateway Integration

> Configuration adapted from [Kong AI Gateway Documentation](https://docs.konghq.com/gateway/latest/get-started/ai-gateway/)

```yaml
# kong.yaml - Declarative configuration
_format_version: "3.0"
services:
  - name: llm-service
    url: https://api.openai.com
    routes:
      - name: llm-route
        paths:
          - /chat
    plugins:
      - name: ai-proxy
        config:
          route_type: llm/v1/chat
          auth:
            header_name: Authorization
            header_value: Bearer <your-openai-api-key>
          model:
            provider: openai
            name: gpt-5.2
```

### Kong AI Gateway Resources

- [Kong AI Gateway Documentation](https://developer.konghq.com/ai-gateway/)
- [AI Plugins Hub](https://developer.konghq.com/index/ai-gateway/)
- [Getting Started Guide](https://docs.konghq.com/gateway/latest/get-started/ai-gateway/)

---

## [Cloudflare AI Gateway](https://developers.cloudflare.com/ai-gateway/)

**Cloudflare AI Gateway** leverages Cloudflare's global edge network to provide caching, rate limiting, and analytics for AI applications. It supports 350+ models across providers like OpenAI, Anthropic, Google, and more—reducing costs through response caching and improving latency with edge computing. Connect with just one line of code.

### Cloudflare AI Gateway Integration

> Code adapted from [Cloudflare AI Gateway Documentation](https://developers.cloudflare.com/ai-gateway/get-started/)

```javascript
import OpenAI from "openai";

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
  baseURL: "https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_id}/openai",
});

const response = await openai.chat.completions.create({
  model: "gpt-5.2",
  messages: [
    { role: "user", content: "How do I integrate Cloudflare AI Gateway with the OpenAI SDK?" }
  ],
});

console.log(response.choices[0].message.content);
```

### Cloudflare AI Gateway Resources

- [Cloudflare AI Gateway Docs](https://developers.cloudflare.com/ai-gateway/)
- [Supported Providers](https://developers.cloudflare.com/ai-gateway/providers/)
- [Unified API (OpenAI Compatible)](https://developers.cloudflare.com/ai-gateway/usage/chat-completion/)

---

## Future Plans

This repository is under active development. Planned additions include:

- [ ] `/integrations` — Detailed setup guides for each LLM gateway platform
- [ ] `/models` — Comprehensive model availability comparison across AI gateways
- [ ] `/pricing` — Cost comparison calculator and LLM pricing breakdowns
- [ ] `/benchmarks` — Latency and performance benchmarks for each gateway
- [ ] `/examples` — Production-ready code samples and starter templates
