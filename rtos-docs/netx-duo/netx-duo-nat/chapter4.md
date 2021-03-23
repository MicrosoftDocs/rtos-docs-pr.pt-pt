---
title: Capítulo 4 - Descrição dos serviços NAT
description: Este capítulo contém uma descrição de todos os serviços da API DA NETX Duo NAT por ordem alfabética.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8bdbdfcb2da6425fb99cadc7b2f6815dedc12953
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104825850"
---
# <a name="chapter-4---description-of-nat-services"></a><span data-ttu-id="2208f-103">Capítulo 4 - Descrição dos serviços NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-103">Chapter 4 - Description of NAT services</span></span>

<span data-ttu-id="2208f-104">Este capítulo contém uma descrição de todos os serviços da API DA NETX Duo NAT (listados abaixo) por ordem alfabética.</span><span class="sxs-lookup"><span data-stu-id="2208f-104">This chapter contains a description of all NetX Duo NAT API services (listed below) in alphabetical order.</span></span>

> [!NOTE]
> <span data-ttu-id="2208f-105">Na secção "Valores de Retorno" nas seguintes descrições da API, os valores em **BOLD** não são afetados pelo **NX_DISABLE_ERROR_CHECKING** definem que é utilizado para desativar a verificação de erros de API, enquanto os valores não arrojados são completamente desactivos.</span><span class="sxs-lookup"><span data-stu-id="2208f-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_nat_create"></a><span data-ttu-id="2208f-106">nx_nat_create</span><span class="sxs-lookup"><span data-stu-id="2208f-106">nx_nat_create</span></span>

<span data-ttu-id="2208f-107">Criar um servidor NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-107">Create a NAT Server</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-108">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-108">Prototype</span></span>

```C
UINT nx_nat_create(NX_NAT_DEVICE *nat_ptr, NX_IP *ip_ptr,
    UINT global_interface_index,
    VOID *dynamic_cache_memory,
    UINT dynamic_cache_size);
```

### <a name="description"></a><span data-ttu-id="2208f-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-109">Description</span></span>

<span data-ttu-id="2208f-110">Este serviço cria uma instância do servidor NAT.</span><span class="sxs-lookup"><span data-stu-id="2208f-110">This service creates an instance of the NAT server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-111">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-111">Input Parameters</span></span>

- <span data-ttu-id="2208f-112">**nat_ptr** Ponteiro para a instância NAT para criar</span><span class="sxs-lookup"><span data-stu-id="2208f-112">**nat_ptr** Pointer to NAT instance to create</span></span>
- <span data-ttu-id="2208f-113">**ip_ptr Pointer** para a instância IP</span><span class="sxs-lookup"><span data-stu-id="2208f-113">**ip_ptr Pointer** to IP instance</span></span>
- <span data-ttu-id="2208f-114">**global_interface_index** Índice para a interface global de rede</span><span class="sxs-lookup"><span data-stu-id="2208f-114">**global_interface_index** Index to the global network interface</span></span>
- <span data-ttu-id="2208f-115">**dynamic_cache_memory** Área de memória do ponteiro para a tabela NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-115">**dynamic_cache_memory** Pointer memory area to NAT table</span></span>
- <span data-ttu-id="2208f-116">**dynamic_cache_size** Tamanho da área de memória para tabela NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-116">**dynamic_cache_size** Size of memory area for NAT table</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-117">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-117">Return Values</span></span>

- <span data-ttu-id="2208f-118">**NX_SUCCESS** (0x00) servidor NAT criado com sucesso</span><span class="sxs-lookup"><span data-stu-id="2208f-118">**NX_SUCCESS** (0x00) NAT server successfully created</span></span>
- <span data-ttu-id="2208f-119">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-119">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="2208f-120">NX_NAT_PARAM_ERROR (0xD01) Entrada inválida sem ponteiro</span><span class="sxs-lookup"><span data-stu-id="2208f-120">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>
- <span data-ttu-id="2208f-121">NX_NAT_CACHE_ERROR (0xD02) Entrada inválida do ponteiro do cache</span><span class="sxs-lookup"><span data-stu-id="2208f-121">NX_NAT_CACHE_ERROR (0xD02) Invalid cache pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-122">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-122">Allowed From</span></span>

