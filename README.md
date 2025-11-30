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

**Requirements:** a modern browser (Chrome, Firefox, Edge, Safari). Optionally, Python 3 (for local HTTP server).

### Option 1: Direct Open

```powershell
# Windows PowerShell
Invoke-Item ".\unit.html"

# macOS/Linux
open unit.html
# or
xdg-open unit.html
```

### Option 2: Local HTTP Server (Recommended)

```powershell
# Windows PowerShell with Python
cd c:\unit1.8  # or your repo path
python -m http.server 8000
# Then open: http://localhost:8000/unit.html
```

### Using the Application

1. **Login / Create Node**
   - Enter username and password (min 6 chars)
   - Click "Acessar Conta / Registrar Novo Nó"
   - You'll receive 100 UNIT genesis reward

2. **L1 Mining (PoW Cooperative)**
   - Adjust difficulty (1-11 zeros) in "Dificuldade da Rede"
   - Toggle "Mineração Automática" or click "Iniciar Mineração Manual"
   - Each mined block rewards 10 UNIT (or 20 if staked ≥50 UNIT)

3. **L2 Mining (Sidechain)**
   - Send funds via `BRIDGE_OUT` to META_GAME_ZONE
   - Toggle "Mineração L2" in L2 section or click "Mineração L2 Manual"
   - L2 blocks confirm bridge transactions

4. **Bridge (Cross-Chain)**
   - **BRIDGE_OUT**: Move UNIT from L1 → L2 (fee: 0, recorded in L1 block)
   - **BRIDGE_IN**: Return UNIT from L2 → L1 (fee: 0, recorded in L1 block)

5. **Staking (PoS)**
   - Enter ≥50 UNIT in "Valor para Stake"
   - Click "Apostar (STAKE)"
   - Increases PoS rewards per block

6. **Snapshot / Backup**
   - **Exportar**: Downloads JSON with full node state (chains, balances, pending txs)
   - **Importar**: Upload JSON to restore state
   - Useful for testing rollback scenarios

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
