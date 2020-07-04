# Âmbito

A integração entre os contadores inteligentes com sistemas de domótica permite potenciar automações, controlo e análises com base na informação disponível das grandezas elétricas. Nomeadamente, tensão, intensidade de corrente, potência ativa, fator de potência, frequência, estado do disjuntor controlador de potência, *et al*.

A EDP Distribuição S.A. surge neste contexto enquanto Operadora da Rede de Distribuição de baixa tensão. Independentemente do comercializador de energia elétrica com quem tem contrato de fornecimento e de estar em mercado regulado ou liberalizado.


# Objetivo

Pretende-se partilhar o conceito de integração entre dispositivos EDP Box com um HUB de domótica a executar [Home Assistant Core](https://www.home-assistant.io/).

Esta integração é possível graças à porta de comunicação HAN que está disponível internamente nos contadores inteligentes. É também proposto neste repositório um procedimento para requisitar formalmente o acesso a esta porta.

São propostas duas alternativas distintas possíveis para integração:

1. Integração indireta com Home Assistant, usando um microcontrolador ESP8266 com firmware Tasmota, através de MQTT com Home Assistant Core.
2. Integração direta com Home Assistant Core, com o seu componente nativo para protocolo MODBUS.

**`A porta de comunicação HAN está no interior das EDP Box. A manipulação ou acesso não autorizado a esta porta é da total responsabilidade do próprio.`**


# Conteúdos

1. [A EDP Box e a sua porta HAN](EDP%20Box/README.md)
   1. [Pedido de acesso](EDP%20Box/README.md#pedido-de-acesso)
   2. [Interface físico](EDP%20Box/README.md#interface-físico)
   3. [Impedância de linha](EDP%20Box/README.md#impedância-de-linha)
   4. [Comunicação](EDP%20Box/COMUNICACAO.md)
2. [Tasmota e script de configuração para MODBUS - Para método indireto](Tasmota/README.md)
   1. [Descarga e instalação do firmware no ESP8266](Tasmota/README.md)
   2. [Configuração do script para Smart Meter Interface (SMI)](Tasmota/CONFIGURAÇÃO-SCRIPT-SMI.md)
   3. [Ligação física entre o contador inteligente, o ESP8266 e o hub com Home Assistant Core](Tasmota/LIGACOES_INDIRETO.md)
3. [Home Assitant Core e a sua configuração - Para método direto e indireto](Home%20Assistant/README.md)
   1. [Ligação física entre o contador inteligente e o hub com Home Assistant Core](Home%20Assistant/LIGACOES_DIRETO.md)
   2. [Ficheiro de configuração](Home%20Assistant/README.md#configuração-do-home-assistant-core) 
   3. [Personalizar as entidades geradas - método direto](Home%20Assistant/README.md#personalizar-as-entidades-geradas) 
   4. [Aplicação das configurações](Home%20Assistant/README.md#aplicação-das-configurações) 

# Requisitos mínimos

## Transversais
- Contador inteligente com porta HAN ativada, suportando o protocolo de tramas MODBUS.
- Acesso exterior à porta HAN, previamente instalado pela EDP Distribuição S.A.;
- Raspberry Pi 3 B+ ou superior (alternativamente, Home Assistant Core em PC, máquina física ou virtualizada em Proxmox);
- Home Assistant Core instalado (versão inicial de prova de conceito: 0.106.6. Recomendada a versão 0.109.7 ou superior.);
- Acessórios de ligação variados.
## Exclusivamente para o 1º método (indireto)
- Conversor TTL vs RS-485 (por exemplo, "TTL to RS485 For Arduino")
- Wemos D1 Mini
- Resistência de 120 Ohm
## Exclusivamente para o 2º método (direto)
- Conversor USB - TTL vs RS-485 (por exemplo, "Waveshare Industrial USB to RS485")
- Cabo extensor USB "A macho" - "A fêmea" (recomendado)


# Fontes

[EDP Box - HAN protocol specification (DEF-C44-509/N)](https://www.edpdistribuicao.pt/sites/edd/files/normative_docs/DEF-C44-509.pdf)

[Descrição dos requisitos e respetiva aplicabilidade em função do tipo de módulo HAN](https://www.edpdistribuicao.pt/sites/edd/files/2019-06/Requisitos%20dos%20m%C3%B3dulos%20HAN_2019.05.31.pdf?fbclid=IwAR1txmKfYIbwCae6eR5njlblvvBMB1xiLvp5ynURi9qAW4rsOut3WFfJNQM)

[Contadores de energia elétrica - Especificação funcional (DEF-C44-506/N)](https://www.edpdistribuicao.pt/sites/edd/files/normative_docs/DEF-C44-506N.pdf)

[Novos Equipamentos](https://www.edpdistribuicao.pt/sites/edd/files/2019-04/Novos_Equipamentos.pdf?fbclid=IwAR3zNpBId8BMqrSVaPoekoUvqt-xxstLua4iqZN2qz-8Xf2hvRQqtU8g2xo)

# Nota

Todas as marcas registadas, nomes de produtos ou de marcas, referidas neste documento, são propriedade registada do respectivo detentor.

# A fazeres

Método direto:
- [ ] Potência ativa
- [ ] Totalizadores de energia
- [ ] Religação do DCP

Método indireto:
- [ ] Tarifa
- [ ] Estado do DCP
- [ ] Totalizadores de energia
- [ ] Religação do DCP
