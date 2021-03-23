---
title: Capítulo 2 - Instalação e utilização do Azure RTOS NetX AutoIP
description: Este capítulo contém uma descrição de vários problemas relacionados com a instalação, configuração e utilização do componente Azure RTOS NetX AutoIP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 269a3b4e9754fdc19e2cf1482d483fad2b841de9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825610"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-autoip"></a><span data-ttu-id="7a895-103">Capítulo 2 - Instalação e utilização do Azure RTOS NetX AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-103">Chapter 2 - Installation and use of Azure RTOS NetX AutoIP</span></span>

<span data-ttu-id="7a895-104">Este capítulo contém uma descrição de vários problemas relacionados com a instalação, configuração e utilização do componente Azure RTOS NetX AutoIP.</span><span class="sxs-lookup"><span data-stu-id="7a895-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX AutoIP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="7a895-105">Distribuição de Produtos</span><span class="sxs-lookup"><span data-stu-id="7a895-105">Product Distribution</span></span>

<span data-ttu-id="7a895-106">O AutoIP para NetX está disponível em [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="7a895-106">AutoIP for NetX is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="7a895-107">O pacote inclui três ficheiros de origem, um inclui ficheiros e um ficheiro PDF que contém este documento, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7a895-107">The package includes three source files, one include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="7a895-108">**nx_auto_ip.h**: Ficheiro de cabeçalho para NetX AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-108">**nx_auto_ip.h**: Header file for NetX AutoIP</span></span>
- <span data-ttu-id="7a895-109">**nx_auto_ip.c**: Ficheiro C Fonte para NetX AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-109">**nx_auto_ip.c**: C Source file for NetX AutoIP</span></span>
- <span data-ttu-id="7a895-110">**demo_netx_auto_ip.c**: Ficheiro C Fonte para demonstração de NetX AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-110">**demo_netx_auto_ip.c**: C Source file for NetX AutoIP Demo</span></span>
- <span data-ttu-id="7a895-111">**nx_auto_ip.pdf**: Descrição em PDF do NetX AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-111">**nx_auto_ip.pdf**: PDF description of NetX AutoIP</span></span>

## <a name="autoip-installation"></a><span data-ttu-id="7a895-112">Instalação AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-112">AutoIP Installation</span></span>

<span data-ttu-id="7a895-113">Para utilizar o NetX AutoIP, toda a distribuição mencionada anteriormente deve ser copiada para o mesmo diretório onde o NetX está instalado.</span><span class="sxs-lookup"><span data-stu-id="7a895-113">In order to use NetX AutoIP, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="7a895-114">Por exemplo, se o NetX for instalado no diretório "*\threadx\arm7\green*" então o *nx_auto_ip.h*, *nx_auto_ip.c*, e *demo_netx_auto_ip.c* ficheiros devem ser copiados para este diretório.</span><span class="sxs-lookup"><span data-stu-id="7a895-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_auto_ip.h*, *nx_auto_ip.c*, and *demo_netx_auto_ip.c* files should be copied into this directory.</span></span>

## <a name="using-autoip"></a><span data-ttu-id="7a895-115">Utilização de AutoIP</span><span class="sxs-lookup"><span data-stu-id="7a895-115">Using AutoIP</span></span>

<span data-ttu-id="7a895-116">A utilização do NetX AutoIP é fácil.</span><span class="sxs-lookup"><span data-stu-id="7a895-116">Using NetX AutoIP is easy.</span></span> <span data-ttu-id="7a895-117">Basicamente, o código de aplicação deve incluir *nx_auto_ip.h* depois de incluir *tx_api.h* e *nx_api.h,* para utilizar o ThreadX e o NetX.</span><span class="sxs-lookup"><span data-stu-id="7a895-117">Basically, the application code must include *nx_auto_ip.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="7a895-118">Uma vez incluído *nx_auto_ip.h,* o código de aplicação é então capaz de fazer as chamadas de função AutoIP especificadas mais tarde neste guia.</span><span class="sxs-lookup"><span data-stu-id="7a895-118">Once *nx_auto_ip.h* is included, the application code is then able to make the AutoIP function calls specified later in this guide.</span></span> <span data-ttu-id="7a895-119">O pedido também deve incluir *nx_auto_ip.c* no processo de construção.</span><span class="sxs-lookup"><span data-stu-id="7a895-119">The application must also include *nx_auto_ip.c* in the build process.</span></span> <span data-ttu-id="7a895-120">Estes ficheiros devem ser compilados da mesma forma que outros ficheiros de aplicações e a sua forma de objeto deve ser ligada juntamente com os ficheiros da aplicação.</span><span class="sxs-lookup"><span data-stu-id="7a895-120">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="7a895-121">Isto é tudo o que é necessário para usar o NetX AutoIP.</span><span class="sxs-lookup"><span data-stu-id="7a895-121">This is all that is required to use NetX AutoIP.</span></span>

> [!NOTE]
> <span data-ttu-id="7a895-122">Uma vez que o AutoIP utiliza os serviços ARP netx, o ARP deve ser ativado com a chamada *nx_arp_enable* antes de utilizar o AutoIP.</span><span class="sxs-lookup"><span data-stu-id="7a895-122">Since AutoIP utilizes NetX ARP services, ARP must be enabled with the *nx_arp_enable* call prior to using AutoIP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="7a895-123">Sistema de Pequenos Exemplos</span><span class="sxs-lookup"><span data-stu-id="7a895-123">Small Example System</span></span>

<span data-ttu-id="7a895-124">Um exemplo de como é fácil utilizar o NetX AutoIP é descrito na Figura 1.1, que aparece abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a895-124">An example of how easy it is to use NetX AutoIP is described in Figure 1.1, which appears below.</span></span> <span data-ttu-id="7a895-125">Neste exemplo, o AutoIP inclui ficheiro *nx_auto_ip.h* é trazido na linha 002.</span><span class="sxs-lookup"><span data-stu-id="7a895-125">In this example, the AutoIP include file *nx_auto_ip.h* is brought in at line 002.</span></span> <span data-ttu-id="7a895-126">Em seguida, a instância NetX AutoIP é criada em "*tx_application_define*" na linha 090.</span><span class="sxs-lookup"><span data-stu-id="7a895-126">Next, the NetX AutoIP instance is created in "*tx_application_define*" at line 090.</span></span> <span data-ttu-id="7a895-127">Note que o bloco de controlo NetX AutoIP "auto_ip_0" foi definido anteriormente como uma variável global na linha 015.</span><span class="sxs-lookup"><span data-stu-id="7a895-127">Note that the NetX AutoIP control block "auto_ip_0" was defined previously as a global variable at line 015.</span></span> <span data-ttu-id="7a895-128">Após a criação bem sucedida, um NetX AutoIP é iniciado na linha 098.</span><span class="sxs-lookup"><span data-stu-id="7a895-128">After successful creation, an NetX AutoIP is started at line 098.</span></span> <span data-ttu-id="7a895-129">O processamento da função de retorno de alteração de endereço IP começa na linha 105, que é usada para lidar com conflitos subsequentes ou possível resolução de endereços DHCP.</span><span class="sxs-lookup"><span data-stu-id="7a895-129">The IP address change callback function processing starts at line 105, which is used to handle subsequent conflicts or possible DHCP address resolution.</span></span>

> [!NOTE]
> <span data-ttu-id="7a895-130">O exemplo abaixo pressupõe que o dispositivo hospedeiro é um dispositivo de uma única casa.</span><span class="sxs-lookup"><span data-stu-id="7a895-130">The example below assumes the host device is a single-homed device.</span></span> <span data-ttu-id="7a895-131">Para um dispositivo multihomed, a aplicação de anfitrião pode utilizar o serviço NetX AutoIP *nx_auto_ip_interface_* definido para especificar uma interface de rede secundária para sondar para um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="7a895-131">For a multihomed device, the host application can use the NetX AutoIP service *nx_auto_ip_interface_* set to specify a secondary network interface to probe for an IP address.</span></span> <span data-ttu-id="7a895-132">Consulte o Guia do **Utilizador NetX** para obter mais detalhes sobre a configuração de aplicações multihomed.</span><span class="sxs-lookup"><span data-stu-id="7a895-132">See the **NetX User Guide** for more details on setting up multihomed applications.</span></span> <span data-ttu-id="7a895-133">Note ainda que a aplicação de anfitrião deve utilizar o *nx_status_ip_interface_check* netx API para verificar se o AutoIP obteve um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="7a895-133">Note further that the host application should use the NetX API *nx_status_ip_interface_check* to verify AutoIP has obtained an IP address.</span></span>

## <a name="example-of-autoip-use-with-netx"></a><span data-ttu-id="7a895-134">Exemplo de utilização automática com NetX</span><span class="sxs-lookup"><span data-stu-id="7a895-134">Example of AutoIP use with NetX</span></span>

```c
000 #include "tx_api.h"
001 #include "nx_api.h"
002 #include "nx_auto_ip.h"
003
004 #define         DEMO_STACK_SIZE         4096
005
006 /* Define the ThreadX and NetX object control blocks... */
007
008 TX_THREAD         thread_0;
009 NX_PACKET_POOL    pool_0;
010 NX_IP             ip_0;
011
012
013 /* Define the AUTO IP structures for the IP instance. */
014
015 NX_AUTO_IP         auto_ip_0;
016
017
018 /* Define the counters used in the demo application... */
019
020 ULONG             thread_0_counter;
021 ULONG             address_changes;
022 ULONG             error_counter;
023
024
025 /* Define thread prototypes. */
026
027 void     thread_0_entry(ULONG thread_input);
028 void     ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address);
029 void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
030
031
032 /* Define main entry point. */
033
034 int main()
035 {
036
037     /* Enter the ThreadX kernel. */
038     tx_kernel_enter();
039 }
040
041
042 /* Define what the initial system looks like. */
043
044 void     tx_application_define(void *first_unused_memory)
045 {
046
047 CHAR     *pointer;
048 UINT     status;
049
050
051     /* Setup the working pointer. */
052     pointer = (CHAR *) first_unused_memory;
053
054     /* Create the main thread. */
055     tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
056                     pointer, DEMO_STACK_SIZE,
057                     16, 16, 1, TX_AUTO_START);
058
059     pointer = pointer + DEMO_STACK_SIZE;
060
061     /* Initialize the NetX system. */
062     nx_system_initialize();
063
064     /* Create a packet pool. */
065     status = nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 128,
066                                     pointer, 4096);
067                                     pointer = pointer + 4096;
068
069     if (status)
070         error_counter++;
071
072     /* Create an IP instance. */
073     status = nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(0, 0, 0, 0),
074                             0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
075                             pointer, 4096, 1);
076                             pointer = pointer + 4096;
077
078     if (status)
079         error_counter++;
080
081     /* Enable ARP and supply ARP cache memory for IP Instance 0. */
082     status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
083     pointer = pointer + 1024;
084
085     /* Check ARP enable status. */
086     if (status)
087         error_counter++;
088
089     /* Create the AutoIP instance for IP Instance 0. */
090     status = nx_auto_ip_create(&auto_ip_0, "AutoIP 0", &ip_0, pointer, 4096, 1);
091     pointer = pointer + 4096;
092
093     /* Check AutoIP create status. */
094     if (status)
095         error_counter++;
096
097     /* Start AutoIP instances. */
098     status = nx_auto_ip_start(&auto_ip_0, 0 /*IP_ADDRESS(169,254,254,255)*/);
099
100     /* Check AutoIP start status. */
101     if (status)
102         error_counter++;
103
104     /* Register an IP address change function for IP Instance 0. */
105     status = nx_ip_address_change_notify(&ip_0, ip_address_changed,
106                                         (void *) &auto_ip_0);
107
108     /* Check IP address change notify status. */
109     if (status)
110         error_counter++;
111     }
112
113
114     /* Define the test thread. */
115
116     void thread_0_entry(ULONG thread_input)
117     {
118
119     UINT      status;
120     ULONG     actual_status;
121
122
123          /* Wait for IP address to be resolved. */
124         do
125         {
126
127             /* Call IP status check routine. */
128             status = nx_ip_status_check(&ip_0, NX_IP_ADDRESS_RESOLVED,
129                                         &actual_status, 10000);
130
131         } while (status != NX_SUCCESS);
132
133         /* Since the IP address is resolved at this point, the application
134         can now fully utilize NetX! */
135
136         while(1)
137         {
138
139
140
141             /* Increment thread 0's counter. */
142             thread_0_counter++;
143
144             /* Sleep... */
145             tx_thread_sleep(10);
146         }
147     }
148
149
150     void ip_address_changed(NX_IP *ip_ptr, VOID *auto_ip_address)
151     {
152
153     ULONG         ip_address;
154     ULONG         network_mask;
155     NX_AUTO_IP    *auto_ip_ptr;
156
157
158     /* Setup pointer to auto IP instance. */
159     auto_ip_ptr = (NX_AUTO_IP *) auto_ip_address;
160
161     /* Pickup the current IP address. */
162     nx_ip_address_get(ip_ptr, &ip_address, &network_mask);
163
164     /* Determine if the IP address has changed back to zero. If so,
165     make sure the AutoIP instance is started. */
166     if (ip_address == 0)
167     {
168
169         /* Get the last AutoIP address for this node. */
170         nx_auto_ip_get_address(auto_ip_ptr, &ip_address);
171
172         /* Start this AutoIP instance. */
173         nx_auto_ip_start(auto_ip_ptr, ip_address);
174     }
175
176     /* Determine if IP address has transitioned to a non local IP address. */
177     else if ((ip_address & 0xFFFF0000UL) != IP_ADDRESS(169, 254, 0, 0))
178     {
179
180         /* Stop the AutoIP processing. */
181         nx_auto_ip_stop(auto_ip_ptr);
182     }
183
184     /* Increment a counter. */
185     address_changes++;
186 }
```

## <a name="configuration-options"></a><span data-ttu-id="7a895-135">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="7a895-135">Configuration Options</span></span>

<span data-ttu-id="7a895-136">Existem várias opções de configuração para a construção do NetX AutoIP.</span><span class="sxs-lookup"><span data-stu-id="7a895-136">There are several configuration options for building NetX AutoIP.</span></span> <span data-ttu-id="7a895-137">Segue-se uma lista de todas as opções, onde cada uma é descrita em detalhe:</span><span class="sxs-lookup"><span data-stu-id="7a895-137">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="7a895-138">**NX_DISABLE_ERROR_CHECKING**: Definida, esta opção remove a verificação básica de erros autoIP.</span><span class="sxs-lookup"><span data-stu-id="7a895-138">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic AutoIP error checking.</span></span> <span data-ttu-id="7a895-139">É normalmente usado após a depurada aplicação.</span><span class="sxs-lookup"><span data-stu-id="7a895-139">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="7a895-140">**NX_AUTO_IP_PROBE_WAIT**: O número de segundos a esperar antes de enviar a primeira sonda.</span><span class="sxs-lookup"><span data-stu-id="7a895-140">**NX_AUTO_IP_PROBE_WAIT**: The number of seconds to wait before sending first probe.</span></span> <span data-ttu-id="7a895-141">Por predefinição, este valor é definido como 1.</span><span class="sxs-lookup"><span data-stu-id="7a895-141">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="7a895-142">**NX_AUTO_IP_PROBE_NUM**: O número de sondas ARP a enviar.</span><span class="sxs-lookup"><span data-stu-id="7a895-142">**NX_AUTO_IP_PROBE_NUM**: The number of ARP probes to send.</span></span> <span data-ttu-id="7a895-143">Por predefinição, este valor é definido como 3.</span><span class="sxs-lookup"><span data-stu-id="7a895-143">By default, this value is defined as 3.</span></span>
- <span data-ttu-id="7a895-144">**NX_AUTO_IP_PROBE_MIN**: O número mínimo de segundos para esperar entre o envio de sondas.</span><span class="sxs-lookup"><span data-stu-id="7a895-144">**NX_AUTO_IP_PROBE_MIN**: The minimum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="7a895-145">Por predefinição, este valor é definido como 1.</span><span class="sxs-lookup"><span data-stu-id="7a895-145">By default, this value is defined as 1.</span></span>
- <span data-ttu-id="7a895-146">**NX_AUTO_IP_PROBE_MAX**: O número máximo de segundos para esperar entre o envio de sondas.</span><span class="sxs-lookup"><span data-stu-id="7a895-146">**NX_AUTO_IP_PROBE_MAX**: The maximum number of seconds to wait between sending probes.</span></span> <span data-ttu-id="7a895-147">Por predefinição, este valor é definido como 2.</span><span class="sxs-lookup"><span data-stu-id="7a895-147">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="7a895-148">**NX_AUTO_IP_MAX_CONFLICTS**: O número de conflitos autoip antes de aumentar os atrasos de processamento.</span><span class="sxs-lookup"><span data-stu-id="7a895-148">**NX_AUTO_IP_MAX_CONFLICTS**: The number of AutoIP conflicts before increasing processing delays.</span></span> <span data-ttu-id="7a895-149">Por predefinição, este valor é definido como 10.</span><span class="sxs-lookup"><span data-stu-id="7a895-149">By default, this value is defined as 10.</span></span>
- <span data-ttu-id="7a895-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: O número de segundos para prolongar o período de espera quando o número total de conflitos for ultrapassado.</span><span class="sxs-lookup"><span data-stu-id="7a895-150">**NX_AUTO_IP_RATE_LIMIT_INTERVAL**: The number of seconds to extend the wait period when the total number of conflicts is exceeded.</span></span> <span data-ttu-id="7a895-151">Por predefinição, este valor é definido como 60.</span><span class="sxs-lookup"><span data-stu-id="7a895-151">By default, this value is defined as 60.</span></span>
- <span data-ttu-id="7a895-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: O número de segundos a esperar antes de enviar o anúncio.</span><span class="sxs-lookup"><span data-stu-id="7a895-152">**NX_AUTO_IP_ANNOUNCE_WAIT**: The number of seconds to wait before sending announcement.</span></span> <span data-ttu-id="7a895-153">Por predefinição, este valor é definido como 2.</span><span class="sxs-lookup"><span data-stu-id="7a895-153">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="7a895-154">**NX_AUTO_IP_ANNOUNCE_NUM**: O número de ARP anuncia enviar.</span><span class="sxs-lookup"><span data-stu-id="7a895-154">**NX_AUTO_IP_ANNOUNCE_NUM**: The number of ARP announces to send.</span></span> <span data-ttu-id="7a895-155">Por predefinição, este valor é definido como 2.</span><span class="sxs-lookup"><span data-stu-id="7a895-155">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="7a895-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: O número de segundos a esperar entre o envio de anúncios.</span><span class="sxs-lookup"><span data-stu-id="7a895-156">**NX_AUTO_IP_ANNOUNCE_INTERVAL**: The number of seconds to wait between sending announces.</span></span> <span data-ttu-id="7a895-157">Por predefinição, este valor é definido como 2.</span><span class="sxs-lookup"><span data-stu-id="7a895-157">By default, this value is defined as 2.</span></span>
- <span data-ttu-id="7a895-158">**NX_AUTO_IP_DEFEND_INTERVAL:** O número de segundos a esperar entre a defesa anuncia.</span><span class="sxs-lookup"><span data-stu-id="7a895-158">**NX_AUTO_IP_DEFEND_INTERVAL**: The number of seconds to wait between defense announces.</span></span> <span data-ttu-id="7a895-159">Por predefinição, este valor é definido como 10.</span><span class="sxs-lookup"><span data-stu-id="7a895-159">By default, this value is defined as 10.</span></span>