<span data-ttu-id="2208f-123">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-123">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-124">Example</span></span>

```C
#define NX_NAT_ENTRY_CACHE_SIZE 20480

static UCHAR nat_cache[NX_NAT_ENTRY_CACHE_SIZE];
UINT global_interface_index = 0;

/* Create a NAT Server and cache with a global interface index. */
status = nx_nat_create(nat_ptr, ip_ptr, global_interface_index,
    nat_cache, NX_NAT_ENTRY_CACHE_SIZE);

/* If status = NX_SUCCESS, the NAT instance was successfully
    created. */
```

## <a name="nx_nat_delete"></a><span data-ttu-id="2208f-125">nx_nat_delete</span><span class="sxs-lookup"><span data-stu-id="2208f-125">nx_nat_delete</span></span>

<span data-ttu-id="2208f-126">Excluir um servidor NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-126">Delete a NAT Server</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-127">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-127">Prototype</span></span>

```C
UINT nx_nat_delete(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="2208f-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-128">Description</span></span>

<span data-ttu-id="2208f-129">Este serviço elimina um SERVIDOR NAT previamente criado.</span><span class="sxs-lookup"><span data-stu-id="2208f-129">This service deletes a previously created NAT Server.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-130">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-130">Input Parameters</span></span>

- <span data-ttu-id="2208f-131">**nat_ptr** Ponteiro para a instância NAT para eliminar</span><span class="sxs-lookup"><span data-stu-id="2208f-131">**nat_ptr** Pointer to NAT instance to delete</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-132">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-132">Return Values</span></span>

- <span data-ttu-id="2208f-133">**NAT NX_SUCCESS** (0x00) eliminado com sucesso</span><span class="sxs-lookup"><span data-stu-id="2208f-133">**NX_SUCCESS** (0x00) NAT successfully deleted</span></span>
- <span data-ttu-id="2208f-134">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-134">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-135">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-135">Allowed From</span></span>

<span data-ttu-id="2208f-136">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-136">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-137">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-137">Example</span></span>

```C
/* Delete the NAT instance. */
status = nx_nat_delete (nat_ptr);

/* If the NAT instance was successfully deleted, status = NX_SUCCESS. */
```

## <a name="nx_nat_enable"></a><span data-ttu-id="2208f-138">nx_nat_enable</span><span class="sxs-lookup"><span data-stu-id="2208f-138">nx_nat_enable</span></span>

<span data-ttu-id="2208f-139">Ativar a instância IP para NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-139">Enable the IP instance for NAT</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-140">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-140">Prototype</span></span>

```C
UINT nx_nat_enable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="2208f-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-141">Description</span></span>

<span data-ttu-id="2208f-142">Este serviço permite a instância IP para NAT (por exemplo, pacotes recebidos para o servidor NAT).</span><span class="sxs-lookup"><span data-stu-id="2208f-142">This service enables the IP instance for NAT (e.g. forward received packets to the NAT server).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-143">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-143">Input Parameters</span></span>

- <span data-ttu-id="2208f-144">**nat_ptr** Ponteiro para a instância NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-144">**nat_ptr** Pointer to NAT instance</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-145">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-145">Return Values</span></span>

- <span data-ttu-id="2208f-146">**NAT NX_SUCCESS** (0x00) habilitado com sucesso</span><span class="sxs-lookup"><span data-stu-id="2208f-146">**NX_SUCCESS** (0x00) NAT successfully enabled</span></span>
- <span data-ttu-id="2208f-147">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-147">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-148">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-148">Allowed From</span></span>

<span data-ttu-id="2208f-149">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-149">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-150">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-150">Example</span></span>

```C
/* Enable the NAT server. */
status = nx_nat_enable (nat_ptr);

/* If status = NX_SUCCESS, the IP instance was successfully enabled for NAT. */
```

