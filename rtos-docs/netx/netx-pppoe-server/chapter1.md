---
title: Capítulo 1 - Introdução ao Azure RTOS NetX PPPoE Server
description: Este documento centra-se nos detalhes do módulo Azure RTOS NetX PPPoE.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2f79cba35991555f7f8d10e589aa251387ce25c48c3b729da371b548f13321bd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798328"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-server"></a>Capítulo 1 - Introdução ao Azure RTOS NetX PPPoE Server

PPP sobre Ethernet (PPPoE) permite que os anfitriões conectem ao servidor PPP via Ethernet em vez da comunicação tradicional da linha de série baseada em caracteres. Os detalhes técnicos do PPPoE são descritos no RFC 2516: Um Método de Transmissão de PPP sobre Ethernet (PPPoE). Este documento centra-se nos detalhes do módulo Azure RTOS NetX PPPoE.

Para fornecer uma ligação ponto-a-ponto sobre o Ethernet, cada sessão de PPP deve aprender o endereço Ethernet do par remoto, bem como estabelecer um identificador de sessão único.

De acordo com o RFC 2516, o PPPoE é composto por duas etapas: a fase Discovery e o palco PPPoE Session. Quando um anfitrião (cliente) deseja iniciar uma sessão de PPP, tem primeiro de executar a Discovery para encontrar o servidor PPPoE. Este passo também permite que o servidor e o cliente identifiquem o endereço Ethernet MAC e SESSION_ID, que serão utilizados para o resto da sessão de PPP.

Um quadro Ethernet é o seguinte:

![Diagrama mostrando uma moldura Ethernet.](media/netx-pppoe-server-01.png)

A carga útil do Ethernet para PPPoE é a seguinte:

![Diagrama mostrando uma carga de ethernet para PPPoE.](media/netx-pppoe-server-02.png)

## <a name="pppoe-discovery-stage"></a>Fase de Descoberta ppPoe

A fase PPPoE Discovery permite que os clientes selecionem um servidor de todos os servidores disponíveis na rede, efetivamente para criar uma sessão antes da troca de quadros de PPP. No final da fase de descoberta, tanto o cliente como o servidor concordarão com um ID de sessão único, e ambos os lados precisam de saber o endereço MAC do par.

| Mensagem de Descoberta                                  | Código | Direção                                     |
| -------------------------------------------------- | ---- | --------------------------------------------- |
| Iniciação da descoberta ativa ppPoe (PADI)           | 0x09 | Do Cliente à transmissão                      |
| Oferta de descoberta ativa ppPoe (PADO)                | 0x07 | De Servidor a Cliente                         |
| Pedido de descoberta ativa ppPoe (PADR)              | 0x19 | De Cliente a Servidor                         |
| Pppoe Ative Discovery Sessão de confirmação (PADS) | 0x65 | De Servidor a Cliente                         |
| PPPoe Ative Discovery Terminate (PADT)            | 0xa7 | Pode ser iniciado a partir de servidor ou cliente |

Todos os quadros discovery Ethernet têm o campo de ETHER_TYPE definido para o valor 0x8863.

## <a name="pppoe-session-message"></a>Mensagem de sessão pppoe

Após o cliente e o servidor criarem uma sessão, os quadros de PPP podem ser transferidos como mensagens PPPoE Session. Durante uma sessão, o SESSION_ID não deve ser alterado e deve ser o valor atribuído pelo servidor durante a fase Discovery.

Todos os quadros Ethernet da Sessão PPPoE têm o campo ETHER_TYPE definido para o valor 0x8864.