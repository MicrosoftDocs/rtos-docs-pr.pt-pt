---
title: Capítulo 1 - Introdução ao Cliente DHCPv6 da Azure RTOS NetX Duo DHCPv6
description: Nas redes IPv6, o DHCPv6 substitui o DHCP por uma atribuição dinâmica global de endereços IP a partir de um Servidor DHCPv6, e oferece a maioria das mesmas funcionalidades, bem como muitas melhorias.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3bf3b52c53bb26e2c9c2c736ae35817eb967f609
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826096"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcpv6-client"></a><span data-ttu-id="706cc-103">Capítulo 1 - Introdução ao Cliente DHCPv6 da Azure RTOS NetX Duo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-103">Chapter 1 - Introduction to Azure RTOS NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="706cc-104">Nas redes IPv6, o DHCPv6 substitui o DHCP por uma atribuição dinâmica global de endereços IP a partir de um Servidor DHCPv6, e oferece a maioria das mesmas funcionalidades, bem como muitas melhorias.</span><span class="sxs-lookup"><span data-stu-id="706cc-104">In IPv6 networks, DHCPv6 replaces DHCP for dynamic global IP address assignment from a DHCPv6 Server, and offers most of the same features as well as many enhancements.</span></span> <span data-ttu-id="706cc-105">Este documento explicará em detalhe como é utilizada a API do Cliente Azure RTOS NetX Duo DHCPv6 para obter endereços IPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-105">This document will explain in detail how the Azure RTOS NetX Duo DHCPv6 Client API is used to obtain IPv6 addresses.</span></span>

## <a name="dhcpv6-communication"></a><span data-ttu-id="706cc-106">Comunicação DHCPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-106">DHCPv6 Communication</span></span>

<span data-ttu-id="706cc-107">O protocolo DHCPv6 utiliza uDP.</span><span class="sxs-lookup"><span data-stu-id="706cc-107">The DHCPv6 protocol uses UDP.</span></span> <span data-ttu-id="706cc-108">O Cliente utiliza a porta 546 e o Servidor utiliza a porta 547 para trocar mensagens DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-108">The Client uses port 546 and the Server uses port 547 to exchange DHCPv6 messages.</span></span> <span data-ttu-id="706cc-109">O Cliente utiliza o seu endereço local de ligação para um endereço de origem para iniciar os pedidos DHCPv6 para os servidores(s) DHCPv6 disponíveis.</span><span class="sxs-lookup"><span data-stu-id="706cc-109">The Client uses its link local address for a source address to initiate the DHCPv6 requests to the DHCPv6 server(s) available.</span></span> <span data-ttu-id="706cc-110">Quando o Cliente envia mensagens destinadas a todos os servidores DHCPv6 da rede, utiliza o endereço multicast *All_DHCP_Relay_Agents_and_Servers* *FF02::01:02*.</span><span class="sxs-lookup"><span data-stu-id="706cc-110">When the Client sends messages intended for all DHCPv6 servers on the network it uses the *All_DHCP_Relay_Agents_and_Servers* multicast address *FF02::01:02*.</span></span> <span data-ttu-id="706cc-111">Este é um endereço multicast reservado e com âmbito de ligação.</span><span class="sxs-lookup"><span data-stu-id="706cc-111">This is a reserved, link-scoped multicast address.</span></span>

## <a name="dhcpv6-process-of-requesting-an-ipv6-address"></a><span data-ttu-id="706cc-112">DHCPv6 Processo de Solicitação de Um Endereço IPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-112">DHCPv6 Process of Requesting an IPv6 Address</span></span>

<span data-ttu-id="706cc-113">Para iniciar o processo de solicitação de uma atribuição global de endereços IPv6, um Cliente envia primeiro uma mensagem SOLICIT utilizando o serviço *nx_dhcpv6_send_solicit:*</span><span class="sxs-lookup"><span data-stu-id="706cc-113">To begin the process of requesting a global IPv6 address assignment, a Client first sends a SOLICIT message using the *nx_dhcpv6_send_solicit* service:</span></span>

<span data-ttu-id="706cc-114">**UINT nx_dhcpv6_request_solicit(NX_DHCPV6 \* dhcpv6_ptr)**</span><span class="sxs-lookup"><span data-stu-id="706cc-114">**UINT nx_dhcpv6_request_solicit(NX_DHCPV6 \*dhcpv6_ptr)**</span></span>