## <a name="nx_nat_disable"></a><span data-ttu-id="2208f-151">nx_nat_disable</span><span class="sxs-lookup"><span data-stu-id="2208f-151">nx_nat_disable</span></span>

<span data-ttu-id="2208f-152">Desative a instância IP para NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-152">Disable the IP instance for NAT</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-153">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-153">Prototype</span></span>

```C
UINT nx_nat_disable(NX_NAT_DEVICE *nat_ptr);
```

### <a name="description"></a><span data-ttu-id="2208f-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-154">Description</span></span>

<span data-ttu-id="2208f-155">Este serviço desativa o NAT na instância IP.</span><span class="sxs-lookup"><span data-stu-id="2208f-155">This service disables NAT on the IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-156">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-156">Input Parameters</span></span>

- <span data-ttu-id="2208f-157">**nat_ptr** Ponteiro para a instância NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-157">**nat_ptr** Pointer to NAT instance</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-158">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-158">Return Values</span></span>

- <span data-ttu-id="2208f-159">**NX_SUCCESS** (0x00) NAT com sucesso desativado</span><span class="sxs-lookup"><span data-stu-id="2208f-159">**NX_SUCCESS** (0x00) NAT successfully disabled</span></span>
- <span data-ttu-id="2208f-160">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-160">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-161">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-161">Allowed From</span></span>

<span data-ttu-id="2208f-162">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-162">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-163">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-163">Example</span></span>

```C
/* Disable the NAT server. */
status = nx_nat_disable (nat_ptr);

/* If status = NX_SUCCESS the NAT operation successfully disable. */
```

## <a name="nx_nat_cache_notify_set"></a><span data-ttu-id="2208f-164">nx_nat_cache_notify_set</span><span class="sxs-lookup"><span data-stu-id="2208f-164">nx_nat_cache_notify_set</span></span>

<span data-ttu-id="2208f-165">Desa um cache completa notifique a função de retorno de chamada</span><span class="sxs-lookup"><span data-stu-id="2208f-165">Set a cache full notify callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-166">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-166">Prototype</span></span>

```C
UINT nx_nat_cache_notify_set(NX_NAT_DEVICE *nat_ptr,
    VOID (*cache_full_notify_cb)
    (NX_NAT_DEVICE *nat_ptr)));
```

### <a name="description"></a><span data-ttu-id="2208f-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-167">Description</span></span>

<span data-ttu-id="2208f-168">Este serviço regista a chamada completa da cache com o ponteiro da função de entrada cache_full_notify_cb que aponta para uma função de notificação completa de cache definida pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="2208f-168">This service registers the cache full callback with the input function pointer cache_full_notify_cb which points to a user defined cache full notify function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-169">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-169">Input Parameters</span></span>

- <span data-ttu-id="2208f-170">**nat_ptr** Ponteiro para a instância NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-170">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="2208f-171">**cache_full_notify_cb** Ponteiro para cache função de notificação completa</span><span class="sxs-lookup"><span data-stu-id="2208f-171">**cache_full_notify_cb** Pointer to cache full notify function</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-172">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-172">Return Values</span></span>

- <span data-ttu-id="2208f-173">**NX_SUCCESS** (0x00) Cache funciona completamente definida com sucesso</span><span class="sxs-lookup"><span data-stu-id="2208f-173">**NX_SUCCESS** (0x00) Cache full notify function successfully set</span></span>
- <span data-ttu-id="2208f-174">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-174">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="2208f-175">NX_NAT_PARAM_ERROR (0xD01) Entrada inválida sem ponteiro</span><span class="sxs-lookup"><span data-stu-id="2208f-175">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-176">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-176">Allowed From</span></span>

<span data-ttu-id="2208f-177">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-177">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-178">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-178">Example</span></span>

```C
/* Set the cache full notify callback function to the NAT instance. */
status = nx_nat_cache_notify_set(nat_ptr, cache_full_notify_cb);

/* If status = NX_SUCCESS the callback function was successfully set. */
```

