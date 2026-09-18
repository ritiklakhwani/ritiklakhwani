<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=22&duration=3000&pause=1200&color=FFFFFF&center=true&vCenter=true&width=700&height=45&lines=Ritik+Lakhwani+%C2%B7+backend+engineer;Real-time+pipelines+and+agent+infrastructure;Node.js+%C2%B7+TypeScript+%C2%B7+Postgres+%C2%B7+Redis+%C2%B7+Solidity">
    <img alt="Ritik Lakhwani, backend engineer" src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=22&duration=3000&pause=1200&color=0A0A0A&center=true&vCenter=true&width=700&height=45&lines=Ritik+Lakhwani+%C2%B7+backend+engineer;Real-time+pipelines+and+agent+infrastructure;Node.js+%C2%B7+TypeScript+%C2%B7+Postgres+%C2%B7+Redis+%C2%B7+Solidity">
  </picture>
</p>

<p align="center">
  Backend engineer building real-time pipelines and the infrastructure AI agents run on.<br>
  Prizes at ETHOnline 2026 and ETHGlobal Bangkok ($2,000).
</p>

<p align="center">
  <a href="https://oceandev.xyz">oceandev.xyz</a> &nbsp;·&nbsp;
  <a href="mailto:ritiklakhwani28@gmail.com">Email</a> &nbsp;·&nbsp;
  <a href="https://x.com/ritiklakhwani">X</a> &nbsp;·&nbsp;
  <a href="https://www.linkedin.com/in/ritiklakhwani">LinkedIn</a>
</p>

---

### Hackathons &nbsp;<sub>6 ETHGlobal events · prizes at 4</sub>