<span data-ttu-id="706cc-115">Esta mensagem é enviada para todos os servidores utilizando o endereço *All_DHCP_Relay_Agents_and_Servers.*</span><span class="sxs-lookup"><span data-stu-id="706cc-115">This message is sent to all servers using the *All_DHCP_Relay_Agents_and_Servers* address.</span></span> <span data-ttu-id="706cc-116">No pedido SOLICIT, o Cliente poderá solicitar a atribuição de endereços IPv6 específicos(es) como uma dica para o Servidor.</span><span class="sxs-lookup"><span data-stu-id="706cc-116">In the SOLICIT request, the Client may request the assignment of specific IPv6 address(es) as a hint to the Server.</span></span> <span data-ttu-id="706cc-117">Também pode solicitar outras informações de configuração de rede a partir do Servidor, como servidor DNS, servidor NTP e outras opções no Pedido de Opção na mensagem SOLICIT.</span><span class="sxs-lookup"><span data-stu-id="706cc-117">It can also request other network configuration information from the Server such as DNS server, NTP server and other options in the Option Request in the SOLICIT message.</span></span>

<span data-ttu-id="706cc-118">Um Servidor DHCPv6 que pode servir um pedido de Cliente responde com uma mensagem DE ANÚNCIO contendo o endereço IPv6(es) que pode atribuir ao Cliente, o tempo de locação de endereço iPv6 e qualquer informação adicional solicitada pelo Cliente.</span><span class="sxs-lookup"><span data-stu-id="706cc-118">A DHCPv6 Server that can service a Client request responds with an ADVERTISE message containing the IPv6 address(es) it can assign to the Client, the IPv6 address lease time and any additional information requested by the Client.</span></span> <span data-ttu-id="706cc-119">O protocolo do Cliente DHCPv6 exige que o Cliente aguarde um período de tempo para receber mensagens DE ANÚNCIO DE TODOS os Servidores DHCPv6 da rede.</span><span class="sxs-lookup"><span data-stu-id="706cc-119">The DHCPv6 Client protocol requires the Client to wait for a period of time to receive ADVERTISE messages from all DHCPv6 Servers on the network.</span></span> <span data-ttu-id="706cc-120">Ele pré-processa cada mensagem ADVERTISE para ser uma mensagem válida, e digitaliza os dados de opção para vários parâmetros DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-120">It pre-processes each ADVERTISE message to be a valid message, and scans the option data for various DHCPv6 parameters.</span></span> <span data-ttu-id="706cc-121">Verifica também o valor preferencial na Opção Preferência, se for fornecido pelo Servidor.</span><span class="sxs-lookup"><span data-stu-id="706cc-121">It also checks the Preference value in the Preference Option, if supplied by the Server.</span></span> <span data-ttu-id="706cc-122">Se mais de uma mensagem DE ANÚNCIO for recebida, o Cliente NetX DHCPv6 escolhe o Servidor com o valor de preferência mais elevado recebido no final do período de espera.</span><span class="sxs-lookup"><span data-stu-id="706cc-122">If more than one ADVERTISE message is received, the NetX DHCPv6 Client chooses the Server with the highest preference value received by the end of the wait period.</span></span>

<span data-ttu-id="706cc-123">A exceção é se o Cliente receber uma mensagem DE ANÚNCIO COM um valor preferencial de 255.</span><span class="sxs-lookup"><span data-stu-id="706cc-123">The exception is if the Client receives an ADVERTISE message with a preference value of 255.</span></span> <span data-ttu-id="706cc-124">Aceita essa mensagem imediatamente e descarta todas as mensagens de PUBLICIDADE subsequentes.</span><span class="sxs-lookup"><span data-stu-id="706cc-124">It accepts that message immediately and discards all subsequent ADVERTISE messages.</span></span>

<span data-ttu-id="706cc-125">O período de espera é definido como o período de retransmissão que o Cliente DHCPv6 aguarda antes de enviar outra mensagem SOLICIT se não tiver recebido uma resposta de qualquer Servidor.</span><span class="sxs-lookup"><span data-stu-id="706cc-125">The wait period is defined as the retransmission period that the DHCPv6 Client waits before sending another SOLICIT message if it has not received a response from any Server.</span></span> <span data-ttu-id="706cc-126">O tempo limite inicial de retransmissão no estado SOLICIT é definido pelo protocolo DHCPv6 descrito no RFC 3315 para ser de 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="706cc-126">The initial retransmission timeout in the SOLICIT state is defined by to the DHCPv6 protocol described in RFC 3315 to be 1 second.</span></span> <span data-ttu-id="706cc-127">Os intervalos de retransmissão subsequentes, se o Cliente DHCPv6 não receber uma resposta válida do Servidor, são duplicados até um máximo de 120 segundos.</span><span class="sxs-lookup"><span data-stu-id="706cc-127">Subsequent retransmission intervals, if the DHCPv6 Client fails to receive a valid Server response, are doubled up to a maximum of 120 seconds.</span></span>

