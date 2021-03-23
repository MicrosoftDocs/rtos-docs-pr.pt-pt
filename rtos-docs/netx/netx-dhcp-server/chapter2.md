---
title: Capítulo 2 - Instalação e utilização do Servidor Azure RTOS NetX DHCP
description: Este capítulo contém uma descrição de vários problemas relacionados com a instalação, configuração e utilização do componente do servidor Azure RTOS NetX DHCP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 034a4d74c566fbfe94981a42b7e06e7f2ee79d25
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826791"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-dhcp-server"></a><span data-ttu-id="0b16c-103">Capítulo 2 - Instalação e utilização do Servidor Azure RTOS NetX DHCP</span><span class="sxs-lookup"><span data-stu-id="0b16c-103">Chapter 2 - Installation and use of the Azure RTOS NetX DHCP Server</span></span>

<span data-ttu-id="0b16c-104">Este capítulo contém uma descrição de vários problemas relacionados com a instalação, configuração e utilização do componente Azure RTOS NetX DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX DHCP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="0b16c-105">Distribuição de Produtos</span><span class="sxs-lookup"><span data-stu-id="0b16c-105">Product Distribution</span></span>

<span data-ttu-id="0b16c-106">O Azure RTOS NetX DHCP Server pode ser obtido a partir do nosso repositório de código fonte pública em [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="0b16c-106">Azure RTOS NetX DHCP Server can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="0b16c-107">O pacote inclui dois ficheiros de origem e um ficheiro PDF que contém este documento, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="0b16c-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="0b16c-108">**nx_dhcp_server.h:** Ficheiro de cabeçalho para o Servidor DHCP netX</span><span class="sxs-lookup"><span data-stu-id="0b16c-108">**nx_dhcp_server.h**: Header file for NetX DHCP Server</span></span>
- <span data-ttu-id="0b16c-109">**nx_dhcp_server.c**: Ficheiro C Fonte para o Servidor DHCP netX</span><span class="sxs-lookup"><span data-stu-id="0b16c-109">**nx_dhcp_server.c**: C Source file for NetX DHCP Server</span></span>
- <span data-ttu-id="0b16c-110">**nx_dhcp_server.pdf**: Descrição em PDF do NetX DHCP Server</span><span class="sxs-lookup"><span data-stu-id="0b16c-110">**nx_dhcp_server.pdf**: PDF description of NetX DHCP Server</span></span>
- <span data-ttu-id="0b16c-111">**demo_netx_dhcp_server.c**: Demonstração do Servidor NetX DHCP</span><span class="sxs-lookup"><span data-stu-id="0b16c-111">**demo_netx_dhcp_server.c**: NetX DHCP Server demonstration</span></span>

## <a name="dhcp-installation"></a><span data-ttu-id="0b16c-112">Instalação DHCP</span><span class="sxs-lookup"><span data-stu-id="0b16c-112">DHCP Installation</span></span>

<span data-ttu-id="0b16c-113">Para utilizar o NetX DHCP Server, toda a distribuição mencionada anteriormente deve ser copiada para o mesmo diretório onde o NetX está instalado.</span><span class="sxs-lookup"><span data-stu-id="0b16c-113">In order to use NetX DHCP Server, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="0b16c-114">Por exemplo, se o NetX for instalado no diretório "*\threadx\arm7\green*", então os ficheiros *nx_dhcp_server.h* e *nx_dhpc_server.c* devem ser copiados para este diretório.</span><span class="sxs-lookup"><span data-stu-id="0b16c-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_dhcp_server.h* and *nx_dhpc_server.c* files should be copied into this directory.</span></span>

## <a name="using-netx-dhcp-server"></a><span data-ttu-id="0b16c-115">Usando o servidor DHCP NetX</span><span class="sxs-lookup"><span data-stu-id="0b16c-115">Using NetX DHCP Server</span></span>

<span data-ttu-id="0b16c-116">A utilização do NetX DHCP Server é fácil.</span><span class="sxs-lookup"><span data-stu-id="0b16c-116">Using NetX DHCP Server is easy.</span></span> <span data-ttu-id="0b16c-117">Basicamente, o código de aplicação deve incluir *nx_dhcp_server.h* depois de incluir *tx_api.h* e *nx_api.h,* para utilizar o ThreadX e o NetX, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-117">Basically, the application code must include *nx_dhcp_server.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="0b16c-118">Uma vez *incluído nx_dhcp_server.h,* o código de aplicação é então capaz de fazer as chamadas de função DHCP especificadas mais tarde neste guia.</span><span class="sxs-lookup"><span data-stu-id="0b16c-118">Once *nx_dhcp_server.h* is included, the application code is then able to make the DHCP function calls specified later in this guide.</span></span> <span data-ttu-id="0b16c-119">O pedido também deve incluir *nx_dhcp_server.c* no processo de construção.</span><span class="sxs-lookup"><span data-stu-id="0b16c-119">The application must also include *nx_dhcp_server.c* in the build process.</span></span> <span data-ttu-id="0b16c-120">Este ficheiro deve ser compilado da mesma forma que outros ficheiros de aplicações e a sua forma de objeto deve ser ligada juntamente com os ficheiros da aplicação.</span><span class="sxs-lookup"><span data-stu-id="0b16c-120">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="0b16c-121">Para obter mais detalhes sobre a utilização do NetX DHCP Server, consulte as seguintes secções [Requisitos do NetX DHCPServer](#requirements-of-the-netx-dhcp-server) e [Restrições do Servidor DHCP NetX](#constraints-of-the-netx-dhcp-server).</span><span class="sxs-lookup"><span data-stu-id="0b16c-121">For more details on using NetX DHCP Server, see the following sections [Requirements of the NetX DHCPServer](#requirements-of-the-netx-dhcp-server) and [Constraints of the NetX DHCP Server](#constraints-of-the-netx-dhcp-server).</span></span>

> [!NOTE]
> <span data-ttu-id="0b16c-122">Uma vez que o DHCP utiliza os serviços de UDP NetX, o UDP deve ser ativado com a chamada *nx_udp_enable* antes de utilizar o DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-122">Since DHCP utilizes NetX UDP services, UDP must be enabled with the *nx_udp_enable* call prior to using DHCP.</span></span>

## <a name="requirements-of-the-netx-dhcp-server"></a><span data-ttu-id="0b16c-123">Requisitos do Servidor DhCP NetX</span><span class="sxs-lookup"><span data-stu-id="0b16c-123">Requirements of the NetX DHCP Server</span></span>

<span data-ttu-id="0b16c-124">O NetX DHCP Server requer uma porta de tomada UDP atribuída à conhecida porta DHCP 67.</span><span class="sxs-lookup"><span data-stu-id="0b16c-124">The NetX DHCP Server requires a UDP socket port assigned to the well known DHCP port 67.</span></span> <span data-ttu-id="0b16c-125">Para criar o Servidor DHCP, a aplicação deve criar um conjunto de pacotes com carga útil de pacotes de pelo menos 548 bytes mais cabeçalhos IP, UDP e Ethernet (que totalizam 44 bytes com 4 bytes de alinhamento).</span><span class="sxs-lookup"><span data-stu-id="0b16c-125">To create the DHCP Server, the application must create a packet pool with packet payload at least 548 bytes plus IP, UDP and Ethernet headers (which total 44 bytes with 4 byte alignment).</span></span>

<span data-ttu-id="0b16c-126">Presume-se que o Servidor e o Cliente estão ambos a utilizar as definições de endereço de hardware Ethernet:</span><span class="sxs-lookup"><span data-stu-id="0b16c-126">It is assumed that the Server and Client are both using Ethernet hardware address settings:</span></span>

- <span data-ttu-id="0b16c-127">**Tipo de hardware**: 1</span><span class="sxs-lookup"><span data-stu-id="0b16c-127">**Hardware type**: 1</span></span>
- <span data-ttu-id="0b16c-128">**Comprimento do hardware**: 6</span><span class="sxs-lookup"><span data-stu-id="0b16c-128">**Hardware length**: 6</span></span>
- <span data-ttu-id="0b16c-129">**Lúpulo**: 0</span><span class="sxs-lookup"><span data-stu-id="0b16c-129">**Hops**: 0</span></span>

### <a name="multiple-client-sessions"></a><span data-ttu-id="0b16c-130">Múltiplas Sessões de Clientes</span><span class="sxs-lookup"><span data-stu-id="0b16c-130">Multiple Client Sessions</span></span>

<span data-ttu-id="0b16c-131">O NetX DHCP Server pode lidar com várias sessões de Cliente mantendo uma tabela de clientes DHCP ativos e o que 'estado' o Cliente está em, por exemplo, estados DHCP INIT, BOOT, SELECTING, REQUESTING, RENOVAR etc. Se o tempo de sessão expirar antes de receber a próxima mensagem do Cliente, a menos que esse Cliente esteja ligado a uma locação IP, o Servidor limpará os dados da sessão do Cliente e devolverá o endereço IP atribuído ao pool disponível.</span><span class="sxs-lookup"><span data-stu-id="0b16c-131">The NetX DHCP Server can handles multiple Client sessions by keeping a table of active DHCP clients and what 'state' the Client is in e.g. DHCP states INIT, BOOT, SELECTING, REQUESTING, RENEWING etc. If the session time out expires before receiving the next Client message, unless that Client is bound to an IP lease, the Server will clear the Client session data and return the assigned IP address back to the available pool.</span></span> <span data-ttu-id="0b16c-132">Se o Servidor receber várias mensagens DISCOVER do mesmo Cliente, o Servidor reinicia o tempo de saída da sessão e mantém o endereço IP reservado para o Cliente aceitar numa mensagem REQUEST subsequente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-132">If the Server receives multiple DISCOVER messages from the same Client the Server resets the session time out and keeps the IP address reserved for the Client to accept in a subsequent REQUEST message.</span></span>

<span data-ttu-id="0b16c-133">O NetX DHCP Server também aceita o pedido de DHCP do cliente único, por exemplo, o Cliente apenas envia uma mensagem REQUEST.</span><span class="sxs-lookup"><span data-stu-id="0b16c-133">The NetX DHCP Server also accepts the single state Client DHCP request e.g. the Client only sends a REQUEST message.</span></span> <span data-ttu-id="0b16c-134">Isto pressupõe que o Cliente foi previamente atribuído a um contrato de arrendamento IP do servidor DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-134">This assumes the Client has been previously assigned an IP lease from the DHCP server.</span></span>

### <a name="setting-interface-specific-network-parameters-server-responses"></a><span data-ttu-id="0b16c-135">Definição de interface respostas de servidor de parâmetros de rede específicas</span><span class="sxs-lookup"><span data-stu-id="0b16c-135">Setting Interface Specific Network Parameters Server Responses</span></span>

<span data-ttu-id="0b16c-136">A aplicação pode definir os parâmetros do router, da máscara de sub-rede e do servidor DNS para cada interface que lida com os pedidos do Cliente DHCP, utilizando o serviço *nx_dhcp_set_interface_network_parameters.*</span><span class="sxs-lookup"><span data-stu-id="0b16c-136">The application can set the router, subnet mask and DNS server parameters for each interface it handles DHCP Client requests, using the *nx_dhcp_set_interface_network_parameters* service.</span></span> <span data-ttu-id="0b16c-137">Caso contrário, estes parâmetros estão indefinidos no gateway IP da interface primária do Servidor, na sua sub-rede de rede DHCP e no endereço IP do Servidor DHCP, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-137">Otherwise these parameters are defaulted to the IP gateway on the Server's primary interface, its DHCP network subnet, and DHCP Server IP address, respectively.</span></span>

<span data-ttu-id="0b16c-138">O Servidor DHCP inclui estes parâmetros nos dados de opção das mensagens DHCP que envia aos clientes DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-138">The DHCP Server includes these parameters in the option data of DHCP messages it sends to DHCP clients.</span></span>

### <a name="assigning-ip-addresses-to-the-client"></a><span data-ttu-id="0b16c-139">Atribuição de endereços IP ao Cliente</span><span class="sxs-lookup"><span data-stu-id="0b16c-139">Assigning IP addresses to the Client</span></span>

<span data-ttu-id="0b16c-140">Se a mensagem Do Cliente DISCOVER não especificar um endereço IP solicitado, o Servidor DHCP pode utilizar um a partir da sua própria piscina.</span><span class="sxs-lookup"><span data-stu-id="0b16c-140">If the Client DISCOVER message does not specify a requested IP address, the DHCP Server can use one from its own pool.</span></span> <span data-ttu-id="0b16c-141">Se o Servidor não tiver endereços IP disponíveis, enviará ao Cliente uma mensagem NACK.</span><span class="sxs-lookup"><span data-stu-id="0b16c-141">If the Server has no available IP addresses it will send the Client a NACK message.</span></span>

<span data-ttu-id="0b16c-142">O Servidor DHPC NetX concederá o endereço IP solicitado na mensagem Cliente REQUEST desde que o endereço IP esteja disponível e possa ser encontrado na base de dados de endereços IP do Servidor.</span><span class="sxs-lookup"><span data-stu-id="0b16c-142">The NetX DHCP Server will grant the requested IP address in the Client REQUEST message as long as the IP address is available and can be found in the Server IP address database.</span></span> <span data-ttu-id="0b16c-143">A aplicação cria a lista de endereços IP disponíveis do Servidor para a atribuição a Clientes DHCP utilizando o serviço *nx_dhcp_create_server_ip_address_list.*</span><span class="sxs-lookup"><span data-stu-id="0b16c-143">The application creates the Server's list of available IP addresses for assigning to DHCP Clients using the *nx_dhcp_create_server_ip_address_list* service.</span></span> <span data-ttu-id="0b16c-144">Se o Servidor não tiver os endereços IP solicitados ou for atribuído a outro anfitrião, enviará ao Cliente uma mensagem NACK.</span><span class="sxs-lookup"><span data-stu-id="0b16c-144">If the Server does not have the requested IP addresses or it is assigned to another host it will send the Client a NACK message.</span></span>

<span data-ttu-id="0b16c-145">Quando o Servidor DHCP recebe um pedido de Cliente, identifica esse Cliente utilizando exclusivamente o endereço MAC do Cliente no campo de endereços MAC do Cliente na mensagem DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-145">When the DHCP Server receives a Client request, it identifies that Client uniquely using the Client MAC address in the Client MAC address field in the DHCP message.</span></span> <span data-ttu-id="0b16c-146">Se o Cliente alterar o seu endereço MAC ou for transferido para outro sub-redes, deverá enviar uma mensagem RELEASE para o Servidor para devolver o endereço IP de volta ao pool disponível e solicitar um novo endereço IP no estado INIT.</span><span class="sxs-lookup"><span data-stu-id="0b16c-146">If the Client changes it's MAC address or is moved elsewhere onto another subnet it should send a RELEASE message to the Server to return the IP address back to the available pool, and request a new IP address in the INIT state.</span></span>

<span data-ttu-id="0b16c-147">Consulte a figura 1.1 da secção **Sistema de Pequenos Exemplos** para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0b16c-147">See Figure 1.1 of the **Small Example System** section for details.</span></span> <span data-ttu-id="0b16c-148">O número de endereços IP guardados na instância do Servidor DHCP está limitado ao tamanho do conjunto de endereços do servidor no bloco de controlo do servidor DHCP e definido pela opção configurável NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.</span><span class="sxs-lookup"><span data-stu-id="0b16c-148">The number of IP addresses saved to the DHCP Server instance is limited to the size of the server address array in the DHCP Server control block, and defined by the configurable option NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.</span></span>

### <a name="ip-address-lease-times"></a><span data-ttu-id="0b16c-149">Tempos de locação de endereços IP</span><span class="sxs-lookup"><span data-stu-id="0b16c-149">IP Address Lease Times</span></span>

<span data-ttu-id="0b16c-150">O Servidor DHCP também aceitará o tempo de locação do Cliente pedido se esse tempo de locação for inferior ao tempo de locação padrão do Servidor, que é definido em opção configurável NX_DHCP_DEFAULT_LEASE_TIME.</span><span class="sxs-lookup"><span data-stu-id="0b16c-150">The DHCP Server will also accept the request Client lease time if that lease time is less than the Server default lease time which is defined in configurable option NX_DHCP_DEFAULT_LEASE_TIME.</span></span> <span data-ttu-id="0b16c-151">Os tempos de renovação e reencadernação atribuídos ao Cliente são de 50% e 85% do tempo de arrendamento, respectivamente, a menos que o tempo de arrendamento seja infinito (0xFFFFFFFF), caso em que os tempos de renovação e reencadernação também são definidos para o infinito.</span><span class="sxs-lookup"><span data-stu-id="0b16c-151">Renewal and rebind times assigned to the Client are 50% and 85% of the lease time, respectively, unless the lease time is infinity (0xFFFFFFFF), in which case renewal and rebind times are also set to infinity.</span></span>

### <a name="dhcp-server-timeouts"></a><span data-ttu-id="0b16c-152">Intervalos de tempo do servidor DHCP</span><span class="sxs-lookup"><span data-stu-id="0b16c-152">DHCP Server Timeouts</span></span>

<span data-ttu-id="0b16c-153">O Servidor DHCP tem um tempo limite de sessão configurável para o utilizador, NX_DHCP_CLIENT_SESSION_TIMEOUT, para esperar pela próxima mensagem do Cliente DHCP, a menos que a sessão esteja concluída.</span><span class="sxs-lookup"><span data-stu-id="0b16c-153">The DHCP Server has a user configurable session timeout, NX_DHCP_CLIENT_SESSION_TIMEOUT, for waiting for the next DHCP Client message unless the session is completed.</span></span> <span data-ttu-id="0b16c-154">O tempo de ício é reiniciado quando o Servidor recebe a próxima mensagem do Cliente, independentemente de ser a mesma mensagem enviada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-154">The time out is reset when the Server receives the next message from the Client regardless if is the same message previously sent.</span></span>

### <a name="internal-error-handling"></a><span data-ttu-id="0b16c-155">Tratamento interno de erros</span><span class="sxs-lookup"><span data-stu-id="0b16c-155">Internal error handling</span></span>

<span data-ttu-id="0b16c-156">O Servidor DHCP recebe e processa pacotes de clientes DHCP na função *nx_dhcp_listen_for_messages.*</span><span class="sxs-lookup"><span data-stu-id="0b16c-156">The DHCP Server receives and processes DHCP Client packets in the *nx_dhcp_listen_for_messages* function.</span></span> <span data-ttu-id="0b16c-157">Esta função irá descontinuar o processamento do atual pacote do Cliente DHCP se o pacote for inválido, ou se o Servidor DHCP encontrar um erro interno.n *x_dhcp_listen_for_messages* retorne um estado de erro.</span><span class="sxs-lookup"><span data-stu-id="0b16c-157">This function will discontinue processing the current DHCP Client packet if the packet is invalid, or the DHCP Server encounters an internal error.n *x_dhcp_listen_for_messages* returns an error status.</span></span> <span data-ttu-id="0b16c-158">A linha do Servidor DHCP renuncia ao controlo brevemente do programador ThreadX antes de ligar para esta função para receber a próxima mensagem do Cliente DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-158">The DHCP Server thread relinquishes control briefly of the ThreadX scheduler before calling this function to receive the next DHCP Client message.</span></span> <span data-ttu-id="0b16c-159">Na versão atual não existe suporte para registo de retornas de estado de erro a partir de *nx_dhcp_listen_for_messages.*</span><span class="sxs-lookup"><span data-stu-id="0b16c-159">In the current release there is no logging support for error status returns from *nx_dhcp_listen_for_messages.*</span></span>

### <a name="option-55-parameter-request-list"></a><span data-ttu-id="0b16c-160">Opção 55: Lista de Pedidos de Parâmetros</span><span class="sxs-lookup"><span data-stu-id="0b16c-160">Option 55: Parameter Request List</span></span>

<span data-ttu-id="0b16c-161">O Servidor NetX DHCP deve ser configurado com um conjunto de opções para carregar para a lista de pedidos de parâmetros (55) na lista DE OFERTA e DHCPACK que transmite de volta para o Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-161">The NetX DHCP Server must be configured with a set of options to load to Parameter Request Option (55) list in the OFFER and DHCPACK messages it transmits back to the Client.</span></span> <span data-ttu-id="0b16c-162">Estas opções devem incluir dados de configuração crítica de rede para a rede cliente e por padrão é definido como endereço IP router, máscara de sub-rede e servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="0b16c-162">These options should include network critical configuration data for the Client network and by default is defined to be router IP address, subnet mask, and DNS server.</span></span> <span data-ttu-id="0b16c-163">A lista de opções é uma lista delimitada espacial e definida no NX_DHCP_DEFAULT_SERVER_OPTION_LIST configurável do utilizador.</span><span class="sxs-lookup"><span data-stu-id="0b16c-163">The option list is a space delimited list and defined in the user configurable NX_DHCP_DEFAULT_SERVER_OPTION_LIST.</span></span> <span data-ttu-id="0b16c-164">Note-se que o número de opções especificadas nesta lista deve ser igual NX_DHCP_DEFAULT_OPTION_LIST_SIZE que também é definido pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="0b16c-164">Note the number of options specified in this list must equal NX_DHCP_DEFAULT_OPTION_LIST_SIZE which is also user defined.</span></span>

## <a name="constraints-of-the-netx-dhcp-server"></a><span data-ttu-id="0b16c-165">Constrangimentos do Servidor DhCP NetX</span><span class="sxs-lookup"><span data-stu-id="0b16c-165">Constraints of the NetX DHCP Server</span></span>

### <a name="dhcp-messages"></a><span data-ttu-id="0b16c-166">Mensagens DHCP</span><span class="sxs-lookup"><span data-stu-id="0b16c-166">DHCP Messages</span></span>

<span data-ttu-id="0b16c-167">O Servidor DHCP NetX não verifica se um endereço IP não foi atribuído em outro lugar da rede antes de conceder o endereço IP ao Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-167">The NetX DHCP Server does not verify that an IP address has not been assigned elsewhere on the network before granting the IP address to the Client.</span></span> <span data-ttu-id="0b16c-168">Se existem vários servidores DHCP, este pode ser o caso.</span><span class="sxs-lookup"><span data-stu-id="0b16c-168">If there are multiple DHCP servers, this can indeed be the case.</span></span> <span data-ttu-id="0b16c-169">*De acordo com o RFC 2131, é da responsabilidade do Cliente verificar que o endereço IP é único na sua rede* (por exemplo, pingando o endereço).</span><span class="sxs-lookup"><span data-stu-id="0b16c-169">*As per RFC 2131, it is the Client's responsibility to verify the IP address is unique on its network* (e.g. pinging the address).</span></span> <span data-ttu-id="0b16c-170">Caso contrário, o Servidor deverá receber uma mensagem DECLINar com o endereço IP para atualizar a sua base de dados a partir do Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-170">If it is not, the Server should receive a DECLINE message with the IP address to update its database from the Client.</span></span>

<span data-ttu-id="0b16c-171">O Servidor DHCP NetX não emite mensagens FORCE_RENEW.</span><span class="sxs-lookup"><span data-stu-id="0b16c-171">The NetX DHCP Server does not issue FORCE_RENEW messages.</span></span> <span data-ttu-id="0b16c-172">Cabe ao Cliente DHCP renovar o seu contrato de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-172">It is up to the DHCP Client to renew its IP address lease.</span></span> <span data-ttu-id="0b16c-173">No entanto, o Servidor DHCP monitoriza o tempo restante em todos os endereços IP atribuídos na sua base de dados.</span><span class="sxs-lookup"><span data-stu-id="0b16c-173">However, the DHCP Server monitors the time remaining on all the assigned IP addresses in its database.</span></span> <span data-ttu-id="0b16c-174">Quando uma locação de endereço IP expira, esse endereço IP é devolvido ao pool de endereços IP disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0b16c-174">When an IP address lease expires, that IP address is returned to the pool of available IP addresses.</span></span> <span data-ttu-id="0b16c-175">Cabe, portanto, ao Cliente renovar/reencambido ativamente o seu contrato de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-175">Hence it is up to the Client to actively renew/rebind its IP address lease.</span></span>

<span data-ttu-id="0b16c-176">Os dados da sessão são apurados assim que o Cliente é concedido ("vinculado") a um contrato de arrendamento IP (ou um existente é renovado).</span><span class="sxs-lookup"><span data-stu-id="0b16c-176">Session data is cleared as soon as the Client either is granted ("bound") to an IP lease (or an existing one is renewed).</span></span> <span data-ttu-id="0b16c-177">Se um pacote de Cliente provar falso, ou o Cliente se apagar entre respostas, os dados da sessão são eliminados.</span><span class="sxs-lookup"><span data-stu-id="0b16c-177">If a Client packet proves bogus, or the Client times out between responses, session data is cleared.</span></span>

### <a name="saving-data-between-reboots"></a><span data-ttu-id="0b16c-178">Guardar dados entre reboots</span><span class="sxs-lookup"><span data-stu-id="0b16c-178">Saving Data Between Reboots</span></span>

<span data-ttu-id="0b16c-179">O NetX DHCP Server guarda os dados do Cliente, incluindo os parâmetros de pedido do DHCP numa tabela de registos do Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-179">The NetX DHCP Server saves Client data including DHCP request parameters in a Client record table.</span></span> <span data-ttu-id="0b16c-180">Esta tabela não é armazenada em memória não volátil, por isso, se o anfitrião do Servidor DHCP tiver de reiniciar, essa informação não é guardada entre reinicializações.</span><span class="sxs-lookup"><span data-stu-id="0b16c-180">This table is not stored in non volatile memory, so if the DHCP Server host must reboot that information is not saved between reboots.</span></span>

<span data-ttu-id="0b16c-181">O Servidor DHCP NetX guarda dados de locação de endereços IP numa tabela de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-181">The NetX DHCP Server saves IP address lease data in a IP address table.</span></span> <span data-ttu-id="0b16c-182">Esta tabela não é armazenada em memória não volátil, por isso, se o anfitrião do Servidor DHCP tiver de reiniciar, essa informação não é guardada entre reinicializações.</span><span class="sxs-lookup"><span data-stu-id="0b16c-182">This table is not stored in non volatile memory, so if the DHCP Server host must reboot that information is not saved between reboots.</span></span>

### <a name="relay-agents"></a><span data-ttu-id="0b16c-183">Agentes de retransmissão</span><span class="sxs-lookup"><span data-stu-id="0b16c-183">Relay Agents</span></span>

<span data-ttu-id="0b16c-184">O Servidor DHCP NetX está configurado com um endereço IP zero para o campo 'Relay agent' porque não suporta fora dos pedidos de DHCP da rede.</span><span class="sxs-lookup"><span data-stu-id="0b16c-184">The NetX DHCP Server is configured with a zero IP address for the 'Relay agent' field because it does not support out of network DHCP requests.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="0b16c-185">Sistema de Pequenos Exemplos</span><span class="sxs-lookup"><span data-stu-id="0b16c-185">Small Example System</span></span>

<span data-ttu-id="0b16c-186">Um exemplo de como é fácil utilizar o Servidor DHCP NetX é descrito na Figura 1.1 que aparece abaixo.</span><span class="sxs-lookup"><span data-stu-id="0b16c-186">An example of how easy it is to use the NetX DHCP Server is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="0b16c-187">Neste exemplo, o DHCP inclui o ficheiro *nx_dhcp_server.h* é trazido na linha 5.</span><span class="sxs-lookup"><span data-stu-id="0b16c-187">In this example, the DHCP include file *nx_dhcp_server.h* is brought in at line 5.</span></span> <span data-ttu-id="0b16c-188">O tamanho da pilha de fio do servidor DHCP, o tamanho da pilha de fio IP e o tamanho da pilha de fio de teste são todos definidos nas linhas 7-13.</span><span class="sxs-lookup"><span data-stu-id="0b16c-188">DHCP Server thread stack size, IP thread stack size and test thread stack size are all defined in lines 7-13.</span></span>

<span data-ttu-id="0b16c-189">Em primeiro lugar, é criada uma tarefa de fio de teste opcional para parar, reiniciar e eventualmente eliminar o servidor DHCP com a função "*test_thread_entry*" na linha 57.</span><span class="sxs-lookup"><span data-stu-id="0b16c-189">First, an optional test thread task for stopping, restarting and eventually deleting the DHCP server is created with the "*test_thread_entry*" function at line 57.</span></span> <span data-ttu-id="0b16c-190">Um bloco de controlo do servidor DHCP "*dhcp_server*" é definido como uma variável global na linha 20.</span><span class="sxs-lookup"><span data-stu-id="0b16c-190">A DHCP Server control block "*dhcp_server*" is defined as a global variable at line 20.</span></span> <span data-ttu-id="0b16c-191">Note que o conjunto de pacotes do servidor é criado com pacotes com uma carga útil pelo menos tão grande quanto a mensagem DHCP padrão (548 bytes mais bytes ip e cabeçalho UDP).</span><span class="sxs-lookup"><span data-stu-id="0b16c-191">Note that the server packet pool is created with packets having a payload at least as large as the standard DHCP message (548 bytes plus IP and UDP header bytes).</span></span> <span data-ttu-id="0b16c-192">Depois de criar com sucesso uma instância IP para o Servidor DHCP, a aplicação cria o Servidor DHCP na linha 96.</span><span class="sxs-lookup"><span data-stu-id="0b16c-192">After successfully creating an IP instance for the DHCP Server, the application creates the DHCP Server in line 96.</span></span> <span data-ttu-id="0b16c-193">Em seguida, a aplicação permite que a instância IP do servidor seja ativada por UDP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-193">Next, the application enables the Server IP instance to be UDP enabled.</span></span> <span data-ttu-id="0b16c-194">Antes de iniciar o Servidor DHCP, a lista de endereços IP disponível é criada na linha 137 utilizando o serviço *nx_dhcp_create_server_ip_address_list.*</span><span class="sxs-lookup"><span data-stu-id="0b16c-194">Before starting the DHCP Server, the available IP address list is created in line 137 using the *nx_dhcp_create_server_ip_address_list* service.</span></span> <span data-ttu-id="0b16c-195">Os parâmetros de configuração da rede são definidos na seguinte linha 138 utilizando o serviço *nx_dhcp_set_interface_network_parameters,* os serviços do Servidor DHCP ficam disponíveis quando a aplicação chama o *nx_dhcp_server_start* na linha 141.</span><span class="sxs-lookup"><span data-stu-id="0b16c-195">The network configuration parameters are set in the following line 138 using the *nx_dhcp_set_interface_network_parameters* service, DHCP Server services become available when the application calls the *nx_dhcp_server_start* at line 141.</span></span> <span data-ttu-id="0b16c-196">A tarefa do fio de teste demonstra a utilização de parar e reiniciar o servidor DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-196">The test thread task demonstrates the use of stopping and restarting the DHCP server.</span></span>

```c
/* This is a small demo of NetX DHCP Server for the high-performance NetX TCP/IP stack. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nx_dhcp_server.h"

#define     DEMO_TEST_STACK_SIZE       2048
#define     DEMO_SERVER_STACK_SIZE     2048
#define     SERVER_IP_ADDRESS_LIST     "192.168.2.10 192.168.2.11 192.168.2.12"
#define     PACKET_PAYLOAD             1000
#define     PACKET_POOL_SIZE           (PACKET_PAYLOAD * 10)
#define     SERVER_IP_THREAD_STACK     2048

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD          test_thread;
NX_PACKET_POOL     server_pool;
NX_IP              server_ip;
NX_DHCP_SERVER     dhcp_server;

/* Define the counters used in the demo application... */

ULONG             state_changes;

/* Define thread prototypes. */

void     test_thread_entry(ULONG thread_input);
void     nx_etherDriver_mcf5485(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the test thread. */
    status = tx_thread_create(&test_thread, "test thread", test_thread_entry, 0,
                pointer, TEST_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_DONT_START);

    if (status)
    {
        printf("Error with DHCP test thread create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the DHCP Server packet pool. */
    status = nx_packet_pool_create(&server_pool, "NetX Main Packet Pool",
                                PACKET_PAYLOAD, pointer, PACKET_POOL_SIZE);
                                pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        printf("Error with DHCP server packet pool create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server IP instance. */
    status = nx_ip_create(&server_ip, "NetX DHCP Server IP", NX_DHCP_SERVER_IP_ADDRESS,
                        0xFFFFFF00UL, &server_pool, nx_etherDriver_mcf5485, pointer,
                        SERVER_IP_THREAD_STACK, 1);

    pointer = pointer + DEMO_IP_THREAD_STACK;

    /* Check for IP create errors. */
    if (status)
    {
        printf("Error with DHCP server IP task create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server instance. */
    status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE,"DHCP Server", &server_pool);

    if (status)
    {
        printf("Error with DHCP server create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_SERVER_STACK_SIZE;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
    {
        printf("Error with ARP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable UDP traffic. */
    status = nx_udp_enable(&server_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable ICMP to enable the ping utility. */
    status = nx_icmp_enable(&server_ip);

    /* Check for errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
    }

    status = nx_dhcp_create_server_ip_address_list(&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);
    status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                        NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                        IP_ADDRESS(10,0,0,1));

    /* Start the DHCP Server. */
    status = nx_dhcp_server_start(&dhcp_server);

    tx_thread_resume(&test_thread);
}

/* Define the test thread. */
void     test_thread_entry(ULONG thread_input)
{

UINT     status;
UINT     keep_spinning;

    /* Just let the test thread be idle till we're ready to shut things down. */
    keep_spinning = 1;
    while(keep_spinning)
    {
        tx_thread_sleep(300);
    }

    printf("Stopping the server...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(500);

    printf("Starting the server...\n");
    status = nx_dhcp_server_start(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server start. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(600);

    printf("Stopping the server for good...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(200);

    printf("Deleting the server...\n");
    status = nx_dhcp_server_delete(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server delete. Status 0x%x\r\n", status);
        return;
    }
}
```

<span data-ttu-id="0b16c-197">Figura 1.1 Exemplo Aplicação do Servidor DHCP NetX</span><span class="sxs-lookup"><span data-stu-id="0b16c-197">Figure 1.1 Example NetX DHCP Server application</span></span>

## <a name="configuration-options"></a><span data-ttu-id="0b16c-198">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="0b16c-198">Configuration Options</span></span>

<span data-ttu-id="0b16c-199">Existem várias opções de configuração para a construção do NetX DHCP Server.</span><span class="sxs-lookup"><span data-stu-id="0b16c-199">There are several configuration options for building NetX DHCP Server.</span></span> <span data-ttu-id="0b16c-200">A seguinte lista descreve cada uma em detalhe:</span><span class="sxs-lookup"><span data-stu-id="0b16c-200">The following list describes each in detail:</span></span>  
  
- <span data-ttu-id="0b16c-201">**NX_DISABLE_ERROR_CHECKING**: Esta opção remove a verificação básica de erros dhcp.</span><span class="sxs-lookup"><span data-stu-id="0b16c-201">**NX_DISABLE_ERROR_CHECKING**: This option removes the basic DHCP error checking.</span></span> <span data-ttu-id="0b16c-202">É normalmente usado após a depurada aplicação.</span><span class="sxs-lookup"><span data-stu-id="0b16c-202">It is typically used after the application is debugged.</span></span>  
- <span data-ttu-id="0b16c-203">**NX_DHCP_SERVER_THREAD_PRIORITY**: Esta opção especifica a prioridade da linha do Servidor DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-203">**NX_DHCP_SERVER_THREAD_PRIORITY**: This option specifies the priority of the DHCP Server thread.</span></span> <span data-ttu-id="0b16c-204">Por predefinição, este valor especifica que o fio DHCP funciona na prioridade 2.</span><span class="sxs-lookup"><span data-stu-id="0b16c-204">By default, this value specifies that the DHCP thread runs at priority 2.</span></span>
- <span data-ttu-id="0b16c-205">**NX_DHCP_TYPE_OF_SERVICE**: Esta opção especifica o tipo de serviço necessário para os pedidos de UDP da DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-205">**NX_DHCP_TYPE_OF_SERVICE**: This option specifies the type of service required for the DHCP UDP requests.</span></span> <span data-ttu-id="0b16c-206">Por predefinição, este valor é definido como NX_IP_NORMAL para indicar o serviço normal de pacotes IP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-206">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="0b16c-207">**NX_DHCP_FRAGMENT_OPTION**: Ativar fragmentos para pedidos de UDP DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-207">**NX_DHCP_FRAGMENT_OPTION**: Fragment enable for DHCP UDP requests.</span></span> <span data-ttu-id="0b16c-208">Por padrão, este valor é definido para NX_DONT_FRAGMENT para desativar a fragmentação do UDP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-208">By default, this value is set to NX_DONT_FRAGMENT to disable UDP fragmenting.</span></span>
- <span data-ttu-id="0b16c-209">**NX_DHCP_TIME_TO_LIVE**: Especifica o número de routers que o pacote pode passar antes de ser descartado.</span><span class="sxs-lookup"><span data-stu-id="0b16c-209">**NX_DHCP_TIME_TO_LIVE**: Specifies the number of routers the packet can pass before it is discarded.</span></span> <span data-ttu-id="0b16c-210">O valor predefinido é 0x80.</span><span class="sxs-lookup"><span data-stu-id="0b16c-210">The default value is 0x80.</span></span>
- <span data-ttu-id="0b16c-211">**NX_DHCP_QUEUE_DEPTH** Especifica o número de pacotes que a tomada do Servidor DHCP mantém antes de descarregar a fila.</span><span class="sxs-lookup"><span data-stu-id="0b16c-211">**NX_DHCP_QUEUE_DEPTH** Specifies the number of packets that the DHCP Server socket keeps before flushing the queue.</span></span> <span data-ttu-id="0b16c-212">O valor predefinido é 5.</span><span class="sxs-lookup"><span data-stu-id="0b16c-212">The default value is 5.</span></span>
- <span data-ttu-id="0b16c-213">**NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: Especifica o tempo limite nos tiques de tempo para o Servidor DhCP NetX aguardar a atribuição de um pacote a partir da sua piscina de pacotes.</span><span class="sxs-lookup"><span data-stu-id="0b16c-213">**NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: Specifies the timeout in timer ticks for the NetX DHCP Server to wait for allocate a packet from its packet pool.</span></span> <span data-ttu-id="0b16c-214">O valor predefinido é definido para NX_IP_PERIODIC_RATE.</span><span class="sxs-lookup"><span data-stu-id="0b16c-214">The default value is set to NX_IP_PERIODIC_RATE.</span></span>
- <span data-ttu-id="0b16c-215">**NX_DHCP_SUBNET_MASK:** Esta é a máscara de sub-rede com a qual o Cliente DHCP deve ser configurado.</span><span class="sxs-lookup"><span data-stu-id="0b16c-215">**NX_DHCP_SUBNET_MASK**: This is the subnet mask the DHCP Client should be configured with.</span></span> <span data-ttu-id="0b16c-216">O valor predefinido é definido para 0xFFFFFF00.</span><span class="sxs-lookup"><span data-stu-id="0b16c-216">The default value is set to 0xFFFFFF00.</span></span>
- <span data-ttu-id="0b16c-217">**NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: Este é um período de tempo limite nos tiques temporizadores para o temporizador do Servidor DHCP para verificar o tempo restante da sessão e manusear sessões que tenham esgotado o tempo.</span><span class="sxs-lookup"><span data-stu-id="0b16c-217">**NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: This is timeout period in timer ticks for the DHCP Server fast timer to check on session time remaining and handle sessions that have timed out.</span></span>
- <span data-ttu-id="0b16c-218">**NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: Este é um período de tempo limite nos tiques temporizadores para o temporizador lento do Servidor DHCP para verificar o tempo de locação do endereço IP restante e lidar com o arrendamento que tenha esgotado o tempo.</span><span class="sxs-lookup"><span data-stu-id="0b16c-218">**NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: This is timeout period in timer ticks for the DHCP Server slow timer to check on IP address lease time remaining and handle lease that have timed out.</span></span>
- <span data-ttu-id="0b16c-219">**NX_DHCP_CLIENT_SESSION_TIMEOUT**: Este é um período de tempo limite no temporizador que o Servidor DHCP aguarda para receber a próxima mensagem do Cliente DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-219">**NX_DHCP_CLIENT_SESSION_TIMEOUT**: This is timeout period in timer ticks the DHCP Server will wait to receive the next DHCP Client message.</span></span>
- <span data-ttu-id="0b16c-220">**NX_DHCP_DEFAULT_LEASE_TIME**: Este é o tempo de locação ip address em segundos atribuídos ao Cliente DHCP, e a base para a computação dos tempos de renovação e reencadernação também atribuídos ao Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-220">**NX_DHCP_DEFAULT_LEASE_TIME**: This is IP Address lease time in seconds assigned to the DHCP Client, and the basis for computing the renewal and rebind times also assigned to the Client.</span></span> <span data-ttu-id="0b16c-221">O valor predefinido é definido para 0xFFFFFFFF (infinito).</span><span class="sxs-lookup"><span data-stu-id="0b16c-221">The default value is set to 0xFFFFFFFF (infinity).</span></span>
- <span data-ttu-id="0b16c-222">**NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: Este é o tamanho da matriz do Servidor DHCP para a posse de endereços IP disponíveis para a atribuição ao Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-222">**NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: This is size of the DHCP Server array for holding available IP addresses for assigning to the Client.</span></span> <span data-ttu-id="0b16c-223">O valor predefinido é de 20.</span><span class="sxs-lookup"><span data-stu-id="0b16c-223">The default value is 20.</span></span>
- <span data-ttu-id="0b16c-224">**NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: Este é o tamanho da matriz do Servidor DHCP para deter registos do Cliente.</span><span class="sxs-lookup"><span data-stu-id="0b16c-224">**NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: This is size of the DHCP Server array for holding Client records.</span></span> <span data-ttu-id="0b16c-225">O valor predefinido é de 50.</span><span class="sxs-lookup"><span data-stu-id="0b16c-225">The default value is 50.</span></span>
- <span data-ttu-id="0b16c-226">**NX_DHCP_CLIENT_OPTIONS_MAX**: Este é o tamanho da matriz na instância do Cliente DHCP para a realização de todas as opções solicitadas na lista de pedidos de parâmetros na sessão em curso.</span><span class="sxs-lookup"><span data-stu-id="0b16c-226">**NX_DHCP_CLIENT_OPTIONS_MAX**: This is size of the array in the DHCP Client instance for holding the all the requested options in the parameter request list in the current session.</span></span> <span data-ttu-id="0b16c-227">O valor predefinido é 12.</span><span class="sxs-lookup"><span data-stu-id="0b16c-227">The default value is 12.</span></span>
- <span data-ttu-id="0b16c-228">**NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: Este é o tampão que detém a lista padrão do Servidor DHCP de opções a fornecer ao cliente DHCP atual na lista de pedidos de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="0b16c-228">**NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: This is the buffer holding the DHCP Server's default list of options to supply to the current DHCP Client in the parameter request list.</span></span> <span data-ttu-id="0b16c-229">O padrão é "1 36".</span><span class="sxs-lookup"><span data-stu-id="0b16c-229">The default is "1 3 6."</span></span>
- <span data-ttu-id="0b16c-230">**NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: Este é o tamanho da matriz para manter a lista padrão de opções do Servidor DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-230">**NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: This is the size of the array to hold the DHCP Server's default list of options.</span></span> <span data-ttu-id="0b16c-231">O valor predefinido é 3.</span><span class="sxs-lookup"><span data-stu-id="0b16c-231">The default value is 3.</span></span>
- <span data-ttu-id="0b16c-232">**NX_DHCP_SERVER_HOSTNAME_MAX**: Este é o tamanho do tampão para segurar o nome do anfitrião do Servidor.</span><span class="sxs-lookup"><span data-stu-id="0b16c-232">**NX_DHCP_SERVER_HOSTNAME_MAX**: This is size of the buffer for holding the Server host name.</span></span> <span data-ttu-id="0b16c-233">O valor predefinido é 32.</span><span class="sxs-lookup"><span data-stu-id="0b16c-233">The default value is 32.</span></span>
- <span data-ttu-id="0b16c-234">**NX_DHCP_CLIENT_HOSTNAME_MAX**: Este é o tamanho do tampão para manter o nome de anfitrião do Cliente na sessão atual do Cliente do Servidor DHCP.</span><span class="sxs-lookup"><span data-stu-id="0b16c-234">**NX_DHCP_CLIENT_HOSTNAME_MAX**: This is size of the buffer for holding the Client host name in the current DHCP Server Client session.</span></span> <span data-ttu-id="0b16c-235">O valor predefinido é 32.</span><span class="sxs-lookup"><span data-stu-id="0b16c-235">The default value is 32.</span></span>