## <a name="nx_nat_inbound_entry_create"></a><span data-ttu-id="2208f-179">nx_nat_inbound_entry_create</span><span class="sxs-lookup"><span data-stu-id="2208f-179">nx_nat_inbound_entry_create</span></span>

<span data-ttu-id="2208f-180">Criar uma entrada de entrada na tabela de tradução NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-180">Create an inbound entry in the NAT translation table</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-181">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-181">Prototype</span></span>

```C
UINT nx_nat_inbound_entry_create(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *entry_ptr
    ULONG local_ip_address,
    USHORT external_port,
    USHORT local_port, UCHAR protocol);
```

### <a name="description"></a><span data-ttu-id="2208f-182">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-182">Description</span></span>

<span data-ttu-id="2208f-183">Este serviço cria uma entrada de entrada como estática (entrada permanente, nunca expira) e adiciona-a à tabela de tradução NAT.</span><span class="sxs-lookup"><span data-stu-id="2208f-183">This service creates an inbound entry as static (permanent entry, never expires) and adds it to the NAT translation table.</span></span> <span data-ttu-id="2208f-184">Estas entradas são geralmente criadas para servidores anfitriões locais onde uma ligação é iniciada a partir de um anfitrião na rede externa.</span><span class="sxs-lookup"><span data-stu-id="2208f-184">These entries are usually created for local host servers where a connection is initiated from a host on the outside network.</span></span> <span data-ttu-id="2208f-185">O servidor NAT verifica se a porta externa ainda não está a ser utilizada na tabela de tradução ou vinculada por uma tomada NetX Duo anteriormente existente do mesmo protocolo.</span><span class="sxs-lookup"><span data-stu-id="2208f-185">The NAT server checks that the external port is not already in use in the translation table or bound by a previously existing NetX Duo socket of the same protocol.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-186">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-186">Input Parameters</span></span>

- <span data-ttu-id="2208f-187">**nat_ptr** Ponteiro para a instância NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-187">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="2208f-188">**entry_ptr** Ponteiro para a entrada de tradução</span><span class="sxs-lookup"><span data-stu-id="2208f-188">**entry_ptr** Pointer to translation entry</span></span>
- <span data-ttu-id="2208f-189">**local_ip_address** Endereço IP do anfitrião local</span><span class="sxs-lookup"><span data-stu-id="2208f-189">**local_ip_address** Local host IP address</span></span>
- <span data-ttu-id="2208f-190">**external_port** Porta de destino na rede externa</span><span class="sxs-lookup"><span data-stu-id="2208f-190">**external_port** Destination port on the external network</span></span>
- <span data-ttu-id="2208f-191">**local_port** Porto de origem (anfitrião local)</span><span class="sxs-lookup"><span data-stu-id="2208f-191">**local_port** Source (local host) port</span></span>
- <span data-ttu-id="2208f-192">**protocolo** Protocolo do pacote (por exemplo, TCP)</span><span class="sxs-lookup"><span data-stu-id="2208f-192">**protocol** Packet protocol (e.g TCP)</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-193">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-193">Return Values</span></span>

- <span data-ttu-id="2208f-194">**NX_SUCCESS** (0x00) Entrada criada com sucesso</span><span class="sxs-lookup"><span data-stu-id="2208f-194">**NX_SUCCESS** (0x00) Entry successfully created</span></span>
- <span data-ttu-id="2208f-195">**porta** externa NX_NAT_PORT_UNAVAILABLE (0xD0D) Inválida</span><span class="sxs-lookup"><span data-stu-id="2208f-195">**NX_NAT_PORT_UNAVAILABLE** (0xD0D) Invalid external port</span></span>
- <span data-ttu-id="2208f-196">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-196">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="2208f-197">NX_NAT_PARAM_ERROR (0xD01) Entrada inválida sem ponteiro</span><span class="sxs-lookup"><span data-stu-id="2208f-197">NX_NAT_PARAM_ERROR (0xD01) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-198">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-198">Allowed From</span></span>

<span data-ttu-id="2208f-199">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-199">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-200">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-200">Example</span></span>