<span data-ttu-id="706cc-128">Tendo escolhido o Servidor, o Cliente extrai dados da mensagem "ANÚNCIO" e envia uma mensagem REQUEST de volta ao Servidor para aceitar as informações de endereço e os tempos de locação atribuídos.</span><span class="sxs-lookup"><span data-stu-id="706cc-128">Having chosen the Server, the Client extracts data from the ADVERTISE message and sends a REQUEST message back to the Server to accept the assigned address information and lease times.</span></span> <span data-ttu-id="706cc-129">O Servidor responde com uma mensagem RESPOSTA para confirmar que o endereço (es) do Cliente IPv6 está registado no Servidor conforme atribuído ao Cliente.</span><span class="sxs-lookup"><span data-stu-id="706cc-129">The Server responds with a REPLY message to confirm the Client IPv6 address(es) are registered with the Server as assigned to the Client.</span></span>

<span data-ttu-id="706cc-130">O Cliente DHCPv6 regista o endereço IPv6 atribuído(es) com a instância IP (por exemplo, NetX Duo).</span><span class="sxs-lookup"><span data-stu-id="706cc-130">The DHCPv6 Client registers the assigned IPv6 address(es) with the IP instance (e.g NetX Duo).</span></span> <span data-ttu-id="706cc-131">Se configurado para o protocolo de Deteção de Endereços Duplicado (DAD) (ativado por padrão), o NetX Duo enviará automaticamente mensagens Neighbor Solicit para verificar se os endereços atribuídos são únicos na rede.</span><span class="sxs-lookup"><span data-stu-id="706cc-131">If configured for the Duplicate Address Detection (DAD) protocol (enabled by default), NetX Duo will automatically send Neighbor Solicit messages to verify the assigned address(es) are unique on the network.</span></span> <span data-ttu-id="706cc-132">Em caso afirmativo, notifica o Cliente DHCPv6 quando cada endereço atribuído foi promovido de PROVISÓRIO a VALID.</span><span class="sxs-lookup"><span data-stu-id="706cc-132">If so, it notifies the DHCPv6 Client when the each assigned address has been promoted from TENTATIVE to VALID.</span></span> <span data-ttu-id="706cc-133">O Cliente DHCPv6 é promovido ao estado BOUND e o dispositivo pode usar esse endereço IPv6 para enviar e transmitir mensagens.</span><span class="sxs-lookup"><span data-stu-id="706cc-133">The DHCPv6 Client is promoted to the BOUND state and the device may use that IPv6 address to send and transmit messages.</span></span> <span data-ttu-id="706cc-134">Se o protocolo DAD falhar, a NetX Duo notifica o Cliente DHCPv6 e o Cliente DHCPv6 envia uma mensagem DECLINante para o endereço IPv6(es) atribuído de volta ao Servidor e repõe o estado do Cliente DHCPv6 para o estado INIT.</span><span class="sxs-lookup"><span data-stu-id="706cc-134">If the DAD protocol fails, NetX Duo notifies the DHCPv6 Client and the DHCPv6 Client sends a DECLINE message for the IPv6 address(es) assigned back to the Server and resets the DHCPv6 Client state to the INIT state.</span></span>

### <a name="notification-of-successful-address-assignment-and-validation"></a><span data-ttu-id="706cc-135">Notificação de atribuição e validação de endereços bem sucedidos</span><span class="sxs-lookup"><span data-stu-id="706cc-135">Notification of Successful Address Assignment and Validation</span></span>

