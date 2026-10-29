# Candle CLI

Your wallets and agent tools, one command away.

[Agent Kit](https://github.com/candledottv/agent-kit) · **CLI** · TUI (in development)

[![Release](https://img.shields.io/github/v/release/candledottv/cli?filter=cli-v*&label=candle&color=111113)](https://github.com/candledottv/cli/releases/latest)
[![Docs](https://img.shields.io/badge/docs-docs.candle.tv-111113)](https://docs.candle.tv/developers/cli)
[![License: MIT](https://img.shields.io/badge/license-MIT-111113)](LICENSE)

## Install

On macOS with Homebrew:

```sh
brew install candledottv/tap/candle
```

<details>
<summary>Linux and direct installation</summary>

Supported: macOS 13 or later and Linux, each on arm64 and x64.

```sh
curl -fsSL https://candle.tv/install.sh | bash
```

The installer checks the download's SHA-256 and verifies its signature before it writes anything.
It needs `curl`, `sha256sum` or `shasum`, and one signature verifier: `cosign` 2.2 or later, or a
signed-in `gh`. Without a verifier it stops and installs nothing, and tells you how to get one.
It installs `candle` into `~/.local/bin`.

[Verify a release yourself](https://docs.candle.tv/developers/verify-a-candle-release)

</details>

## First three commands

```sh
candle --help    # See the command groups
candle setup     # Connect your account and configure the client
candle portfolio # Read holdings after setup
```

`candle --help` works straight away. `candle setup` and `candle portfolio` need a Candle account:
setup opens a browser page to authorize this device and stores an API key in your OS keychain. A
vault is optional.

Want to try market data first, with no account?
[Try a market read with Agent Kit](https://github.com/candledottv/agent-kit#try-a-market-read-no-account-required).

<details>
<summary>Transcript of the recorded local session (Demo data)</summary>

```text
Demo data $ candle --help | head -n 9
candle: Candle from the terminal: trade, launch, and hold your keys on your own machine

Usage: candle <command> [<subcommand>] [flags]
       candle help <command>                a command's subcommands, flags and examples

Start here
  setup       One wizard: authorize, fund, connect, verify
  auth        Authorize this device, or show and clear its credentials
  doctor      Diagnose CLI setup: credentials, storage backend, API reachability, security key helper
Demo data $

--- next screen ---

Demo data $ CANDLE_API_KEY=demo-not-a-credential candle portfolio --chain solana --no-perps
Profile demo-data · Account unknown (CANDLE_API_KEY override) · http://127.0.0.1:40571

GROUP  CHAIN   WALLET                                  TOKEN  AMOUNT  PRICE    VALUE
-----  ------  --------------------------------------  -----  ------  -------  -------
tee    solana  Demo data: practice wallet (Demo…1111)  SOL    2       $100.00  $200.00

vault           -  no vault at ~/.config/candle/vault.enc
tee       $200.00  1 wallet
embedded    $0.00  0 wallets
solana    $200.00  1 wallet
total     $200.00  every holding priced
Demo data $

--- next screen ---

Demo data $ candle mcp --read-only --print-config
Profile demo-data · Account unknown · http://127.0.0.1:40571

{
  "mcpServers": {
    "candle": {
      "command": "/usr/local/bin/candle",
      "args": [
        "mcp",
        "--read-only"
      ]
    }
  }
}
Demo data $
```

The portfolio uses a synthetic local fixture marker, not an account key. The amounts are Demo data;
using your own portfolio requires account setup. The MCP configuration is read-only and contains no key.

</details>

## Wallets and custody

Your keys can stay on this machine in an encrypted vault that opens with a passphrase or a FIDO2
security key, and no Candle server sees them. The vault is optional; you can use Candle with only
an API key.

To let an agent trade without unlocking your vault, `candle vault promote` places a key in a
hardware enclave (TEE), bound to one API key. That changes who can use the key; it does not fund
the wallet. Funding, transfers and sweeping back to your vault are separate commands.
[CLI custody](https://docs.candle.tv/developers/cli-custody)

## Agents and automation

`candle mcp` runs the Candle MCP server inside the CLI, using the key it stores, so no key sits in
a client config file. `candle mcp --print-config` prints the client block for this install.
The MCP server is a bundled part of the CLI. To connect an agent without installing the CLI, use
[Agent Kit](https://github.com/candledottv/agent-kit).

Through a direct MCP connection, authorized writes run without a local prompt. The preview
`candle core mcp` route turns live money writes into approval cards instead.
[The MCP server](https://docs.candle.tv/developers/cli#the-mcp-server)

## Trading tools

Swap, launch, stake and read P&L on Solana and Hood from commands that print exactly one JSON value
with `--json`, for scripts and CI. Trades and launches take a client id: retry with the same id
after a timeout and it never runs twice.
[Command reference](https://docs.candle.tv/developers/cli#commands) ·
[Headless and CI use](https://docs.candle.tv/developers/cli#headless-and-ci-use)

> **Agents and money.** A scoped API key can move funds within its permissions. Use the minimum
> permissions and limits required for the job. Local approval cards apply when tools run through
> the Candle core; a direct MCP or SDK connection can execute authorized writes. Revoke compromised
> credentials, and reconcile uncertain transaction outcomes before retrying. Limits and approvals
> do not prevent trading losses.

## Other ways to install

| Route | Command | Notes |
| --- | --- | --- |
| npm | `npm i -g @candledottv/cli` | Node 18 or later. Use this on Windows and on macOS 12 or earlier. |
| Run once | `bunx @candledottv/cli <command>` | Nothing installed permanently. |
| Direct binary | [Releases](https://github.com/candledottv/cli/releases) | Verify with [these steps](https://docs.candle.tv/developers/verify-a-candle-release). |

## Updates and verification

- `candle update` installs the latest signed release and verifies it first. Homebrew and npm
  installs update through their own package managers.
- `candle verify` checks a downloaded release asset's signature.
- [Release notes](https://docs.candle.tv/developers/cli-release-notes) ·
  [Verify a Candle release](https://docs.candle.tv/developers/verify-a-candle-release)

## More

- [Full command reference](https://docs.candle.tv/developers/cli) ·
  [Quick start and FAQ](https://docs.candle.tv/developers/cli-quickstart)
- [Vulnerability disclosure](https://docs.candle.tv/rights-and-reporting/vulnerability-disclosure):
  report security issues privately, never in a public issue.
- This repository is generated from Candle's private monorepo, so pull requests cannot be merged
  here. Issues are read and welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).
- MIT, see [LICENSE](LICENSE).
