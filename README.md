# UNIT Hub-Chains

Simulação de Blockchain Híbrida (L1/L2) com Pool Cooperativo e Bridge Cross-Chain.

## Descrição (Português)

Simulação educacional em HTML/JavaScript que demonstra:
- Rede principal (L1) `UNIT_HUB` com Proof-of-Work cooperativo (pool) e Proof-of-Stake (PoS).
- Sidechain (L2) `META_GAME_ZONE` usada como mundo de jogo.
- Bridge bidirecional: `BRIDGE_OUT` (L1 → L2) e `BRIDGE_IN` (L2 → L1).

Use este projeto para experimentar conceitos de mineração cooperativa, staking, e transferência cross-chain em um ambiente didático.

## Description (English)

Educational simulation in HTML/JavaScript demonstrating:
- Main chain (L1) `UNIT_HUB` with cooperative Proof-of-Work pool and Proof-of-Stake.
- Sidechain (L2) `META_GAME_ZONE` used as a game world.
- Bidirectional bridge: `BRIDGE_OUT` (L1 → L2) and `BRIDGE_IN` (L2 → L1).

This project is intended for learning and demonstration purposes only.

## Quick Start

Requirements: a modern browser. Optionally, Python (for a local static server).

1. Open directly in your browser (double-click):

```
Open the file `unit.html` in your browser (e.g. double-click or `Invoke-Item .\unit.html` in PowerShell).
```

2. Recommended (serve via local HTTP server):

PowerShell / Windows (Python required):

```powershell
# from repository root
python -m http.server 8000
Start-Process "http://localhost:8000/unit.html"
```

3. Interaja com the UI:
- Crie/acesse um nó (usuário + senha)
- Use `BRIDGE_OUT` para mover fundos L1 → L2
- Use `BRIDGE_IN` para retornar fundos L2 → L1
- Ajuste `#difficulty-input` e teste mineração manual/automática

## Arquivos importantes

- `unit.html` — Aplicação monolítica (HTML + CSS + JS).
- `.github/copilot-instructions.md` — Instruções específicas para agentes de IA.

## Convenções do projeto

- Valores UNIT exibidos com `toFixed(10)`.
- `STORAGE_KEY = 'UNIT_NODE_DB_V5'` usado para persistência mínima em `localStorage`.
- Use `parseFloat()` e valide com `isNaN()` antes de operar valores financeiros.

## Licença

Projeto de exemplo / educativo — sem garantia. Sinta-se à vontade para adaptar.

## Topics

blockchain, simulation, hybrid-blockchain, pow-pos, cross-chain-bridge, html5, javascript, educational
# unit1.8
Simulação de Blockchain Híbrida (L1/L2) com Pool Cooperativo e Bridge Cross-Chain. Sistema educacional em HTML/JavaScript com Proof-of-Work, Proof-of-Stake e transferência bidirecional entre cadeias.