<span data-ttu-id="706cc-136">A aplicação pode determinar o resultado da solicitação de endereço do Cliente DHCPv6 a partir das alterações do estado se o Cliente DHCPv6 estiver configurado com a chamada de alteração do Estado no serviço *nx_dhcpv6_client_create.*</span><span class="sxs-lookup"><span data-stu-id="706cc-136">The application can determine the result of the DHCPv6 Client address solicitation from the state changes if the DHCPv6 Client is configured with the state change callback in the *nx_dhcpv6_client_create* service.</span></span> <span data-ttu-id="706cc-137">Se não receber resposta do Servidor, a alteração de estado observada é de SOLICIT para INIT.</span><span class="sxs-lookup"><span data-stu-id="706cc-137">If it receives no response from the Server the state change observed is from SOLICIT to INIT.</span></span> <span data-ttu-id="706cc-138">Se recebeu uma resposta do Servidor mas o Servidor não conseguir atribuir o endereço, a aplicação será notificada pela chamada de erro do servidor do cliente DHCPv6 se configurada com uma (também em *nx_dhcpv6_client_create).*</span><span class="sxs-lookup"><span data-stu-id="706cc-138">If it received a response from the Server but the Server is unable to assign the address, the application will be notified by the DHCPv6 Client server error callback if configured with one (also in *nx_dhcpv6_client_create).*</span></span> <span data-ttu-id="706cc-139">Se o Cliente alcançou o estado BOUND mas depois falhou na verificação do PAI, verá uma mudança de estado de BOUND para INIT.</span><span class="sxs-lookup"><span data-stu-id="706cc-139">If the Client achieved the BOUND state but then failed the DAD check, it will see a state change from BOUND to INIT.</span></span> <span data-ttu-id="706cc-140">Note que uma aplicação ativada para o PAI deve dar tempo para o cheque do PAI após o início do processo de pedido.</span><span class="sxs-lookup"><span data-stu-id="706cc-140">Note that an application that is enabled for DAD must allow time for the DAD check after starting the request process.</span></span> <span data-ttu-id="706cc-141">Normalmente, isto é cerca de 400-500 carrapatos (4-5 segundos na maioria dos casos).</span><span class="sxs-lookup"><span data-stu-id="706cc-141">Typically this is about 400-500 ticks (4-5 seconds in most cases).</span></span>

### <a name="relinquishing-an-ipv6-address"></a><span data-ttu-id="706cc-142">Renunciar a um endereço IPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-142">Relinquishing an IPv6 Address</span></span>

<span data-ttu-id="706cc-143">Se e quando o Cliente precisar de lançar um endereço IPv6 atribuído, informa o servidor DHCPv6 ligando para o serviço *nx_dhcpv6_request_release:*</span><span class="sxs-lookup"><span data-stu-id="706cc-143">If and when the Client needs to release an assigned IPv6 address, it informs the DHCPv6 server by calling the *nx_dhcpv6_request_release* service:</span></span>

### <a name="uint-nx_dhcpv6_request_releasenx_dhcpv6-dhcpv6_ptr"></a><span data-ttu-id="706cc-144">UINT nx_dhcpv6_request_release(dhcpv6_ptr \* NX_DHCPV6)</span><span class="sxs-lookup"><span data-stu-id="706cc-144">UINT nx_dhcpv6_request_release(NX_DHCPV6 \*dhcpv6_ptr)</span></span>

<span data-ttu-id="706cc-145">O Cliente DHCPv6 envia uma mensagem de LANÇAMENTO unicast contendo os endereços atribuídos ao Servidor que atribuiu o endereço e aguarda uma RESPOSTA confirmando que o Servidor recebeu a mensagem.</span><span class="sxs-lookup"><span data-stu-id="706cc-145">The DHCPv6 Client sends a unicast RELEASE message containing the assigned addresses to the Server who assigned the address and waits for a REPLY confirming the Server received the message.</span></span>

<span data-ttu-id="706cc-146">Nota: Existe um processo diferente para o Cliente que está a desligar-se mas planeia continuar a utilizar os endereços IPv6 atribuídos no reboot.</span><span class="sxs-lookup"><span data-stu-id="706cc-146">Note: There is a different process for the Client that is powering down but plans to continue using the assigned IPv6 addresses on reboot.</span></span> <span data-ttu-id="706cc-147">Não envia a mensagem RELEASE ao desligar a menos que planeie solicitar um novo endereço de alimentação.</span><span class="sxs-lookup"><span data-stu-id="706cc-147">It does not send the RELEASE message on powering down unless it plans to request a new address on power up.</span></span> <span data-ttu-id="706cc-148">Consulte "Requisitos de Memória Não Voláteis" para obter uma explicação sobre esta situação.</span><span class="sxs-lookup"><span data-stu-id="706cc-148">See “Non Volatile Memory Requirements” for explanation of this situation.</span></span>

