# Google Vertex AI Claude Provider for Pi

Access Anthropic Claude models via Google Vertex AI with this Pi extension.

## Installation

```bash
pi install npm:@isaacraja/pi-vertex-claude
```

## Prerequisites

1. **Google Cloud Project** with Vertex AI API enabled
2. **Claude models enabled** in your project's [Model Garden](https://console.cloud.google.com/vertex-ai/model-garden)
3. **Application Default Credentials** configured

## Setup

### 1. Authenticate

```bash
gcloud auth application-default login
```

### 2. Set Environment Variables

```bash
export GOOGLE_CLOUD_PROJECT=your-project-id
export GOOGLE_CLOUD_LOCATION=us-east5  # Optional, defaults to us-east5
```

### 3. Use It

```bash
pi --provider google-vertex-claude --model claude-sonnet-4@20250514
```

## Shell Helper (Recommended)

Add to your `~/.bashrc` or `~/.zshrc`:

```bash
piv() {
  GOOGLE_CLOUD_PROJECT=your-project-id \
  pi --provider google-vertex-claude --model claude-sonnet-4@20250514 "$@"
}
```

Then use:

```bash
piv "Your prompt here"
```

## Available Models

| Model ID | Name | Context | Max Output |
|----------|------|---------|------------|
| `claude-opus-4-5@20251101` | Claude Opus 4.5 | 200K | 32K |
| `claude-opus-4-1@20250805` | Claude Opus 4.1 | 200K | 32K |
| `claude-opus-4@20250514` | Claude Opus 4 | 200K | 32K |
| `claude-sonnet-4-5@20250929` | Claude Sonnet 4.5 | 200K | 64K |
| `claude-sonnet-4@20250514` | Claude Sonnet 4 | 200K | 64K |
| `claude-3-7-sonnet@20250219` | Claude 3.7 Sonnet | 200K | 64K |
| `claude-haiku-4-5@20251001` | Claude Haiku 4.5 | 200K | 64K |
| `claude-3-5-sonnet-v2@20241022` | Claude 3.5 Sonnet v2 | 200K | 8K |
| `claude-3-5-haiku@20241022` | Claude 3.5 Haiku | 200K | 8K |

All models support extended thinking, tool calling, image inputs, and prompt caching.

## Features

- ✅ Full streaming support
- ✅ Extended thinking/reasoning
- ✅ Tool/function calling
- ✅ Image input support
- ✅ Prompt caching
- ✅ Token usage tracking

## Common Issues

**"Vertex AI requires a project ID"**
- Set `GOOGLE_CLOUD_PROJECT` or `GCLOUD_PROJECT`

**"Vertex AI requires Application Default Credentials"**
- Run `gcloud auth application-default login`

**"Model not found" or "Permission denied"**
- Enable the model in [Model Garden](https://console.cloud.google.com/vertex-ai/model-garden)
- Check Vertex AI API is enabled
- Verify IAM permissions (Vertex AI User role)

## License

MIT © Isaac Raja