```C
/* Create an entry for an inbound TCP packet. */
status = nx_nat_inbound_entry_create(nat_ptr, entry_ptr,
    IP_ADDRESS(192,168,2,2), 5001, 5001,
    NX_PROTOCOL_TCP);

/* If status = NX_SUCCESS the entry was successfully created. */
```

## <a name="nx_nat_inbound_entry_delete"></a><span data-ttu-id="2208f-201">nx_nat_inbound_entry_delete</span><span class="sxs-lookup"><span data-stu-id="2208f-201">nx_nat_inbound_entry_delete</span></span>

<span data-ttu-id="2208f-202">Eliminar uma entrada de entrada na tabela de tradução NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-202">Delete an inbound entry in the NAT translation table</span></span>

### <a name="prototype"></a><span data-ttu-id="2208f-203">Prototype</span><span class="sxs-lookup"><span data-stu-id="2208f-203">Prototype</span></span>

```C
UINT nx_nat_inbound_entry_delete(NX_NAT_DEVICE *nat_ptr,
    NX_NAT_TRANSLATION_ENTRY *delete_entry_ptr)
```

### <a name="description"></a><span data-ttu-id="2208f-204">Descrição</span><span class="sxs-lookup"><span data-stu-id="2208f-204">Description</span></span>

<span data-ttu-id="2208f-205">Este serviço elimina a entrada especificada da tabela de tradução.</span><span class="sxs-lookup"><span data-stu-id="2208f-205">This service deletes the specified inbound entry from the translation table.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2208f-206">Parâmetros de Entrada</span><span class="sxs-lookup"><span data-stu-id="2208f-206">Input Parameters</span></span>

- <span data-ttu-id="2208f-207">**nat_ptr** Ponteiro para a instância NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-207">**nat_ptr** Pointer to NAT instance</span></span>
- <span data-ttu-id="2208f-208">**delete_entry_ptr** Ponteiro para a entrada de tradução NAT</span><span class="sxs-lookup"><span data-stu-id="2208f-208">**delete_entry_ptr** Pointer to the NAT translation entry</span></span>

### <a name="return-values"></a><span data-ttu-id="2208f-209">Valores de devolução</span><span class="sxs-lookup"><span data-stu-id="2208f-209">Return Values</span></span>

- <span data-ttu-id="2208f-210">**NX_SUCCESS** (0x00) Entrada eliminada com sucesso</span><span class="sxs-lookup"><span data-stu-id="2208f-210">**NX_SUCCESS** (0x00) Entry successfully deleted</span></span>
- <span data-ttu-id="2208f-211">**NX_NAT_ENTRY_NOT_FOUND** (0xD04) A entrada não é encontrada</span><span class="sxs-lookup"><span data-stu-id="2208f-211">**NX_NAT_ENTRY_NOT_FOUND** (0xD04) Entry does not found</span></span>
- <span data-ttu-id="2208f-212">NX_PTR_ERROR (0x07) Parâmetro de ponteiro de entrada inválido</span><span class="sxs-lookup"><span data-stu-id="2208f-212">NX_PTR_ERROR (0x07) Invalid input pointer parameter</span></span>
- <span data-ttu-id="2208f-213">NX_NAT_ENTRY_TYPE_ERROR (0xD0C) Tipo de tradução inválida</span><span class="sxs-lookup"><span data-stu-id="2208f-213">NX_NAT_ENTRY_TYPE_ERROR (0xD0C) Invalid translation type</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2208f-214">Permitido a partir de</span><span class="sxs-lookup"><span data-stu-id="2208f-214">Allowed From</span></span>

<span data-ttu-id="2208f-215">Código de aplicação</span><span class="sxs-lookup"><span data-stu-id="2208f-215">Application code</span></span>

### <a name="example"></a><span data-ttu-id="2208f-216">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2208f-216">Example</span></span>

```C
/* Delete the specified static entry from the translation table. */
status = nx_nat_inbound_entry_delete(nat_ptr, delete_entry_ptr);

/* If status = NX_SUCCESS the entry was successfully deleted. */
```