### <a name="dhcpv6-lease-timeouts"></a><span data-ttu-id="706cc-149">Intervalos de tempo de locação DHCPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-149">DHCPv6 Lease Timeouts</span></span>

<span data-ttu-id="706cc-150">O contrato de arrendamento IPv6 atribuído pelo Servidor contém dois parâmetros de tempo limite, T1 e T2 em cada bloco De Associação de Identidade – Endereços Não Temporários (IANA).</span><span class="sxs-lookup"><span data-stu-id="706cc-150">The IPv6 lease assigned by the Server contains two timeout parameters, T1 and T2 in each Identity Association – Non Temporary Addresses (IANA) block.</span></span> <span data-ttu-id="706cc-151">Um IANA é descrito em outros lugares neste Manual do Utilizador.</span><span class="sxs-lookup"><span data-stu-id="706cc-151">An IANA is described in elsewhere in this User Guide.</span></span> <span data-ttu-id="706cc-152">Se o tempo decorrido a partir do momento em que o Cliente DHCPv6 estava vinculado ao endereço IPv6 atribuído é igual a T1, o Cliente DHCPv6 começa automaticamente a renovar o endereço IPv6 enviando uma mensagem RENOVAR.</span><span class="sxs-lookup"><span data-stu-id="706cc-152">If the elapsed time from when the DHCPv6 Client was bound to the assigned IPv6 address equals T1, the DHCPv6 Client automatically starts renewing the IPv6 address by sending a RENEW message.</span></span> <span data-ttu-id="706cc-153">Se o tempo decorrido for igual a T2, o Cliente DHCPv6 envia automaticamente uma mensagem REBIND se não receber respostas aos seus pedidos DEV.</span><span class="sxs-lookup"><span data-stu-id="706cc-153">If the elapsed time equals T2, DHCPv6 Client automatically sends a REBIND message if it received no responses to its RENEW requests.</span></span>

<span data-ttu-id="706cc-154">Dois outros parâmetros de locação IPv6, preferidos e válidos, são atribuídos a cada bloco da Associação de Identidade (IA) contido no bloco IANA.</span><span class="sxs-lookup"><span data-stu-id="706cc-154">Two other IPv6 lease parameters, preferred and valid lifetime, are assigned with each Identity Association (IA) block contained in the IANA block.</span></span> <span data-ttu-id="706cc-155">As vidas preferidas e válidas são quando o endereço IPv6 atribuído é depreciado ou inválido, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="706cc-155">The preferred and valid lifetimes are when the assigned IPv6 address is deprecated or invalid, respectively.</span></span> <span data-ttu-id="706cc-156">T1 deve ser menos do que a vida preferida.</span><span class="sxs-lookup"><span data-stu-id="706cc-156">T1 must be less than the preferred lifetime.</span></span> <span data-ttu-id="706cc-157">T2 deve ser inferior à vida útil válida.</span><span class="sxs-lookup"><span data-stu-id="706cc-157">T2 must be less than the valid lifetime.</span></span>

### <a name="ip-thread-task-requirements"></a><span data-ttu-id="706cc-158">Requisitos de tarefa ip thread</span><span class="sxs-lookup"><span data-stu-id="706cc-158">IP Thread Task Requirements</span></span>

<span data-ttu-id="706cc-159">O Cliente NetX Duo DHCPv6 requer a criação de uma instância IP NetX Duo anterior à criação do Cliente DHCPv6 para utilizar os serviços de clientes DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-159">The NetX Duo DHCPv6 Client requires creation of a NetX Duo IP instance previous to creating the DHCPv6 Client to use DHCPv6 Client services.</span></span>

<span data-ttu-id="706cc-160">UDP, IPv6 e ICMPv6 devem ser ativados na instância IP antes da utilização do Cliente DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-160">UDP, IPv6, and ICMPv6 must be enabled on the IP instance prior to the using DHCPv6 Client.</span></span>

  - <span data-ttu-id="706cc-161">*nx_udp_enable*</span><span class="sxs-lookup"><span data-stu-id="706cc-161">*nx_udp_enable*</span></span>

  - <span data-ttu-id="706cc-162">*nxd_ipv6_enable*</span><span class="sxs-lookup"><span data-stu-id="706cc-162">*nxd_ipv6_enable*</span></span>

  - <span data-ttu-id="706cc-163">*nxd_icmp_enable*</span><span class="sxs-lookup"><span data-stu-id="706cc-163">*nxd_icmp_enable*</span></span>

