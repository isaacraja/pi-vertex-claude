# Google Vertex AI Claude Provider for Pi

Access Anthropic Claude models via Google Vertex AI with this Pi extension. Use Claude Opus, Sonnet, and Haiku models through your Google Cloud account.

## Installation

### NPM (Recommended)

```bash
# Install globally (available for all projects)
pi install npm:@isaacraja/pi-vertex-claude

# Or install for specific project
pi install -l npm:@isaacraja/pi-vertex-claude
```

### GitHub

```bash
# Install from GitHub
pi install git:github.com/isaacraja/pi-vertex-claude

# Or with specific version
pi install git:github.com/isaacraja/pi-vertex-claude@v1.0.0
```

### Temporary (Try without installing)

```bash
pi -e npm:@isaacraja/pi-vertex-claude --provider google-vertex-claude --model claude-sonnet-4@20250514
```

## Prerequisites

1. **Google Cloud Project** with Vertex AI API enabled
2. **Claude models enabled** in your project's Model Garden
3. **Application Default Credentials** configured

## Setup

### 1. Authenticate with Google Cloud

```bash
gcloud auth application-default login
```

This creates credentials at `~/.config/gcloud/application_default_credentials.json`.

### 2. Set Environment Variables

```bash
export GOOGLE_CLOUD_PROJECT=your-project-id
export GOOGLE_CLOUD_LOCATION=us-east5  # Optional, defaults to us-east5
```

You can use `GCLOUD_PROJECT` instead of `GOOGLE_CLOUD_PROJECT`.

### 3. Use the Provider

```bash
pi --provider google-vertex-claude --model claude-opus-4-5@20251101
```

## Usage

### Shell Helper (Recommended)

Add to your `~/.bashrc` or `~/.zshrc`:

```bash
piv() {
  GOOGLE_CLOUD_PROJECT=your-project-id \
  GOOGLE_CLOUD_LOCATION=us-east5 \
  pi --provider google-vertex-claude --model claude-opus-4-5@20251101 "$@"
}
```

Then use:

```bash
piv "Your prompt here"
```

### Fish Shell

Add to your `~/.config/fish/config.fish`:

```fish
function piv
  set -x GOOGLE_CLOUD_PROJECT your-project-id
  set -x GOOGLE_CLOUD_LOCATION us-east5
  pi --provider google-vertex-claude --model claude-opus-4-5@20251101 $argv
end
```

## Available Models

| Model ID | Name | Reasoning | Max Tokens |
|----------|------|-----------|------------|
| `claude-opus-4-5@20251101` | Claude Opus 4.5 | ✅ | 32,000 |
| `claude-opus-4-1@20250805` | Claude Opus 4.1 | ✅ | 32,000 |
| `claude-opus-4@20250514` | Claude Opus 4 | ✅ | 32,000 |
| `claude-sonnet-4-5@20250929` | Claude Sonnet 4.5 | ✅ | 64,000 |
| `claude-sonnet-4@20250514` | Claude Sonnet 4 | ✅ | 64,000 |
| `claude-3-7-sonnet@20250219` | Claude 3.7 Sonnet | ✅ | 64,000 |
| `claude-haiku-4-5@20251001` | Claude Haiku 4.5 | ✅ | 64,000 |
| `claude-3-5-sonnet-v2@20241022` | Claude 3.5 Sonnet v2 | ❌ | 8,192 |
| `claude-3-5-haiku@20241022` | Claude 3.5 Haiku | ❌ | 8,192 |

## Features

- ✅ Full streaming support
- ✅ Extended thinking (for reasoning models)
- ✅ Tool/function calling
- ✅ Image input support
- ✅ Prompt caching
- ✅ Token usage tracking and cost calculation

## Thinking Mode

For models with reasoning support (✅), you can enable thinking:

```bash
piv --thinking high "Solve this complex problem"
```

Thinking levels: `minimal`, `low`, `medium`, `high`, `xhigh`.

## Troubleshooting

### "Vertex AI requires a project ID"

Ensure `GOOGLE_CLOUD_PROJECT` or `GCLOUD_PROJECT` is set:

```bash
export GOOGLE_CLOUD_PROJECT=your-project-id
```

### "Vertex AI requires Application Default Credentials"

Run `gcloud auth application-default login` or set `GOOGLE_APPLICATION_CREDENTIALS` to your service account key file.

### "Model not found" or "Permission denied"

1. Ensure the model is enabled in your project's [Model Garden](https://console.cloud.google.com/vertex-ai/model-garden)
2. Check that your project has Vertex AI API enabled
3. Verify your account has the required IAM permissions (`Vertex AI User` role)

## Pricing

See [Vertex AI partner model pricing](https://cloud.google.com/vertex-ai/generative-ai/pricing#partner-models) for current rates.

All costs are calculated in USD per million tokens:

- **Opus 4.5/4.1/4**: $15 input, $75 output
- **Sonnet 4.5/4/3.7**: $3 input, $15 output
- **Haiku 4.5**: $1 input, $5 output
- **Cache reads**: 10% of input cost
- **Cache writes**: 25% additional cost

## Development

```bash
# Clone the repository
git clone https://github.com/isaacraja/pi-vertex-claude.git
cd pi-vertex-claude

# Install dependencies
npm install

# Run tests
npm test

# Test locally with pi
pi -e . --provider google-vertex-claude --model claude-sonnet-4@20250514
```

## License

MIT © Isaac Raja

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Model Source

Model information sourced from `models.dev` (`google-vertex-anthropic`).
