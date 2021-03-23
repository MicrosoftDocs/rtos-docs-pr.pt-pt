---
title: Guia de utilizadores do estúdio Azure RTOS GUIX
description: Este guia fornece informações completas sobre o Azure RTOS GUIX Studio, o ambiente de desenvolvimento rápido de UI baseado no Microsoft, especificamente concebido para a biblioteca de tempo de execução Azure RTOS GUIX da Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 4be5049fca40d6d57961e692661d8df6706eac28
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827295"
---
# <a name="about-this-guix-studio-user-guide"></a><span data-ttu-id="9882a-103">Sobre este guix Studio User Guide</span><span class="sxs-lookup"><span data-stu-id="9882a-103">About This GUIX Studio User Guide</span></span>

<span data-ttu-id="9882a-104">Este guia fornece informações completas sobre o Azure RTOS GUIX Studio, o ambiente de desenvolvimento rápido de UI baseado no Microsoft, especificamente concebido para a biblioteca de tempo de execução Azure RTOS GUIX da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9882a-104">This guide provides comprehensive information about Azure RTOS GUIX Studio, the Microsoft Windows-based rapid UI development environment specifically designed for the Azure RTOS GUIX runtime library from Microsoft.</span></span> 

<span data-ttu-id="9882a-105">Destina-se ao desenvolvedor de software incorporado em tempo real utilizando o Sistema Operativo Real-Time ThreadX (RTOS) e a biblioteca de tempo de execução Azure RTOS GUIX UI.</span><span class="sxs-lookup"><span data-stu-id="9882a-105">It is intended for the embedded real-time software developer using the ThreadX Real-Time Operating System (RTOS) and the Azure RTOS GUIX UI run-time library.</span></span> <span data-ttu-id="9882a-106">O desenvolvedor deve estar familiarizado com os conceitos standard Azure RTOS ThreadX e Azure RTOS GUIX.</span><span class="sxs-lookup"><span data-stu-id="9882a-106">The developer should be familiar with standard Azure RTOS ThreadX and Azure RTOS GUIX concepts.</span></span>

## <a name="organization"></a><span data-ttu-id="9882a-107">Organização</span><span class="sxs-lookup"><span data-stu-id="9882a-107">Organization</span></span>

- <span data-ttu-id="9882a-108">[**O Capítulo 1**](guix-studio-1.md) fornece uma visão geral básica do Azure RTOS GUIX Studio e a sua relação com o desenvolvimento em tempo real.</span><span class="sxs-lookup"><span data-stu-id="9882a-108">[**Chapter 1**](guix-studio-1.md) provides a basic overview of Azure RTOS GUIX Studio and its relationship to real-time development.</span></span>
- <span data-ttu-id="9882a-109">[**O Capítulo 2**](guix-studio-2.md) dá os passos básicos para instalar e utilizar o Azure RTOS GUIX Studio para analisar a sua aplicação fora da caixa.</span><span class="sxs-lookup"><span data-stu-id="9882a-109">[**Chapter 2**](guix-studio-2.md) gives the basic steps to install and use Azure RTOS GUIX Studio to analyze your application right out of the box.</span></span>
- <span data-ttu-id="9882a-110">[**O Capítulo 3**](guix-studio-3.md) descreve as principais características do Azure RTOS GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="9882a-110">[**Chapter 3**](guix-studio-3.md) describes the main features of Azure RTOS GUIX Studio.</span></span>
- <span data-ttu-id="9882a-111">[**O Capítulo 4**](guix-studio-4.md) descreve como utilizar o Azure RTOS GUIX Studio para criar e gerir os seus recursos de aplicação.</span><span class="sxs-lookup"><span data-stu-id="9882a-111">[**Chapter 4**](guix-studio-4.md) describes how to use Azure RTOS GUIX Studio to create and manage your application resources.</span></span>
- <span data-ttu-id="9882a-112">[**O Capítulo 5**](guix-studio-5.md) descreve como utilizar o designer de ecrã Azure RTOS GUIX WYSIWYG.</span><span class="sxs-lookup"><span data-stu-id="9882a-112">[**Chapter 5**](guix-studio-5.md) describes how to use the Azure RTOS GUIX WYSIWYG screen designer.</span></span>
- <span data-ttu-id="9882a-113">[**O Capítulo 6**](guix-studio-6.md) descreve como a sua aplicação utilizará os ficheiros de saída e as funções API geradas pelo Azure RTOS GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="9882a-113">[**Chapter 6**](guix-studio-6.md) describes how your application will utilize the output files and API functions generated by Azure RTOS GUIX Studio.</span></span>
- <span data-ttu-id="9882a-114">[**Capítulo 7**](guix-studio-7.md) descreve como configurar o fluxo do ecrã</span><span class="sxs-lookup"><span data-stu-id="9882a-114">[**Chapter 7**](guix-studio-7.md) describes how to configure screen flow</span></span>
- <span data-ttu-id="9882a-115">[**Capítulo 8**](guix-studio-8.md) descreve o uso da ferramenta da linha de comando</span><span class="sxs-lookup"><span data-stu-id="9882a-115">[**Chapter 8**](guix-studio-8.md) describes the usage of command line tool</span></span>
- <span data-ttu-id="9882a-116">[**O Capítulo 9**](guix-studio-9.md) descreve uma aplicação uI simples mas completa criada pelo Azure RTOS GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="9882a-116">[**Chapter 9**](guix-studio-9.md) describes a simple but complete UI application created by Azure RTOS GUIX Studio.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="9882a-117">Centro de Apoio ao Cliente</span><span class="sxs-lookup"><span data-stu-id="9882a-117">Customer Support Center</span></span>

<span data-ttu-id="9882a-118">Por favor envie um bilhete de apoio através do Portal Azure para perguntas ou ajuda a usar os passos aqui.</span><span class="sxs-lookup"><span data-stu-id="9882a-118">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="9882a-119">Por favor, forneça-nos as seguintes informações numa mensagem de correio eletrónico para que possamos resolver de forma mais eficiente o seu pedido de apoio:</span><span class="sxs-lookup"><span data-stu-id="9882a-119">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

- <span data-ttu-id="9882a-120">Uma descrição detalhada do problema, incluindo a frequência de ocorrência e como pode ser reproduzida de forma fiável.</span><span class="sxs-lookup"><span data-stu-id="9882a-120">A detailed description of the problem, including frequency of occurrence and how it can be reliably reproduced.</span></span>
- <span data-ttu-id="9882a-121">Prenda o ficheiro de rastreio que causa o problema.</span><span class="sxs-lookup"><span data-stu-id="9882a-121">Attach the trace file that causes the problem.</span></span>
- <span data-ttu-id="9882a-122">A versão do Azure RTOS GUIX Studio que está a utilizar (mostrada na parte superior esquerda do ecrã).</span><span class="sxs-lookup"><span data-stu-id="9882a-122">The version of Azure RTOS GUIX Studio that you are using (shown in the upper left of the display).</span></span>
- <span data-ttu-id="9882a-123">A versão do Azure RTOS GUIX que está a usar incluindo a **variável _gx_version_idstring** e **_gx_build_options.**</span><span class="sxs-lookup"><span data-stu-id="9882a-123">The version of Azure RTOS GUIX that you are using including the **_gx_version_idstring** and **_gx_build_options** variable.</span></span>
- <span data-ttu-id="9882a-124">A versão do Azure RTOS ThreadX que está a utilizar, incluindo o **_tx_version_idstring**.</span><span class="sxs-lookup"><span data-stu-id="9882a-124">The version of Azure RTOS ThreadX that you are using including the **_tx_version_idstring**.</span></span>