### <a name="packet-pool-requirements"></a><span data-ttu-id="706cc-164">Requisitos de piscina de pacotes</span><span class="sxs-lookup"><span data-stu-id="706cc-164">Packet Pool Requirements</span></span>

<span data-ttu-id="706cc-165">NetX Duo DHCPv6 A criação do cliente requer um pacote de pacotes previamente criado para o envio de mensagens DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-165">NetX Duo DHCPv6 Client creation requires a previously created packet pool for sending DHCPv6 messages.</span></span> <span data-ttu-id="706cc-166">O tamanho do pacote em termos de carga útil de pacotes e número de pacotes disponíveis é configurável pelo utilizador, e depende do volume antecipado de mensagens DHCPv6 e outras transmissões que a aplicação irá enviar.</span><span class="sxs-lookup"><span data-stu-id="706cc-166">The size of the packet pool in terms of packet payload and number of packets available is user configurable, and depends on the anticipated volume of DHCPv6 messages and other transmissions the application will be sending.</span></span>

<span data-ttu-id="706cc-167">Uma mensagem típica de DHCPv6 é de cerca de 200 bytes dependendo do número de endereços IA e opções DHCPv6 solicitadas pelo Cliente.</span><span class="sxs-lookup"><span data-stu-id="706cc-167">A typical DHCPv6 message is about 200 bytes depending on the number of IA addresses and DHCPv6 options requested by the Client.</span></span>

### <a name="network-requirements"></a><span data-ttu-id="706cc-168">Requisitos de rede</span><span class="sxs-lookup"><span data-stu-id="706cc-168">Network Requirements</span></span>

<span data-ttu-id="706cc-169">O Cliente NetX Duo DHCPv6 requer a criação de uma tomada UDP ligada à porta 546.</span><span class="sxs-lookup"><span data-stu-id="706cc-169">The NetX Duo DHCPv6 Client requires the creation of UDP socket bound to port 546.</span></span> <span data-ttu-id="706cc-170">A tomada é criada quando a tarefa do Cliente DHCPv6 é criada.</span><span class="sxs-lookup"><span data-stu-id="706cc-170">The socket is created when the DHCPv6 Client task is created.</span></span>

### <a name="non-volatile-memory-requirements"></a><span data-ttu-id="706cc-171">Requisitos de memória não voláteis</span><span class="sxs-lookup"><span data-stu-id="706cc-171">Non Volatile Memory Requirements</span></span>

<span data-ttu-id="706cc-172">Se um Cliente DHCPv6 lançar o seu contrato de arrendamento IPv6 com o Servidor DHCPv6 ao desligar-se e solicitar novos endereços IPv6 no reboot, então não é necessário armazenamento de memória não volátil.</span><span class="sxs-lookup"><span data-stu-id="706cc-172">If a DHCPv6 Client releases its IPv6 lease with the DHCPv6 Server when powering down, and requests new IPv6 address(es) on reboot, then non volatile memory storage is not required.</span></span> <span data-ttu-id="706cc-173">Se um Cliente pretender continuar a utilizar o seu contrato de arrendamento atribuído, deve armazenar determinadas informações sobre o Cliente DHCPv6 para memória não volátil através de reboots.</span><span class="sxs-lookup"><span data-stu-id="706cc-173">If a Client wishes to continue using its assigned lease, it must store certain information about the DHCPv6 Client to non volatile memory across reboots.</span></span>

<span data-ttu-id="706cc-174">Os requisitos de memória não voláteis e a API do cliente DHCPv6 são discutidos mais aprofundadamente na **Utilização do Cliente DHCPv6 da NetX Duo** no Capítulo Dois.</span><span class="sxs-lookup"><span data-stu-id="706cc-174">Non volatile memory requirements and the DHCPv6 Client API are discussed further in **Using the NetX Duo DHCPv6 Client** in Chapter Two.</span></span>

### <a name="netx-duo-dhcpv6-client-limitations"></a><span data-ttu-id="706cc-175">Limitações do cliente NetX Duo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-175">NetX Duo DHCPv6 Client Limitations</span></span>

