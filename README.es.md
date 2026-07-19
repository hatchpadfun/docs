<p align="center"><a href="README.md">English</a> · <a href="README.pt-BR.md">Português</a> · <a href="README.es.md">Español</a></p>

<p align="center">
  <img src="assets/hatchpad-logo-512.png" width="120" alt="Hatchpad" />
</p>

<h1 align="center">Hatchpad — hatchpad.fun</h1>

<p align="center">Launchpad de memecoins sin permisos en Robinhood Chain.<br/>Los tokens eclosionan en una bonding curve y se gradúan a Uniswap V3 con la liquidez bloqueada para siempre.</p>

---

## Cómo funciona

1. **Crear** — cualquiera puede lanzar un token en segundos por una tarifa de
   0.002 ETH. Todo token tiene un supply fijo de 1.000.000.000 y la misma
   asignación transparente: **80%** vendido en la bonding curve, **10%**
   reservado para la liquidez en Uniswap, **5%** para el creador, **5%** para
   un airdrop comunitario.
2. **Operar** — las compras y ventas ocurren en una bonding curve de producto
   constante. El precio se mueve determinísticamente con el supply; no hay
   order books ni preventas. Cada trade paga una **tarifa del 1%**, dividida
   50/50 entre el creador del token y el protocolo.
3. **Graduarse** — cuando la curve recauda **2.5 ETH**, la negociación migra a
   un pool canónico de **Uniswap V3** creado exactamente al precio final de la
   curve. La posición de LP se mintea a una bóveda que **nunca puede retirar
   el principal ni transferir el NFT** — la liquidez queda bloqueada para
   siempre. Las tarifas de LP siguen fluyendo: 50% al creador, 50% al
   protocolo.
4. **Airdrop** — cualquier creador puede distribuir su token con un airdrop
   Merkle integrado: pega la lista de direcciones, despliega un distribuidor,
   lo financia, y los destinatarios reclaman on-chain. Los tokens no
   reclamados pueden ser recuperados por el creador tras el cierre de la
   ventana.

## Tarifas de un vistazo

| Tarifa | Monto | Destino |
| --- | --- | --- |
| Creación de token | 0.002 ETH | protocolo |
| Tarifa de trade en la curve | 1% por trade | 50% creador / 50% protocolo |
| Tarifas de LP post-graduación | tier 1% de Uniswap V3 | 50% creador / 50% protocolo |

Cada lanzamiento congela su economía en la creación — el protocolo no puede
cambiar tarifas ni objetivos de un token existente, nunca.

## El token HATCH

Supply fijo de **1.000.000.000 HATCH**. Sin minteo después del despliegue.

| Asignación | Parte |
| --- | --- |
| Comunidad y airdrops | 50% |
| Tesorería del protocolo | 20% |
| Incentivos del ecosistema | 15% |
| Equipo (cliff + vesting lineal) | 10% |
| Reserva de liquidez | 5% |

### Recompra y quema

**El 40% de las tarifas del protocolo** se enruta automáticamente mediante un
splitter on-chain a un contrato de quema. Ejecutar una quema requiere la
aprobación del multisig del protocolo (al menos 2 de 3 firmantes); el contrato
entonces compra HATCH en Uniswap V3 y llama a `burn()`, reduciendo el supply
total permanentemente. Cada quema emite un evento público on-chain con los
montos exactos.

La gobernanza puede ajustar la parte de quema dentro de los límites impuestos
por el contrato; nunca puede quedar por debajo del 10%. Las quemas son gestión
discrecional del supply. Nada en estos documentos es asesoramiento financiero
ni una promesa de valor del token.

## Lo que el protocolo puede y no puede hacer

**No puede** (garantizado por los contratos):

- retirar reservas de la curve ni el principal de LP bloqueado
- cambiar la economía de un token ya lanzado
- mintear más supply de ningún token, incluido HATCH
- bloquear ventas, graduaciones o reclamos válidos — incluso durante una pausa
  de emergencia

**Puede** (gobernanza, multisig + timelock de 48h, todo registrado públicamente):

- ajustar defaults acotados para *futuros* lanzamientos (tarifa de creación ≤
  0.01 ETH, tarifa de trade ≤ 2%, objetivo de graduación 0.5–10 ETH)
- pausar *nuevos* lanzamientos durante un incidente (expira solo en 72h)
- ocultar metadata maliciosa del descubrimiento (el contrato sigue utilizable)
- aprobar quemas de recompra y tomas comunitarias de tokens abandonados

## Seguridad

- Suite de pruebas completa: unitarias, fuzz, invariantes y pruebas en fork de
  mainnet contra la Uniswap V3 canónica de Robinhood Chain
- Fuzzing stateful (Echidna), ejecución simbólica (Halmos) y mutation testing
  (100% de mutantes eliminados en la matemática de precios)
- Análisis estático (Slither) con triaje público
- Liquidez bloqueada por contrato, no por promesa

⚠️ Hatchpad está en **beta** y los contratos aún no han completado una
auditoría independiente de terceros. Las memecoins son altamente especulativas
— nunca gastes lo que no puedas permitirte perder.

## Enlaces

- App: [hatchpad.fun](https://hatchpad.fun)
- X / Twitter: [@hatchpadfun](https://x.com/hatchpadfun)
- Telegram: [t.me/hatchpadfun](https://t.me/hatchpadfun)
- Chain: Robinhood Chain (id 4663) · explorador vía Blockscout

Las direcciones de los contratos se publicarán aquí después del despliegue en
mainnet y su verificación.
