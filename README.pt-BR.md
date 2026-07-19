<p align="center"><a href="README.md">English</a> · <a href="README.pt-BR.md">Português</a> · <a href="README.es.md">Español</a></p>

<p align="center">
  <img src="assets/hatchpad-logo-512.png" width="120" alt="Hatchpad" />
</p>

<h1 align="center">Hatchpad — hatchpad.fun</h1>

<p align="center">Launchpad de memecoins sem permissão na Robinhood Chain.<br/>Os tokens eclodem numa bonding curve e se graduam para a Uniswap V3 com liquidez travada para sempre.</p>

---

## Como funciona

1. **Criar** — qualquer pessoa lança um token em segundos de graça (você paga
   só o gás da rede). Todo token tem supply fixo de 1.000.000.000 e a mesma
   alocação
   transparente: **80%** vendidos na bonding curve, **10%** reservados para a
   liquidez na Uniswap, **5%** para o criador, **5%** para airdrop comunitário.
2. **Negociar** — compras e vendas acontecem numa bonding curve de produto
   constante. O preço se move deterministicamente com o supply; não há order
   book nem pré-venda. Cada trade paga **1% de taxa**, dividida 50/50 entre o
   criador do token e o protocolo.
3. **Graduar** — quando a curve arrecada **2.5 ETH**, a negociação migra para
   um pool canônico da **Uniswap V3** criado exatamente no preço final da
   curve. A posição de LP é mintada para um cofre que **nunca pode sacar o
   principal nem transferir o NFT** — a liquidez fica travada para sempre. As
   taxas de LP continuam fluindo: 50% para o criador, 50% para o protocolo.
4. **Airdrop** — qualquer criador pode distribuir seu token com um airdrop
   Merkle nativo: cola a lista de endereços, faz o deploy de um distribuidor,
   financia, e os contemplados resgatam on-chain. Tokens não resgatados podem
   ser recolhidos pelo criador após o fim da janela.

## Taxas num relance

| Taxa | Valor | Destino |
| --- | --- | --- |
| Criação de token | grátis (só gás) | — |
| Taxa de trade na curve | 1% por trade | 50% criador / 50% protocolo |
| Taxas de LP pós-graduação | tier 1% da Uniswap V3 | 50% criador / 50% protocolo |

Cada launch congela sua economia na criação — o protocolo não pode alterar
taxas nem alvos de um token existente, nunca.

## O token HATCH

Supply fixo de **1.000.000.000 HATCH**. Sem mint após o deploy.

| Alocação | Parcela |
| --- | --- |
| Comunidade e airdrops | 50% |
| Tesouraria do protocolo | 20% |
| Incentivos de ecossistema | 15% |
| Time (cliff + vesting linear) | 10% |
| Reserva de liquidez | 5% |

### Recompra e queima

**40% das taxas do protocolo** são roteados automaticamente por um splitter
on-chain para um contrato de queima. Executar uma queima exige aprovação do
multisig do protocolo (pelo menos 2 de 3 signatários); o contrato então compra
HATCH na Uniswap V3 e chama `burn()`, reduzindo o supply total
permanentemente. Cada queima emite um evento público on-chain com os valores
exatos.

A governança pode ajustar a parcela de queima dentro dos limites impostos pelo
contrato; ela nunca pode ficar abaixo de 10%. Queimas são gestão discricionária
de supply. Nada nestes documentos é aconselhamento financeiro ou promessa de
valor do token.

## O que o protocolo pode e não pode fazer

**Não pode** (garantido pelos contratos):

- sacar reservas da curve nem o principal de LP travado
- alterar a economia de um token já lançado
- mintar mais supply de qualquer token, incluindo o HATCH
- bloquear vendas, graduação ou resgates válidos — mesmo durante uma pausa de
  emergência

**Pode** (governança, multisig + timelock de 48h, tudo registrado publicamente):

- ajustar defaults limitados para *futuros* launches (taxa de criação ≤ 0.01
  ETH, taxa de trade ≤ 2%, alvo de graduação 0.5–10 ETH)
- pausar *novos* launches durante um incidente (expira sozinho em 72h)
- ocultar metadata maliciosa da descoberta (o contrato continua utilizável)
- aprovar queimas de recompra e retomadas comunitárias de tokens abandonados

## Segurança

- Suite de testes completa: unitários, fuzz, invariantes e testes em fork da
  mainnet contra a Uniswap V3 canônica da Robinhood Chain
- Fuzzing stateful (Echidna), execução simbólica (Halmos) e mutation testing
  (100% dos mutantes mortos na matemática de preço)
- Análise estática (Slither) com triagem pública
- Liquidez travada por contrato, não por promessa

⚠️ O Hatchpad está em **beta** e os contratos ainda não passaram por auditoria
independente de terceiros. Memecoins são altamente especulativas — nunca gaste
o que não pode perder.

## Links

- App: [hatchpad.fun](https://hatchpad.fun)
- X / Twitter: [@hatchpadfun](https://x.com/hatchpadfun)
- Telegram: [t.me/hatchpadfun](https://t.me/hatchpadfun)
- Chain: Robinhood Chain (id 4663) · explorer via Blockscout

Os endereços dos contratos serão publicados aqui após o deploy em mainnet e a
verificação.