<span data-ttu-id="706cc-176">O lançamento atual do Cliente DhCPv6 da NetX Duo tem as seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="706cc-176">The current release of the NetX Duo DHCPv6 Client has the following limitations:</span></span>

  - <span data-ttu-id="706cc-177">O Cliente NetX Duo DHCPv6 não suporta a opção Server Unicast para enviar mensagens UNICAST DHCPv6 para o Servidor DHCPv6, mesmo que o Servidor indique que tal é permitido.</span><span class="sxs-lookup"><span data-stu-id="706cc-177">NetX Duo DHCPv6 Client does not support the Server Unicast option for sending unicast DHCPv6 messages to the DHCPv6 Server even if the Server indicates this is permitted.</span></span>

  - <span data-ttu-id="706cc-178">O Cliente NetX Duo DHCPv6 não suporta o pedido de Reconfigure no qual um Servidor inicia alterações de endereço IPv6 aos Clientes da rede.</span><span class="sxs-lookup"><span data-stu-id="706cc-178">NetX Duo DHCPv6 Client does not support the Reconfigure request in which a Server initiates IPv6 address changes to the Clients on the network.</span></span>

  - <span data-ttu-id="706cc-179">O Cliente NetX Duo DHCPv6 não suporta o formato Enterprise para o bloco de controlo de identificador exclusivo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-179">NetX Duo DHCPv6 Client does not support the Enterprise format for the DHCPv6 Unique Identifier control block.</span></span> <span data-ttu-id="706cc-180">Suporta apenas o formato Link Layer e Link Layer Plus Time.</span><span class="sxs-lookup"><span data-stu-id="706cc-180">It only supports Link Layer and Link Layer Plus Time format.</span></span>

  - <span data-ttu-id="706cc-181">O Cliente NetX Duo DHCPv6 não suporta pedidos de endereço da Associação Temporária (TA), mas apoia pedidos de opção não temporários (IANA).</span><span class="sxs-lookup"><span data-stu-id="706cc-181">NetX Duo DHCPv6 Client does not support Temporary Association (TA) address requests, but does support Non Temporary (IANA) option requests.</span></span>

## <a name="multihome-and-multiple-address-support"></a><span data-ttu-id="706cc-182">Suporte multihome e de endereços múltiplos</span><span class="sxs-lookup"><span data-stu-id="706cc-182">Multihome and Multiple Address Support</span></span>

<span data-ttu-id="706cc-183">O Cliente DHCPv6 suporta múltiplas interfaces e vários endereços por interface.</span><span class="sxs-lookup"><span data-stu-id="706cc-183">The DHCPv6 Client supports multiple interfaces and multiple addresses per interface.</span></span> <span data-ttu-id="706cc-184">O serviço dhcpv6 Client, *nx_dhcpv6_client_set_interface* permite que a aplicação do Cliente desabrada a interface de rede na qual a aplicação irá comunicar com o Servidor DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="706cc-184">The DHCPv6 Client service, *nx_dhcpv6_client_set_interface* enables the Client application to set the network interface on which the application will be communicating with the DHCPv6 Server.</span></span> <span data-ttu-id="706cc-185">O Cliente DHCPv6 falha na interface primária (índice zero).</span><span class="sxs-lookup"><span data-stu-id="706cc-185">The DHCPv6 Client defaults to the primary interface (index zero).</span></span>

<span data-ttu-id="706cc-186">Para vários endereços por interface, o Cliente DHCPv6 mantém uma lista interna de endereços a partir do índice 0.</span><span class="sxs-lookup"><span data-stu-id="706cc-186">For multiple addresses per interface, the DHCPv6 Client keeps an internal list of addresses starting at index 0.</span></span> <span data-ttu-id="706cc-187">Note que o mesmo endereço registado no Cliente DHCPv6 pode não estar necessariamente localizado no mesmo índice na tabela IP dos endereços de interface.</span><span class="sxs-lookup"><span data-stu-id="706cc-187">Note that the same address registered with the DHCPv6 Client may not necessarily be located at the same index in the IP table of interface addresses.</span></span>

<span data-ttu-id="706cc-188">Para os serviços de clientes DHCPv6 que recuperam informações sobre o contrato de arrendamento de endereços IPv6 do Cliente, alguns exigem que seja especificado um índice de endereço.</span><span class="sxs-lookup"><span data-stu-id="706cc-188">For DHCPv6 Client services that retrieve information about the Client IPv6 address lease, some require an address index to be specified.</span></span> <span data-ttu-id="706cc-189">Um exemplo para a obtenção das vidas preferidas e válidas é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="706cc-189">An example for obtaining the preferred and valid lifetimes is shown below:</span></span>

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                              UINT address_index, 
                                              NXD_ADDRESS *ip_address,
                                              ULONG preferred_lifetime, 
                                              ULONG *valid_lifetime)
