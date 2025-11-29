# UNIT Hub-Chains: Instruções para Agentes de IA

## Visão Geral da Arquitetura

**UNIT Hub-Chains** é uma simulação de blockchain híbrida (L1/L2) em HTML/JavaScript com:
- **L1 (UNIT HUB)**: Rede principal com PoW cooperativo e PoS
- **L2 (META_GAME_ZONE)**: Sidechain para valor de jogo
- **Bridge**: Transferência cross-chain de fundos
- **Pool Cooperativo**: Mineração compartilhada entre 5 nós com recompensas divididas

## Fluxo de Dados Principal

1. **Login/Registro** → Cria `node` com `walletAddress` e `id` únicos (hash SHA256)
2. **Transações Pendentes** → Aguardam em `node.pendingTransactions[]`
3. **Mineração** → Encontra hash PoW, cria bloco com transações, distribui recompensas
4. **Atualização de Saldo** → `updateBalance()` processa transações (TRANSFER, STAKE, BRIDGE_OUT, REWARD_*)
5. **Persistência** → `localStorage[STORAGE_KEY]` armazena apenas `id` e `walletAddress` por usuário

## Componentes Críticos

### Estado Global (`node` object)
```javascript
{
  id, walletAddress,           // Identidade do nó
  chains: {UNIT_HUB, META_GAME_ZONE},  // Blockchains por chainId
  pendingTransactions: [],     // Fila de tx para próximo bloco
  balance, sideChainBalance, stake, pendingStake,  // Saldos em float
  autoMiningInterval          // Handle para mining automático
}
```

### Blockchain Storage
- Cada chain é um array de blocos
- Bloco: `{index, timestamp, data, prevHash, nonce, hash, chainId, miner, transactions, poolShare}`
- Transação: `{from, to, amount, fee, timestamp, type, ...}` (type: TRANSFER, STAKE, BRIDGE_OUT, REWARD_POW_SHARE, REWARD_POS_SHARE)

### Recompensas
- PoW Total: 50 UNIT → dividido por POOL_SIZE (5 nós)
- PoS Total: 50 UNIT (se stake ≥ 0) → dividido por POOL_SIZE
- Stake mínimo para PoS: 50 UNIT

## Padrões e Convenções Específicas

### Precisão Numérica
Use `toFixed(10)` para exibir UNIT (suporta até 10 casas decimais), `parseFloat()` para conversão.

### Hash SHA256 Simulado
Função `sha256()` não é SHA256 real, mas é determinística. Usada em:
- Proof-of-Work: hash deve começar com N zeros (dificuldade)
- Endereços: gerados de `sha256(usuario + senha)`.substring(0, 16)

### Mineração PoW Cooperativa
- **Pool Difficulty** (4 zeros fixos): encontra hash rápido no pool
- **Network Difficulty**: até 11 zeros selecionáveis via UI
- Loop busca hash com 4 zeros, depois simula substituição para difficulty alta
- Apenas `poolShare` é recompensa real; transações em bloco são confirmadas

### Bridge (L1 → L2)
- Tx BRIDGE_OUT registrada em L1 (UNIT_HUB)
- Valor movido para `sideChainBalance` (simulado, não armazenado em chain L2)
- Sem tx reversa L2 → L1 implementada

### Atualização de Saldo
Lógica em `updateBalance(block)`:
- Se `tx.to === node.walletAddress` → adiciona ao saldo (depósitos, recompensas)
- Se `tx.from === node.walletAddress` e `type: STAKE` → move para `node.stake`, desconta de `pendingStake`
- Se `type: BRIDGE_OUT` → apenas log (saldo já movido antecipadamente)

## Fluxos de Desenvolvimento Comuns

### Adicionar Nova Transação Type
1. Criar objeto tx com `type: 'NOVO_TIPO'`
2. Adicionar `node.pendingTransactions.push(tx)`
3. Implementar lógica em `updateBalance()` para processar tipo
4. Adicionar UI (button, inputs) para ação
5. Log com cor apropriada (`log(msg, type: 'color-name')`)

### Modificar Dificuldade ou Recompensas
- Dificuldade: input `#difficulty-input` (1-11 zeros), validado no loop PoW
- Recompensas: constantes PoW/PoS (50 UNIT cada) multiplicadas por node.stake
- Alterar POOL_SIZE afeta divisão de recompensas

### Corrigir Estado de Mineração
- Mining automático controlado por `#auto-mine-toggle` checkbox
- `toggleAutoMining()` inicia/para com `setTimeout(autoMineLoop, 1000)`
- Limpar `node.autoMiningInterval` antes de reassign

## Armadilhas Comuns

1. **Valores Numéricos**: `amount` é string de input. Usar `parseFloat()` sempre, validar com `isNaN()`.
2. **Sincronização de Saldo**: `node.balance` é decrementado ao criar tx, não ao confirmar. Evita double-spend na UI, mas não é blockchain real.
3. **Cadeia Não Sincronizada**: Múltiplos nós compartilham `node.chains` globalmente. Alterações afetam todos.
4. **Hash Simulado**: Não é criptograficamente seguro. Apenas para demonstração educacional.
5. **Sem Validação de Hash Prévio**: Ao criar bloco, `prevHash` não é validado contra hash anterior.

## Estrutura de Arquivos Esperada

- `unit.html` - Arquivo único monolítico (HTML + CSS + JS)
- `.github/copilot-instructions.md` - Este arquivo
- Possível expansão: separar em `js/blockchain.js`, `js/ui.js`, `styles/theme.css`

## Checklist para Agentes

- [ ] Validar `isNaN()` antes de usar parseFloat
- [ ] Usar `toFixed(10)` para exibir valores UNIT
- [ ] Chamar `renderUI()` após modificar estado global
- [ ] Adicionar logs com tipo apropriado (error, success, warning, bridge)
- [ ] Testar mineração com dificuldades variadas (3-11 zeros)
- [ ] Persistir estado via `localStorage` se necessário
- [ ] Não quebrar mineração automática (`autoMiningInterval`)
