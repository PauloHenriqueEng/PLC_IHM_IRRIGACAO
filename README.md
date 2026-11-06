# PAINEL PLC IRRIGAÇÃO

Projeto de automação para irrigação por gotejamento em plantação de café.

## Hardware
- CLP: SIMATIC S7-1200, CPU 1214C DC/DC/DC
- IHM: painel Comfort (WinCC)

## Software
- TIA Portal V16
- Versão do archive: v1.0 (03/11/2026)

## Conteúdo
- `*.zap16` — projeto completo (PLC + IHM), reabrir em TIA Portal V16 ou superior

## Estrutura do programa
- 010 — Lógicas gerais
- 040 — I/Os
- 080 / 090 — Válvulas setor 01 e 02
- 100 — Bomba de irrigação
- 110 — Bomba de produtos
- 120 — Sinalizações
- 9000 — Blocos de função
