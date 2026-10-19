# FactCheck MCP Pack — make your AI verify before it asserts

**FactCheck MCP Pack is an MCP server with six verification tools that make an AI assistant check claims before asserting them. It verifies claims against Wikipedia, fetches live sources, cross-verifies evidence with confidence scoring, and pulls real citations from Semantic Scholar. It runs locally over stdio and needs no API key for five of its six tools.**

**[Get FactCheck MCP Pack — $12 →](https://ritterbeck.gumroad.com/l/factcheck-mcp)** · or get it with three other packs in the [Complete MCP Toolkit](https://github.com/Ritterbeckaj/mcp-toolkit-bundle) for $29.

---

## What's inside

| Tool | What it does | Needs |
|---|---|---|
| `verify_claim` | Checks a claim against Wikipedia → `SUPPORTED` / `PARTIAL` / `NOT VERIFIED` + sources | network, no key |
| `fetch_source` | Fetches a live URL and returns title, HTTP status, and the first N characters | network, no key |
| `cross_verify` | Scores a claim against N independent evidence strings → confidence + stance | **fully local** |
| `get_citations` | Returns real Semantic Scholar papers and their references | network, no key |
| `anti_hallucination_protocol` | The pre-publication workflow to run before asserting anything | **fully local** |
| `check_facts_google` | Queries Google Fact Check Tools ratings | optional free Google key |

Six tools. Five work with zero keys. One optional free key unlocks the sixth.

## The rule it enforces

**Never assert what isn't tagged `VERIFIED`.** When verification comes back `UNKNOWN`, the answer is "UNVERIFIED" — not a guess. The pack supplies structure and evidence; you keep the final judgment.

That is the whole design premise: this is a verification tool that fails *closed*. Given no network, it says `UNVERIFIED` instead of inventing a source. For an anti-hallucination tool, failing that way is the entire point.

## What needs the network — honestly

Most "offline" claims in this space are approximations. Here is the precise split:

| Tool | Network |
|---|---|
| `cross_verify` | **None.** Runs entirely on the evidence you supply. |
| `anti_hallucination_protocol` | **None.** A local workflow. |
| `verify_claim` | Wikipedia — free, keyless, read-only. |
| `get_citations` | Semantic Scholar — free, keyless, read-only. |
| `fetch_source` | The URL you name. Fetching a live source is the feature. |
| `check_facts_google` | Google Fact Check Tools — needs a free key, degrades gracefully without one. |

No telemetry. No account. No per-call billing. Your claims and evidence stay on your machine.

## Install

Requires **Node 18+**.

```bash
cd factcheck-mcp && npm install
```

Add to your MCP client. For OpenCode (`~/.config/opencode/opencode.json`):

```json
{
  "mcp": { "servers": {
    "factcheck": { "type": "local", "command": ["node", "/absolute/path/factcheck-mcp/index.js"] }
  }}
}
```

The same entry goes in Claude Desktop, Claude Code, Cursor, Windsurf, Cline, or any stdio MCP client.

**Optional:** set `GOOGLE_FACTCHECK_API_KEY` to activate `check_facts_google`. Everything else works with zero keys.

## Example prompts

- *"Verify the claim: the Eiffel Tower is in Paris"* → `factcheck_verify_claim`
- *"Cross-verify 'dolphin-llama3 is an uncensored local model' against these 3 sources"* → `factcheck_cross_verify`
- *"Get citations for 'marketing automation'"* → `factcheck_get_citations`
- *"Fetch https://example.com and summarize what it actually claims"* → `factcheck_fetch_source`

## FAQ

### Do I need an API key?

No. Five of the six tools run keyless. The sixth, `check_facts_google`, uses an optional **free** Google Fact Check Tools key; without it, that one tool reports that it's unavailable and the other five are unaffected.

### Does it work offline?

Two tools run fully air-gapped: `cross_verify` and `anti_hallucination_protocol`. The other four read free public endpoints by design — verifying a claim requires going to a source. Offline, they return `UNVERIFIED` rather than guessing.

### Which MCP clients does it work with?

Any stdio MCP client: Claude Desktop, Claude Code, OpenCode, Cursor, Windsurf, Cline, or your own. It's plain MCP over stdio.

### Is this the same as other fact-check MCP projects?

No. This is **FactCheck MCP Pack by [@RitterbeckAj](https://github.com/Ritterbeckaj)** — six tools, distributed via Gumroad. There are unrelated projects with similar names; this repository and its Gumroad page are the official source for *this* one.

### How much does it cost?

$12 one time. No subscription, no per-call cost. It's also included in [The Complete MCP Toolkit](https://github.com/Ritterbeckaj/mcp-toolkit-bundle) ($29 for four packs, 32 tools). 30-day money-back guarantee via Gumroad.

### Does it get updates?

Yes — free updates, republished to the product page.

## Related

- [mcp-toolkit-bundle](https://github.com/Ritterbeckaj/mcp-toolkit-bundle) — all four packs, 32 tools, $29
- [monetize-mcp](https://github.com/Ritterbeckaj/monetize-mcp) — free MIT monetization toolkit (8 tools)
- [lead-gen-mcp](https://github.com/Ritterbeckaj/lead-gen-mcp) — lead generation server (6 tools)
- [strategy-mcp](https://github.com/Ritterbeckaj/strategy-mcp) — strategy frameworks server (12 tools)

## License

Proprietary — licensed per purchaser. 30-day guarantee via Gumroad. This repository contains documentation only; the pack source is delivered with purchase.

**Built by [@RitterbeckAj](https://github.com/Ritterbeckaj).**
