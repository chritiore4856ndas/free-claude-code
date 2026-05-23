# free-claude-code

A free, open-source implementation of Claude Code — an AI-powered coding assistant that runs in your terminal.

Forked from [Alishahryar1/free-claude-code](https://github.com/Alishahryar1/free-claude-code).

## Features

- 🤖 AI-powered code generation and editing
- 💻 Terminal-based interface
- 🔧 File system operations (read, write, create, delete)
- 🔍 Code search and navigation
- 🧪 Test execution and debugging
- 🌐 Multiple AI provider support

## Requirements

- Python 3.11+
- An API key for a supported AI provider

## Installation

```bash
# Clone the repository
git clone https://github.com/your-username/free-claude-code.git
cd free-claude-code

# Install dependencies
pip install -e .
```

## Configuration

Copy `.env.example` to `.env` and fill in your API credentials:

```bash
cp .env.example .env
```

Then edit `.env` with your preferred editor and add your API keys.

## Usage

```bash
# Start the assistant in the current directory
python -m free_claude_code

# Or if installed as a package
free-claude-code
```

## Supported Providers

| Provider | Models |
|----------|--------|
| Anthropic | claude-3-5-sonnet, claude-3-opus |
| OpenAI | gpt-4o, gpt-4-turbo |
| OpenRouter | Various models via API |
| Groq | llama, mixtral models |

## Development

```bash
# Install dev dependencies
pip install -e ".[dev]"

# Run tests
pytest

# Run with debug logging
DEBUG=1 python -m free_claude_code
```

## Contributing

Pull requests are welcome! Please read [AGENTS.md](AGENTS.md) before contributing.

## License

MIT — see [LICENSE](LICENSE) for details.
