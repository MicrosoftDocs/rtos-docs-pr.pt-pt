---
title: Capítulo 1 - Introdução ao Cliente Azure RTOS NetX Duo LWM2M
description: Este capítulo contém uma introdução ao cliente de protocolo Azure RTOS NetX Duo Lightweight Machine para cliente do protocolo Machine.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 12f13c154668b3cadfae0924e59b55631dc27424
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825957"
---
# <a name="chapter-1--introduction-to-lwm2m-client"></a><span data-ttu-id="c3d66-103">Capítulo 1 Introdução ao Cliente LWM2M</span><span class="sxs-lookup"><span data-stu-id="c3d66-103">Chapter 1  Introduction to LWM2M Client</span></span>

<span data-ttu-id="c3d66-104">O Protocolo de Cliente Azure RTOS NetX Duo LWM2M implementa a parte do cliente da norma de protocolo de máquina leve para máquina.</span><span class="sxs-lookup"><span data-stu-id="c3d66-104">The Azure RTOS NetX Duo LWM2M Client Protocol implements the client part of the Lightweight Machine to Machine protocol standard.</span></span> <span data-ttu-id="c3d66-105">(LWM2M 1.0-20170208A)</span><span class="sxs-lookup"><span data-stu-id="c3d66-105">(LWM2M 1.0-20170208A)</span></span>

## <a name="netx-lwm2m-client-requirements"></a><span data-ttu-id="c3d66-106">Requisitos do cliente NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="c3d66-106">NetX LWM2M Client Requirements</span></span>

<span data-ttu-id="c3d66-107">Para funcionar corretamente, a biblioteca de tempo de execução do cliente LWM2M requer que já tenha sido criada uma instância IP NetX.</span><span class="sxs-lookup"><span data-stu-id="c3d66-107">In order to function properly, the LWM2M Client run-time library requires that a NetX IP instance has already been created.</span></span> <span data-ttu-id="c3d66-108">O pacote de clientes NetX LWM2M não tem mais requisitos.</span><span class="sxs-lookup"><span data-stu-id="c3d66-108">The NetX LWM2M Client package has no further requirements.</span></span>

## <a name="netx-lwm2m-client-rfcs"></a><span data-ttu-id="c3d66-109">RFCs de clientes NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="c3d66-109">NetX LWM2M Client RFCs</span></span>

<span data-ttu-id="c3d66-110">O Cliente LWM2M está em conformidade com o OMA-TS-LightweightM2M-V1 \_ 0-20170208-A e os seguintes RFCs relacionados com o Protocolo de Aplicação Restrita (CoAP).</span><span class="sxs-lookup"><span data-stu-id="c3d66-110">LWM2M Client is compliant with OMA-TS-LightweightM2M-V1\_0-20170208-A and the following RFCs related to the Constrained Application Protocol (CoAP).</span></span>

* <span data-ttu-id="c3d66-111">RFC 7252 O Protocolo de Aplicação Restrita (CoAP)</span><span class="sxs-lookup"><span data-stu-id="c3d66-111">RFC 7252 The Constrained Application Protocol (CoAP)</span></span>

* <span data-ttu-id="c3d66-112">RFC 7641 Recursos de Observação no Protocolo de Aplicação Restrita (CoAP)</span><span class="sxs-lookup"><span data-stu-id="c3d66-112">RFC 7641 Observing Resources in the Constrained Application Protocol (CoAP)</span></span>

* <span data-ttu-id="c3d66-113">Formato de ligação RESTful Ambientes RESTful (CoRE) (CoRE)</span><span class="sxs-lookup"><span data-stu-id="c3d66-113">RFC 6690 Constrained RESTful Environments (CoRE) Link Format</span></span>

<span data-ttu-id="c3d66-114">Para mais informações, consulte [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).</span><span class="sxs-lookup"><span data-stu-id="c3d66-114">For more information, please see [OMA-TS-LightweightM2M-V1\_0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).</span></span>