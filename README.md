# PAINEL PLC IRRIGAÇÃO

Projeto de automação para irrigação por gotejamento em plantação de café,
desenvolvido como trabalho de conclusão do curso de Bacharelado em Engenharia
Elétrica.

![TIA Portal](https://img.shields.io/badge/TIA%20Portal-V16-blue)
![CLP](https://img.shields.io/badge/CLP-S7--1200%20CPU%201214C-green)
![Status](https://img.shields.io/badge/status-defendido-brightgreen)

---

## Download do projeto

O projeto completo (PLC + IHM) está disponível na página de Releases:

**https://github.com/PauloHenriqueEng/PLC_IHM_IRRIGACAO/releases/tag/V1.0**

| Item | Valor |
|---|---|
| Versão | V1.0 — versão da defesa |
| Arquivo | `PAINEL_PLC_IRRIGACAO_20261105.zap16` |
| Tamanho | 3,02 MB |
| Formato | Archive do TIA Portal (`.zap16`) |
| Software | TIA Portal V16 ou superior |

Para reabrir: no TIA Portal, acesse **Project → Retrieve**, selecione o arquivo
`.zap16` e escolha a pasta de destino. O projeto é restaurado com os blocos do
PLC, as telas da IHM, as tags e os alarmes já vinculados.

---

## Hardware

| Componente | Modelo / Especificação |
|---|---|
| CLP | SIMATIC S7-1200 — CPU 1214C DC/DC/DC |
| IHM | Painel Comfort (WinCC) |
| Software de engenharia | TIA Portal V16 |
| Comunicação | Ethernet PROFINET entre CLP e IHM |
| Acionamento | Válvulas solenoides por setor e motobombas (principal e de produtos) |

---

## Estrutura do programa

O programa está organizado em pastas numeradas por função:

| Pasta | Bloco | Conteúdo |
|---|---|---|
| 010 — LÓGICAS GERAIS | FC10, DB10, DB11, DB12, DB17, DB18 | Lógica geral do sistema e blocos de dados de apoio |
| 040 — I/Os | 050, FC60, DB60, 070 | Entradas digitais, saídas digitais e entradas analógicas |
| 080 — VÁLVULA SETOR 01 | FC80, DB80 | Controle e intertravamento da válvula do setor 01 |
| 090 — VÁLVULA SETOR 02 | FC90, DB90 | Controle e intertravamento da válvula do setor 02 |
| 100 — BOMBA DE IRRIGAÇÃO | FC100, DB100 | Acionamento da motobomba principal |
| 110 — BOMBA DE PRODUTOS | FC110, DB110 | Acionamento da motobomba de produtos |
| 120 — SINALIZAÇÕES | FC120, DB120 | Sinalizações, indicações de estado e alarmes |
| 9000 — BLOCOS DE FUNÇÃO | FC9000, FB9002, FB9003 | Blocos de função reutilizáveis |

A nomenclatura segue o padrão `0xx` para as pastas de função, `FCxx` para
funções e `DBxx` para os blocos de dados associados.

---

## Lógica de operação

O sistema opera em dois modos, selecionáveis na IHM: **Automático** e **Manual**,
com botão de **Reset** para retorno ao estado inicial.

### Modo automático

1. O operador programa na IHM o dia da semana e o horário de início da irrigação.
2. O CLP compara continuamente o dia e o horário atuais com os valores programados.
3. Quando a comparação é verdadeira, o sistema energiza as válvulas dos setores habilitados.
4. Em seguida, aciona a motobomba principal.
5. Por último, aciona a motobomba de produtos.
6. Ao atingir o horário de término programado, válvulas e bombas são desenergizadas.

A ordem de acionamento (válvulas antes das bombas) tem função de segurança: o
caminho hidráulico é aberto antes da pressurização. Na parada, a sequência
inversa evita golpe de aríete na linha.

### Modo manual

Permite comandar individualmente cada válvula e cada bomba pela IHM, para
manutenção e testes de comissionamento, mantidos os intertravamentos de segurança.

---

## IHM

| Item | Configuração |
|---|---|
| Telas | Menu principal, Operação, Programações, Telemetria, Alarmes |
| Comandos | Botões Automático, Manual e Reset |
| Relógio | Data e hora exibidas no cabeçalho da tela |
| Formato de data | `dd/mm/aaaa` configurado no evento de sistema ID 330018 (HMI Alarms → System events) |

O formato de data e hora do runtime é definido pela string de formatação do
evento de sistema ID 330018, e não pelo locale do dispositivo. Essa escolha
mantém a configuração dentro do projeto, garantindo que ela viaje junto com a
transferência e sobreviva a uma restauração de fábrica do painel.

---

## Documentação

| Documento | Onde está |
|---|---|
| Monografia do TCC | Repositório institucional da universidade |
| Lógica do programa (LAD) | Apêndice do TCC, gerado por impressão do TIA Portal |
| Projeto completo | Release V1.0 deste repositório |

---

## Autor

**Paulo Henrique**
Bacharelado em Engenharia Elétrica
Trabalho de Conclusão de Curso — 2026

---

## Licença

Projeto de caráter acadêmico, disponibilizado para consulta e referência.
As bibliotecas e blocos de sistema utilizados pertencem à Siemens AG.