```

<span data-ttu-id="706cc-190">A aplicação Do Cliente também pode recuperar o número de endereços IPv6 válidos atribuídos a partir do serviço *nx_dhcpv6_get_valid_ip_address_count:*</span><span class="sxs-lookup"><span data-stu-id="706cc-190">The Client application can also retrieve the number of valid IPv6 addresses assigned from the *nx_dhcpv6_get_valid_ip_address_count* service:</span></span>

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count)
```

<span data-ttu-id="706cc-191">Os serviços de clientes Legacy DHCPv6 que foram criados antes de vários endereços terem sido suportados no NetX Duo não têm um índice de endereços.</span><span class="sxs-lookup"><span data-stu-id="706cc-191">Legacy DHCPv6 Client services which were created before multiple addresses were supported in NetX Duo do not take an address index.</span></span> <span data-ttu-id="706cc-192">Portanto, com estes serviços, os dados solicitados são retirados do endereço principal global da IA, independentemente de quantos endereços de IA são atribuídos ao Cliente.</span><span class="sxs-lookup"><span data-stu-id="706cc-192">Therefore, with these services, the data requested is taken from the primary global IA address, regardless how many IA addresses are assigned to the Client.</span></span> <span data-ttu-id="706cc-193">Apresentamos um exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="706cc-193">An example is shown below:</span></span>

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address)
```

## <a name="netx-duo-dhcpv6-client-callback-functions"></a><span data-ttu-id="706cc-194">Funções de callback de clientes NetX Duo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="706cc-194">NetX Duo DHCPv6 Client Callback Functions</span></span>

<span data-ttu-id="706cc-195">*nx_dhcpv6_state_change_callback*</span><span class="sxs-lookup"><span data-stu-id="706cc-195">*nx_dhcpv6_state_change_callback*</span></span>

<span data-ttu-id="706cc-196">Quando o Cliente DHCPv6 muda para um novo estado DHCPv6 como resultado do processamento de um pedido DHCPv6, notifica a aplicação com esta função de retorno.</span><span class="sxs-lookup"><span data-stu-id="706cc-196">When the DHCPv6 Client changes to a new DHCPv6 state as a result of processing a DHCPv6 request, it notifies the application with this callback function.</span></span>

<span data-ttu-id="706cc-197">*nx_dhcpv6_server_error_handler*</span><span class="sxs-lookup"><span data-stu-id="706cc-197">*nx_dhcpv6_server_error_handler*</span></span>

<span data-ttu-id="706cc-198">Quando o Cliente DHCPv6 recebe uma resposta do Servidor contendo uma opção *de Estado* com um estado não-zero (não bem sucedido), notifica a aplicação com esta chamada que inclui o código de estado de erro do Servidor.</span><span class="sxs-lookup"><span data-stu-id="706cc-198">When the DHCPv6 Client receives a Server reply containing a *Status* option with a non-zero (non successful) status, it notifies the application with this callback which includes the Server error status code.</span></span>

<span data-ttu-id="706cc-199">Nota: Uma vez que estas funções de retorno são chamadas da tarefa de thread do Cliente DHCPv6, a aplicação do Cliente NÃO deve ligar para nenhum serviço de Cliente NetX Duo DHCPv6 que exija controlo mutex do Cliente DHCPv6, como *nx_dhcpv6_start, nx_dhcpv6_stop* e qualquer um dos API que enviam mensagens diretamente a partir da *chamada, por exemplo, nx_dhcpv6_request_release*.</span><span class="sxs-lookup"><span data-stu-id="706cc-199">Note: Since these callback functions are called from the DHCPv6 Client thread task, the Client application must NOT call any NetX Duo DHCPv6 Client services that require mutex control of the DHCPv6 Client such as *nx_dhcpv6_start, nx_dhcpv6_stop,* and any of the API that send messages directly from the callback e.g. *nx_dhcpv6_request_release*.</span></span>

## <a name="dhcpv6-rfcs"></a><span data-ttu-id="706cc-200">DHCPv6 RFCs</span><span class="sxs-lookup"><span data-stu-id="706cc-200">DHCPv6 RFCs</span></span>

<span data-ttu-id="706cc-201">NetX Duo DHCP está em conformidade com RFC3315, RFC3646 e RFCs relacionados.</span><span class="sxs-lookup"><span data-stu-id="706cc-201">NetX Duo DHCP is compliant with RFC3315, RFC3646, and related RFCs.</span></span>