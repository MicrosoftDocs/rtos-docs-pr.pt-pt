---
title: Apêndice A – Códigos de opção Azure RTOS NetX Duo DHCPv6
description: Este capítulo contém uma descrição de todos os códigos de opção NetX Duo DHCPv6
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 36d673c34479ec2d476eeaa094c0dc02714ee010
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826065"
---
# <a name="appendix-a--azure-rtos-netx-duo-dhcpv6-option-codes"></a><span data-ttu-id="0f05a-103">Apêndice A – Códigos de opção Azure RTOS NetX Duo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="0f05a-103">Appendix A – Azure RTOS NetX Duo DHCPv6 option codes</span></span>

| <span data-ttu-id="0f05a-104">Opção</span><span class="sxs-lookup"><span data-stu-id="0f05a-104">Option</span></span>              | <span data-ttu-id="0f05a-105">Código</span><span class="sxs-lookup"><span data-stu-id="0f05a-105">Code</span></span>            | <span data-ttu-id="0f05a-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f05a-106">Description</span></span> |
| ------------------- | ------------------- | --------------- |
| <span data-ttu-id="0f05a-107">Identificador de cliente DUID</span><span class="sxs-lookup"><span data-stu-id="0f05a-107">Client Identifier DUID</span></span> | <span data-ttu-id="0f05a-108">1</span><span class="sxs-lookup"><span data-stu-id="0f05a-108">1</span></span> | <span data-ttu-id="0f05a-109">Identifica exclusivamente um anfitrião do Cliente na rede</span><span class="sxs-lookup"><span data-stu-id="0f05a-109">Uniquely identifies a Client host on the network</span></span> |
| <span data-ttu-id="0f05a-110">Identificador de servidor (DUID)</span><span class="sxs-lookup"><span data-stu-id="0f05a-110">Server Identifier (DUID)</span></span> | <span data-ttu-id="0f05a-111">2</span><span class="sxs-lookup"><span data-stu-id="0f05a-111">2</span></span> | <span data-ttu-id="0f05a-112">Identifica exclusivamente o hospedeiro DHCPv6Server na rede</span><span class="sxs-lookup"><span data-stu-id="0f05a-112">Uniquely identifies the DHCPv6Server host on the network</span></span> |
| <span data-ttu-id="0f05a-113">Associação de Identidade para Endereços Não Temporários (IANA)</span><span class="sxs-lookup"><span data-stu-id="0f05a-113">Identity Association for Non Temporary Addresses (IANA)</span></span> | <span data-ttu-id="0f05a-114">3</span><span class="sxs-lookup"><span data-stu-id="0f05a-114">3</span></span> | <span data-ttu-id="0f05a-115">Parâmetros para uma atribuição de endereço IP não temporário</span><span class="sxs-lookup"><span data-stu-id="0f05a-115">Parameters for a non temporary IP address assignment</span></span> |
| <span data-ttu-id="0f05a-116">Associação de Identidade para Endereços Temporários (IATA)</span><span class="sxs-lookup"><span data-stu-id="0f05a-116">Identity Association for Temporary Addresses (IATA)</span></span> | <span data-ttu-id="0f05a-117">4</span><span class="sxs-lookup"><span data-stu-id="0f05a-117">4</span></span> | <span data-ttu-id="0f05a-118">Parâmetros para uma atribuição temporária de endereço IP</span><span class="sxs-lookup"><span data-stu-id="0f05a-118">Parameters for a temporary IP address assignment</span></span> |
| <span data-ttu-id="0f05a-119">Endereço IA</span><span class="sxs-lookup"><span data-stu-id="0f05a-119">IA Address</span></span> | <span data-ttu-id="0f05a-120">5</span><span class="sxs-lookup"><span data-stu-id="0f05a-120">5</span></span> | <span data-ttu-id="0f05a-121">Endereço IPv6 real e vida útil de endereço IPv6 a atribuir ao Cliente</span><span class="sxs-lookup"><span data-stu-id="0f05a-121">Actual IPv6 address and IPv6 address lifetimes to be assigned to the Client</span></span> |
| <span data-ttu-id="0f05a-122">Pedido de Opção</span><span class="sxs-lookup"><span data-stu-id="0f05a-122">Option Request</span></span> | <span data-ttu-id="0f05a-123">6</span><span class="sxs-lookup"><span data-stu-id="0f05a-123">6</span></span> | <span data-ttu-id="0f05a-124">Uma lista de pedidos de informação para obter informações de rede, como servidor DNS e outros parâmetros de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="0f05a-124">A list of information requests to obtain network information such as DNS server and other network configuration parameters.</span></span> |
| <span data-ttu-id="0f05a-125">Preferência</span><span class="sxs-lookup"><span data-stu-id="0f05a-125">Preference</span></span> | <span data-ttu-id="0f05a-126">7</span><span class="sxs-lookup"><span data-stu-id="0f05a-126">7</span></span> | <span data-ttu-id="0f05a-127">Incluído no servidor Enviar por palavra de forma positiva ao cliente para influenciar a escolha dos servidores do Cliente.</span><span class="sxs-lookup"><span data-stu-id="0f05a-127">Included in server Advertise message to client to influence the Client’s choice of servers.</span></span> <span data-ttu-id="0f05a-128">O Cliente deve escolher um servidor com maior valor de preferência em relação a outros servidores.</span><span class="sxs-lookup"><span data-stu-id="0f05a-128">The Client must choose a server with higher the preference value over other servers.</span></span> <span data-ttu-id="0f05a-129">255 é o valor máximo, enquanto zero indica que o cliente pode escolher qualquer servidor que responda a eles</span><span class="sxs-lookup"><span data-stu-id="0f05a-129">255 is the maximum value, while zero indicates the client can choose any server replying back to them</span></span> |
| <span data-ttu-id="0f05a-130">Tempo decorrido</span><span class="sxs-lookup"><span data-stu-id="0f05a-130">Elapsed Time</span></span> | <span data-ttu-id="0f05a-131">8</span><span class="sxs-lookup"><span data-stu-id="0f05a-131">8</span></span> | <span data-ttu-id="0f05a-132">Contém o tempo (em 0,01 segundos) quando o Cliente inicia a troca DHCPv6 com o servidor.</span><span class="sxs-lookup"><span data-stu-id="0f05a-132">Contains the time (in 0.01 seconds) when the Client initiates the DHCPv6 exchange with the server.</span></span> <span data-ttu-id="0f05a-133">Utilizado por servidores secundários para determinar se o servidor primário responde a tempo ao pedido do Cliente.</span><span class="sxs-lookup"><span data-stu-id="0f05a-133">Used by secondary server(s) to determine if the primary server responds in time to the Client request.</span></span> |
| <span data-ttu-id="0f05a-134">Mensagem de retransmissão</span><span class="sxs-lookup"><span data-stu-id="0f05a-134">Relay Message</span></span> | <span data-ttu-id="0f05a-135">9</span><span class="sxs-lookup"><span data-stu-id="0f05a-135">9</span></span> | <span data-ttu-id="0f05a-136">Contém a mensagem original na mensagem de retransmissão</span><span class="sxs-lookup"><span data-stu-id="0f05a-136">Contains the original message in Relay message</span></span> | 
| <span data-ttu-id="0f05a-137">Autenticação</span><span class="sxs-lookup"><span data-stu-id="0f05a-137">Authentication</span></span> | <span data-ttu-id="0f05a-138">11</span><span class="sxs-lookup"><span data-stu-id="0f05a-138">11</span></span> | <span data-ttu-id="0f05a-139">Contém informações para autenticar a identidade e o conteúdo das mensagens DHCPv6</span><span class="sxs-lookup"><span data-stu-id="0f05a-139">Contains information to authenticate the identity and content of DHCPv6 messages</span></span> |
| <span data-ttu-id="0f05a-140">Servidor Unicast</span><span class="sxs-lookup"><span data-stu-id="0f05a-140">Server Unicast</span></span> | <span data-ttu-id="0f05a-141">12</span><span class="sxs-lookup"><span data-stu-id="0f05a-141">12</span></span> | <span data-ttu-id="0f05a-142">O servidor envia esta opção para informar o Cliente de que o servidor aceitará mensagens unicast diretamente do Cliente em vez de multicast.</span><span class="sxs-lookup"><span data-stu-id="0f05a-142">Server sends this option to let the Client know that the server will accept unicast messages directly from the Client instead of multicast.</span></span> |

<span data-ttu-id="0f05a-143">As opções IATA, Relay Message, Authentication e Server Unicast não são suportadas nesta versão do NetX Duo DHCPv6 Server.</span><span class="sxs-lookup"><span data-stu-id="0f05a-143">IATA, Relay Message, Authentication and Server Unicast options are not supported in this release of NetX Duo DHCPv6 Server.</span></span> <span data-ttu-id="0f05a-144">O atual código de opção do protocolo DHCPv6 10 é deixado indefinido no RFC 3315.</span><span class="sxs-lookup"><span data-stu-id="0f05a-144">The current DHCPv6 protocol option code 10 is left undefined in RFC 3315.</span></span>