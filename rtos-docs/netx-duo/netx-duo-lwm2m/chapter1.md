---
title: Capítulo 1 - Introdução ao Cliente Azure RTOS NetX Duo LWM2M
description: Este capítulo contém uma introdução ao cliente de protocolo Azure RTOS NetX Duo Lightweight Machine para cliente do protocolo Machine.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a2722daac76632e492d0f9345103c45da9ba1b321e91c9c04e04c76463984c3a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783480"
---
# <a name="chapter-1--introduction-to-lwm2m-client"></a>Capítulo 1 Introdução ao Cliente LWM2M

O Protocolo de Cliente Azure RTOS NetX Duo LWM2M implementa a parte do cliente da norma de protocolo de máquina leve para máquina. (LWM2M 1.0-20170208A)

## <a name="netx-lwm2m-client-requirements"></a>Requisitos do cliente NetX LWM2M

Para funcionar corretamente, a biblioteca de tempo de execução do cliente LWM2M requer que já tenha sido criada uma instância IP NetX. O pacote de clientes NetX LWM2M não tem mais requisitos.

## <a name="netx-lwm2m-client-rfcs"></a>RFCs de clientes NetX LWM2M

O Cliente LWM2M está em conformidade com o OMA-TS-LightweightM2M-V1 \_ 0-20170208-A e os seguintes RFCs relacionados com o Protocolo de Aplicação Restrita (CoAP).

* RFC 7252 O Protocolo de Aplicação Restrita (CoAP)

* RFC 7641 Recursos de Observação no Protocolo de Aplicação Restrita (CoAP)

* Formato de ligação RESTful Ambientes RESTful (CoRE) (CoRE)

Para mais informações, consulte [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).