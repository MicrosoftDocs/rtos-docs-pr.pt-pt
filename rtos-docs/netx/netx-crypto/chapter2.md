---
title: Capítulo 2 - Instalação e utilização do Azure RTOS NetX Crypto
description: Este capítulo contém uma descrição de vários problemas relacionados com a instalação, configuração e utilização do componente NetX Crypto.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1616667c5efd73229ed69bcd4e5de5f80e5826f9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104826816"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-crypto"></a><span data-ttu-id="fb9e3-103">Capítulo 2 - Instalação e utilização do Azure RTOS NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="fb9e3-103">Chapter 2 - Installation and use of Azure RTOS NetX Crypto</span></span>

<span data-ttu-id="fb9e3-104">Este capítulo contém uma descrição de vários problemas relacionados com a instalação, configuração e utilização do componente Azure RTOS NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Crypto component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="fb9e3-105">Distribuição de Produtos</span><span class="sxs-lookup"><span data-stu-id="fb9e3-105">Product Distribution</span></span>

<span data-ttu-id="fb9e3-106">Azure RTOS NetX Crypto está disponível em [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="fb9e3-106">Azure RTOS NetX Crypto is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="fb9e3-107">O pacote inclui ficheiros de origem, inclui ficheiros e um ficheiro PDF que contém este documento, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="fb9e3-107">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="fb9e3-108">**nx_crypto.h**: Arquivo de cabeçalho API público NetX Crypto módulo</span><span class="sxs-lookup"><span data-stu-id="fb9e3-108">**nx_crypto.h**: Public API header file NetX Crypto module</span></span>
- <span data-ttu-id="fb9e3-109">**nx_crypto_\*.c/h:** Ficheiros C/H Source para NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="fb9e3-109">**nx_crypto_\*.c/h**: C/H Source files for NetX Crypto</span></span>
- <span data-ttu-id="fb9e3-110">**nx_crypto_port.h**: Ficheiro de cabeçalho C contendo todas as ferramentas de desenvolvimento e definições e estruturas específicas de dados específicas.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-110">**nx_crypto_port.h**: C header file containing all development-tool and target specific data definitions and structures.</span></span>
- <span data-ttu-id="fb9e3-111">**NetX_Crypto_User_Guide.pdf**: Descrição EM PDF do Módulo Crypto NetX.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-111">**NetX_Crypto_User_Guide.pdf**: PDF description of NetX Crypto Module.</span></span>

## <a name="netx-crypto-installation"></a><span data-ttu-id="fb9e3-112">Instalação NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="fb9e3-112">NetX Crypto Installation</span></span>

<span data-ttu-id="fb9e3-113">Toda a distribuição mencionada anteriormente está disponível no **diretório crypto_libraries,** presente ao nível raiz do repositório NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-113">The entire distribution mentioned previously is available in **crypto_libraries** directory, present at root level of NetX Duo repository.</span></span>

<span data-ttu-id="fb9e3-114">Para utilizar o NetX Crypto, toda a distribuição mencionada anteriormente deve ser copiada para o mesmo nível de diretório onde o NetX está instalado.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-114">In order to use NetX Crypto, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="fb9e3-115">Por exemplo, se o NetX estiver instalado no diretório "\threadx\arm7\NetX" então o nx_crypto *.*</span><span class="sxs-lookup"><span data-stu-id="fb9e3-115">For example, if NetX is installed in the directory "\threadx\arm7\NetX" then the nx_crypto *.*</span></span> <span data-ttu-id="fb9e3-116">os diretórios devem ser copiados em "\threadx\arm7\NetXCrypto".</span><span class="sxs-lookup"><span data-stu-id="fb9e3-116">directories should be copied into "\threadx\arm7\NetXCrypto".</span></span>

<span data-ttu-id="fb9e3-117">Para que o NetX Crypto seja utilizado em modo autónomo, toda a distribuição mencionada anteriormente deve ser copiada para o projeto de aplicação.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-117">For NetX Crypto to be used in standalone mode, the entire distribution mentioned previously should be copied to the application project.</span></span> <span data-ttu-id="fb9e3-118">Por **exemplo, crypto_libraries** diretório deve ser copiado para o projeto de candidatura ou para um projeto de biblioteca com **crypto_libraries** diretório deve ser criado e ligado ao projeto de candidatura.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-118">For example **crypto_libraries** directory should be copied to the application project or a library project with **crypto_libraries** directory should be created and linked to the application project.</span></span> 

## <a name="using-netx-crypto"></a><span data-ttu-id="fb9e3-119">Usando o NetX Crypto</span><span class="sxs-lookup"><span data-stu-id="fb9e3-119">Using NetX Crypto</span></span>

<span data-ttu-id="fb9e3-120">A utilização do NetX Crypto é fácil.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-120">Using NetX Crypto is easy.</span></span> <span data-ttu-id="fb9e3-121">Basicamente, o código de aplicação deve incluir o *nx_crypto.h*.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-121">Basically, the application code must include the *nx_crypto.h*.</span></span>  <span data-ttu-id="fb9e3-122">Uma vez *incluído nx_crypto.h,* o código de aplicação é então capaz de fazer as chamadas de função NetX Crypto especificadas mais tarde neste guia.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-122">Once *nx_crypto.h* is included, the application code is then able to make the NetX Crypto function calls specified later in this guide.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="fb9e3-123">Opções de configuração</span><span class="sxs-lookup"><span data-stu-id="fb9e3-123">Configuration Options</span></span>

<span data-ttu-id="fb9e3-124">Existem várias opções de configuração para a construção do NetX Crypto.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-124">There are several configuration options for building NetX Crypto.</span></span> <span data-ttu-id="fb9e3-125">Segue-se uma lista de todas as opções, onde cada uma é descrita em detalhe:</span><span class="sxs-lookup"><span data-stu-id="fb9e3-125">Following is a list of all options, where each is described in detail:</span></span>

- <span data-ttu-id="fb9e3-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Definida, esta opção dá o módulo RSA máximo esperado, em bits.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-126">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**: Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="fb9e3-127">O valor predefinido é de 4096 para um módulo de 4096 bits.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-127">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="fb9e3-128">Outros valores podem ser 3072, 2048 ou 1024 (não recomendado).</span><span class="sxs-lookup"><span data-stu-id="fb9e3-128">Other values can be 3072, 2048, or 1024 (not recommended).</span></span>
- <span data-ttu-id="fb9e3-129">**NX_CRYPTO_FIPS**: Definida, esta opção permite funcionalidades de segurança extra necessárias para FIPS-Compliant utilização.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-129">**NX_CRYPTO_FIPS**: Defined, this option enables extra security features required for FIPS-Compliant usage.</span></span> <span data-ttu-id="fb9e3-130">Esta opção não está ativada para a construção não-FIPS.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-130">This option is not enabled for non-FIPS build.</span></span>
- <span data-ttu-id="fb9e3-131">**NX_CRYPTO_STANDALONE_ENABLE**: Definido permite que o NetX Crypto seja utilizado em modo autónomo (sem Azure RTOS).</span><span class="sxs-lookup"><span data-stu-id="fb9e3-131">**NX_CRYPTO_STANDALONE_ENABLE**: Defined enables NetX Crypto to be used in standalone mode (without Azure RTOS).</span></span> <span data-ttu-id="fb9e3-132">Por padrão, este símbolo não está definido.</span><span class="sxs-lookup"><span data-stu-id="fb9e3-132">By default this symbol is not defined.</span></span>