# Contributing

This repository is a **read-only mirror**. A sync generates it from Candle's own source, so a pull
request opened here cannot be merged: the next sync would overwrite it.

`packages/mcp` is here because the CLI bundles the MCP server (`candle mcp`). To connect an agent
or an application without the CLI, use [Candle Agent Kit](https://github.com/candledottv/agent-kit).

## How to help

- **Open an issue here.** Bug reports, install problems and confusing docs are welcome, and issues
  are read. Include the CLI version (`candle --version`), how you installed it, your operating
  system, the command you ran and what it printed. Remove API keys, device codes and recovery
  phrases before you post.
- **MCP server and SDK problems** belong in [candledottv/agent-kit](https://github.com/candledottv/agent-kit/issues).
- **Prose documentation** lives at [docs.candle.tv](https://docs.candle.tv).

## Security

Do not open a public issue for a vulnerability. Follow the disclosure process at
[docs.candle.tv/legal/vulnerability-disclosure](https://docs.candle.tv/legal/vulnerability-disclosure).

## License

MIT, see [LICENSE](LICENSE).