| Result | Event | Project | What was hard |
|:--|:--|:--|:--|
| **Prize winner** | ETHOnline 2026 | [Preflight](https://github.com/ritiklakhwani/preflight) | Judging contracts by on-chain history, not by text the deployer wrote |
| **$2,000** | Bangkok 2024 | [ZK Credit Score](https://github.com/ritiklakhwani/zk-credit-score-eth-global-bangkok) <sub>[showcase](https://ethglobal.com/showcase/zk-credit-score-pa7r4)</sub> | Cross-chain balance proofs with vlayer Teleport that keep balances private |
| Built | Open Agents 2026 | [PetCity](https://github.com/ritiklakhwani/eth-open-agents) | One process and one P2P node per agent, under a single supervisor |

<sub>Also: Singapore 2024, [Inspector AI](https://ethglobal.com/showcase/inspector-ai-s5mw5) (Worldcoin pool prize) · ETHOnline 2024, [BlockGood](https://ethglobal.com/showcase/blockgood-qha9s) (Sign Protocol pool prize) · New Delhi 2025, [WalShare](https://ethglobal.com/showcase/walshare-sfg9s)</sub>

---

### Projects

<table>
<tr>
<td width="50%" valign="top">
<b><a href="https://github.com/ritiklakhwani/preflight">Preflight</a></b><br>
The check an AI agent runs before it signs. Scores a contract on its on-chain history and sends risky approvals to a Ledger.<br>
<sub>~12 s per verdict · 11 checks · 3 chains · 167 tests</sub><br>
<sub>TypeScript · MCP · PostgreSQL · The Graph · Ledger</sub>
</td>
<td width="50%" valign="top">
<b><a href="https://github.com/ritiklakhwani/real-time-data-aggregation-service">Solana market pipeline</a></b><br>
DexScreener and Jupiter merged into one live token feed, cached in Redis and pushed to clients over WebSockets.<br>
<sub>2 s cycle · 2 sources · 4 services sharing only Redis</sub><br>
<sub>TypeScript · Redis pub/sub · ws · Express · Docker</sub>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<b><a href="https://github.com/ritiklakhwani/eth-open-agents">PetCity</a></b><br>
Persistent AI agents as transferable NFTs, each running as its own process and P2P node, acting for its owner on-chain.<br>
<sub>1 process + 1 P2P node per agent · 4 contracts · 5 workflow types</sub><br>
<sub>Fastify · Socket.IO · SQLite · Foundry · viem · Claude</sub>
</td>
<td width="50%" valign="top">
<b><a href="https://github.com/ritiklakhwani/csv-to-crm-ai-pipeline">CSV to CRM</a></b> &nbsp;<sub><a href="https://csv-to-crm-ai-pipeline-frontend.vercel.app/">live</a></sub><br>
Maps any lead CSV onto a fixed CRM schema with a two-phase LLM pipeline and a validator that trusts nothing.<br>
<sub>25-row batches, 4 in flight · 3 attempts per batch · 15 fields</sub><br>
<sub>Express · OpenAI · Zod · SSE · Next.js</sub>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<b><a href="https://github.com/ritiklakhwani/notification-microservice">Notification service</a></b><br>
The API publishes an event and returns. A separate service renders and delivers email from priority queues.<br>
<sub>3 priority queues · SET NX dedupe per job · non-blocking API</sub><br>
<sub>Bun · Redis · PostgreSQL · Prisma · Resend</sub>
</td>
<td width="50%" valign="top">
<b>More</b><br>
<a href="https://github.com/ritiklakhwani/agent-marketplace">AgentBazaar</a> &nbsp;<sub><a href="https://agentbazaar.oceandev.xyz/">live</a></sub><br>
<sub>AI agents that bid on and pay each other in USDC over x402</sub><br>
<a href="https://github.com/ritiklakhwani/web3-realtime-stream-proxy">stream-proxy</a><br>
<sub>Exchange WebSocket feed, fanned out to clients by subscription</sub><br>
<a href="https://github.com/ritiklakhwani/solana-wallet-monitor">wallet-monitor</a><br>
<sub>Rust service watching Solana balance changes</sub>
</td>
</tr>
</table>

<details>
<summary><b>Demos and architecture</b></summary>
<br>

**Preflight**: how a verdict is made

```mermaid
flowchart LR
    A["AI agent<br/>holds the signing key"] -->|preflight_check| M["MCP server<br/>+ engine"]
    M --> E["Etherscan V2<br/>source, ABI, deployer"]
    M --> G["The Graph<br/>Uniswap V3, 3 chains"]
    E -->|contract-written text| Q["Quarantine<br/>sealed before any model reads it"]
    Q --> S["score()<br/>deterministic, no model"]
    G --> S
    S -->|every verdict| P[("Postgres")]
    S -->|HIGH| L["Ledger<br/>physical press"]
    S -->|verdict| A
    L -->|approve or refuse| A
```

<img src="https://raw.githubusercontent.com/ritiklakhwani/preflight/main/docs/images/verdict.png" alt="Preflight rating a token HIGH 94 of 100" width="640">

**Solana market pipeline**

https://github.com/user-attachments/assets/e54436c3-9675-4eb6-ab80-389c69d1f09c

**CSV to CRM**

https://github.com/user-attachments/assets/68c84078-4243-4c73-85dd-7d3101548503

</details>

---

### Stack

<table>
<tr>
<td><b>Backend</b></td><td>Node.js, TypeScript, Bun, Express, Fastify, WebSockets, SSE</td>
<td><b>Data</b></td><td>PostgreSQL, Prisma, Redis, MongoDB, SQLite</td>
</tr>
<tr>
<td><b>Infra</b></td><td>Docker, Nginx, Linux, Cloudflare</td>
<td><b>Applied AI</b></td><td>MCP servers, OpenAI and Anthropic SDKs, structured outputs</td>
</tr>
<tr>
<td><b>Chain</b></td><td>Solidity, Foundry, viem, The Graph, Solana</td>
<td><b>Frontend</b></td><td>React, Next.js, Tailwind</td>
</tr>
</table>

---

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/ritiklakhwani/ritiklakhwani/output/github-snake-dark.svg">
  <img alt="Contribution graph animation" src="https://raw.githubusercontent.com/ritiklakhwani/ritiklakhwani/output/github-snake.svg">
</picture>
