---
title: Capítulo 5 - Controladores de Dispositivos para Azure RTOS ThreadX
description: Este capítulo contém uma descrição dos controladores do dispositivo para Azure RTOS ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2432b291f2b3fa7d6d798b8b4c187dd20b97db6b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104827356"
---
# <a name="chapter-5---device-drivers-for-azure-rtos-threadx"></a><span data-ttu-id="cfbd0-103">Capítulo 5 - Controladores de Dispositivos para Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="cfbd0-103">Chapter 5 - Device Drivers for Azure RTOS ThreadX</span></span>

<span data-ttu-id="cfbd0-104">Este capítulo contém uma descrição dos controladores do dispositivo para Azure RTOS ThreadX.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-104">This chapter contains a description of device drivers for Azure RTOS ThreadX.</span></span> <span data-ttu-id="cfbd0-105">A informação apresentada neste capítulo destina-se a ajudar os desenvolvedores a escrever condutores específicos da aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-105">The information presented in this chapter is designed to help developers write application-specific drivers.</span></span>

## <a name="device-driver-introduction"></a><span data-ttu-id="cfbd0-106">Introdução do controlador do dispositivo</span><span class="sxs-lookup"><span data-stu-id="cfbd0-106">Device Driver Introduction</span></span>

<span data-ttu-id="cfbd0-107">A comunicação com o ambiente externo é um componente importante da maioria das aplicações incorporadas.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-107">Communication with the external environment is an important component of most embedded applications.</span></span> <span data-ttu-id="cfbd0-108">Esta comunicação é realizada através de dispositivos de hardware que são acessíveis ao software de aplicação incorporado.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-108">This communication is accomplished through hardware devices that are accessible to the embedded application software.</span></span> <span data-ttu-id="cfbd0-109">Os componentes de software responsáveis pela gestão destes dispositivos são normalmente chamados *de controladores de dispositivos.*</span><span class="sxs-lookup"><span data-stu-id="cfbd0-109">The software components responsible for managing such devices are commonly called *device drivers*.</span></span>

<span data-ttu-id="cfbd0-110">Os controladores de dispositivos em sistemas incorporados e em tempo real são inerentemente dependentes da aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-110">Device drivers in embedded, real-time systems are inherently application dependent.</span></span> <span data-ttu-id="cfbd0-111">Isto é verdade por duas razões principais: a grande diversidade de hardware-alvo e os requisitos de desempenho igualmente vastos impostos às aplicações em tempo real.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-111">This is true for two principal reasons: the vast diversity of target hardware and the equally vast performance requirements imposed on real-time applications.</span></span> <span data-ttu-id="cfbd0-112">Por isso, é praticamente impossível fornecer um conjunto comum de motoristas que satisfaça os requisitos de cada aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-112">Because of this, it is virtually impossible to provide a common set of drivers that will meet the requirements of every application.</span></span> <span data-ttu-id="cfbd0-113">Por estas razões, as informações deste capítulo *destinam-se* a ajudar os utilizadores a personalizar os controladores de dispositivos ThreadX fora da prateleira e a escrever os seus próprios controladores específicos.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-113">For these reasons, the information in this chapter is designed to help users customize *off-the-shelf* ThreadX device drivers and write their own specific drivers.</span></span>

## <a name="driver-functions"></a><span data-ttu-id="cfbd0-114">Funções do controlador</span><span class="sxs-lookup"><span data-stu-id="cfbd0-114">Driver Functions</span></span>

<span data-ttu-id="cfbd0-115">Os controladores de dispositivos ThreadX são compostos por oito áreas funcionais básicas, da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-115">ThreadX device drivers are composed of eight basic functional areas, as follows.</span></span>

- <span data-ttu-id="cfbd0-116">**Inicialização do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-116">**Driver Initialization**</span></span>
- <span data-ttu-id="cfbd0-117">**Controlo do Condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-117">**Driver Control**</span></span>
- <span data-ttu-id="cfbd0-118">**Acesso ao condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-118">**Driver Access**</span></span>
- <span data-ttu-id="cfbd0-119">**Entrada do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-119">**Driver Input**</span></span>
- <span data-ttu-id="cfbd0-120">**Saída do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-120">**Driver Output**</span></span>
- <span data-ttu-id="cfbd0-121">**Interrupções do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-121">**Driver Interrupts**</span></span>
- <span data-ttu-id="cfbd0-122">**Estado do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-122">**Driver Status**</span></span>
- <span data-ttu-id="cfbd0-123">**Rescisão do Condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-123">**Driver Termination**</span></span>

<span data-ttu-id="cfbd0-124">Com exceção da inicialização, cada área funcional do condutor é opcional.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-124">With the exception of initialization, each driver functional area is optional.</span></span> <span data-ttu-id="cfbd0-125">Além disso, o processamento exato em cada área é específico do controlador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-125">Furthermore, the exact processing in each area is specific to the device driver.</span></span>

### <a name="driver-initialization"></a><span data-ttu-id="cfbd0-126">Inicialização do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-126">Driver Initialization</span></span>
<span data-ttu-id="cfbd0-127">Esta área funcional é responsável pela inicialização do dispositivo de hardware real e das estruturas de dados internas do condutor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-127">This functional area is responsible for initialization of the actual hardware device and the internal data structures of the driver.</span></span> <span data-ttu-id="cfbd0-128">Não é permitido chamar outros serviços de motorista até que a inicialização esteja completa.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-128">Calling other driver services is not allowed until initialization is complete.</span></span>

> [!NOTE]
> <span data-ttu-id="cfbd0-129">\*O componente da função de inicialização do condutor é normalmente chamado da função \***tx_application_define** _ ou de uma inicialização thread._</span><span class="sxs-lookup"><span data-stu-id="cfbd0-129">\*The driver's initialization function component is typically called from the \***tx_application_define** _ function or from an initialization thread._</span></span>

### <a name="driver-control"></a><span data-ttu-id="cfbd0-130">Controlo do Condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-130">Driver Control</span></span>

<span data-ttu-id="cfbd0-131">Depois de o condutor ser inicializado e pronto para funcionar, esta área funcional é responsável pelo controlo do tempo de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-131">After the driver is initialized and ready for operation, this functional area is responsible for run-time control.</span></span> <span data-ttu-id="cfbd0-132">Normalmente, o controlo do tempo de execução consiste em fazer alterações no dispositivo de hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-132">Typically, run-time control consists of making changes to the underlying hardware device.</span></span> <span data-ttu-id="cfbd0-133">Exemplos incluem a alteração da taxa de baud de um dispositivo em série ou a procura de um novo sector num disco.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-133">Examples include changing the baud rate of a serial device or seeking a new sector on a disk.</span></span>

### <a name="driver-access"></a><span data-ttu-id="cfbd0-134">Acesso ao condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-134">Driver Access</span></span>

<span data-ttu-id="cfbd0-135">Alguns controladores de dispositivos são chamados apenas a partir de um único fio de aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-135">Some device drivers are called only from a single application thread.</span></span> <span data-ttu-id="cfbd0-136">Nestes casos, esta área funcional não é necessária.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-136">In such cases, this functional area is not needed.</span></span> <span data-ttu-id="cfbd0-137">No entanto, em aplicações em que várias linhas necessitam de acesso simultâneo ao condutor, a sua interação deve ser controlada adicionando instalações de atribuição/desbloqueio no controlador do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-137">However, in applications where multiple threads need simultaneous driver access, their interaction must be controlled by adding assign/ release facilities in the device driver.</span></span> <span data-ttu-id="cfbd0-138">Em alternativa, a aplicação pode utilizar um semáforo para controlar o acesso do condutor e evitar sobrecargas e complicações extra no interior do condutor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-138">Alternatively, the application may use a semaphore to control driver access and avoid extra overhead and complication inside the driver.</span></span>

### <a name="driver-input"></a><span data-ttu-id="cfbd0-139">Entrada do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-139">Driver Input</span></span>

<span data-ttu-id="cfbd0-140">Esta área funcional é responsável por toda a entrada do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-140">This functional area is responsible for all device input.</span></span> <span data-ttu-id="cfbd0-141">As principais questões associadas à entrada do condutor geralmente envolvem como a entrada é tamponada e como os fios aguardam por essa entrada.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-141">The principal issues associated with driver input usually involve how the input is buffered and how threads wait for such input.</span></span>

### <a name="driver-output"></a><span data-ttu-id="cfbd0-142">Saída do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-142">Driver Output</span></span>

<span data-ttu-id="cfbd0-143">Esta área funcional é responsável por toda a saída do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-143">This functional area is responsible for all device output.</span></span> <span data-ttu-id="cfbd0-144">As principais questões associadas à saída do condutor geralmente envolvem a forma como a saída é tamponada e como os fios esperam para executar a saída.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-144">The principal issues associated with driver output usually involve how the output is buffered and how threads wait to perform output.</span></span>

### <a name="driver-interrupts"></a><span data-ttu-id="cfbd0-145">Interrupções do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-145">Driver Interrupts</span></span>

<span data-ttu-id="cfbd0-146">A maioria dos sistemas em tempo real dependem de interrupções de hardware para notificar o condutor de eventos de entrada, saída, controlo e erro do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-146">Most real-time systems rely on hardware interrupts to notify the driver of device input, output, control, and error events.</span></span> <span data-ttu-id="cfbd0-147">As interrupções proporcionam um tempo de resposta garantido a tais eventos externos.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-147">Interrupts provide a guaranteed response time to such external events.</span></span> <span data-ttu-id="cfbd0-148">Em vez de interrupções, o software do controlador pode verificar periodicamente o hardware externo para tais eventos.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-148">Instead of interrupts, the driver software may periodically check the external hardware for such events.</span></span> <span data-ttu-id="cfbd0-149">Esta técnica chama-se *sondagem.*</span><span class="sxs-lookup"><span data-stu-id="cfbd0-149">This technique is called *polling*.</span></span> <span data-ttu-id="cfbd0-150">É menos tempo real do que interrupções, mas as sondagens podem fazer sentido para algumas aplicações menos em tempo real.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-150">It is less real-time than interrupts, but polling may make sense for some less real-time applications.</span></span>

### <a name="driver-status"></a><span data-ttu-id="cfbd0-151">Estado do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-151">Driver Status</span></span>

<span data-ttu-id="cfbd0-152">Esta área de função é responsável por fornecer o estado do tempo de funcionamento e as estatísticas associadas à operação do condutor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-152">This function area is responsible for providing run-time status and statistics associated with the driver operation.</span></span> <span data-ttu-id="cfbd0-153">A informação gerida por esta área de função normalmente inclui o seguinte.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-153">Information managed by this function area typically includes the following.</span></span>

- <span data-ttu-id="cfbd0-154">Estado atual do dispositivo</span><span class="sxs-lookup"><span data-stu-id="cfbd0-154">Current device status</span></span>
- <span data-ttu-id="cfbd0-155">Entradas bytes</span><span class="sxs-lookup"><span data-stu-id="cfbd0-155">Input bytes</span></span>
- <span data-ttu-id="cfbd0-156">Bytes de saída</span><span class="sxs-lookup"><span data-stu-id="cfbd0-156">Output bytes</span></span>
- <span data-ttu-id="cfbd0-157">Contagens de erro do dispositivo</span><span class="sxs-lookup"><span data-stu-id="cfbd0-157">Device error counts</span></span>

### <a name="driver-termination"></a><span data-ttu-id="cfbd0-158">Rescisão do Condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-158">Driver Termination</span></span>

<span data-ttu-id="cfbd0-159">Esta área funcional é opcional.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-159">This functional area is optional.</span></span> <span data-ttu-id="cfbd0-160">Só é necessário desligar o condutor e/ou o dispositivo de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-160">It is only required if the driver and/or the physical hardware device need to be shut down.</span></span> <span data-ttu-id="cfbd0-161">Após a sua demissão, o condutor não deve ser chamado novamente até que seja reiniciado.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-161">After being terminated, the driver must not be called again until it is reinitialized.</span></span>

## <a name="simple-driver-example"></a><span data-ttu-id="cfbd0-162">Exemplo simples do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-162">Simple Driver Example</span></span>

<span data-ttu-id="cfbd0-163">Um exemplo é a melhor maneira de descrever um controlador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-163">An example is the best way to describe a device driver.</span></span> <span data-ttu-id="cfbd0-164">Neste exemplo, o controlador assume um simples dispositivo de hardware em série com um registo de configuração, um registo de entrada e um registo de saída.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-164">In this example, the driver assumes a simple serial hardware device with a configuration register, an input register, and an output register.</span></span> <span data-ttu-id="cfbd0-165">Este exemplo simples do condutor ilustra a inicialização, entrada, saída e interrupção de áreas funcionais.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-165">This simple driver example illustrates the initialization, input, output, and interrupt functional areas.</span></span>

### <a name="simple-driver-initialization"></a><span data-ttu-id="cfbd0-166">Inicialização simples do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-166">Simple Driver Initialization</span></span>

<span data-ttu-id="cfbd0-167">A ***função tx_sdriver_initialize*** do condutor simples cria dois semáforos de contagem que são utilizados para gerir a operação de entrada e saída do condutor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-167">The ***tx_sdriver_initialize*** function of the simple driver creates two counting semaphores that are used to manage the driver's input and output operation.</span></span> <span data-ttu-id="cfbd0-168">O semáforo de entrada é definido pela entrada ISR quando um personagem é recebido pelo dispositivo de hardware em série.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-168">The input semaphore is set by the input ISR when a character is received by the serial hardware device.</span></span> <span data-ttu-id="cfbd0-169">Por causa disso, o semáforo de entrada é criado com uma contagem inicial de zero.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-169">Because of this, the input semaphore is created with an initial count of zero.</span></span>

<span data-ttu-id="cfbd0-170">Inversamente, o semáforo de saída indica a disponibilidade do registo de transmissão de hardware em série.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-170">Conversely, the output semaphore indicates the availability of the serial hardware transmit register.</span></span> <span data-ttu-id="cfbd0-171">É criado com um valor de um para indicar que o registo de transmissão está inicialmente disponível.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-171">It is created with a value of one to indicate the transmit register is initially available.</span></span>

<span data-ttu-id="cfbd0-172">A função de inicialização também é responsável pela instalação dos manipuladores de vetores de interrupção de baixo nível para notificações de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-172">The initialization function is also responsible for installing the low-level interrupt vector handlers for input and output notifications.</span></span> <span data-ttu-id="cfbd0-173">Tal como outras rotinas de serviço de interrupção da ThreadX, o manipulador de baixo nível deve ligar para \***_tx_thread_context_save** _ antes de ligar para o simples controlador ISR.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-173">Like other ThreadX interrupt service routines, the low-level handler must call \***_tx_thread_context_save** _ before calling the simple driver ISR.</span></span> <span data-ttu-id="cfbd0-174">Após a retorna do controlador ISR, o manipulador de baixo nível deve ligar para _\*_ _tx_thread_context_restore_\*\*.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-174">After the driver ISR returns, the low-level handler must call _\*_ _tx_thread_context_restore_\*\*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfbd0-175">\*É importante que a inicialização seja chamada antes de qualquer outra função do controlador.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-175">\*It is important that initialization is called before any of the other driver functions.</span></span> <span data-ttu-id="cfbd0-176">Normalmente, a inicialização do condutor é chamada de ***tx_application_define***.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-176">Typically, driver initialization is called from ***tx_application_define***.</span></span>

```c
VOID tx_sdriver_initialize(VOID)
{
    /* Initialize the two counting semaphores used to control
    the simple driver I/O. */
    tx_semaphore_create(&tx_sdriver_input_semaphore,
                        "simple driver input semaphore", 0);
    tx_semaphore_create(&tx_sdriver_output_semaphore,
                        "simple driver output semaphore", 1);

    /* Setup interrupt vectors for input and output ISRs.
    The initial vector handling should call the ISRs
    defined in this file. */

    /* Configure serial device hardware for RX/TX interrupt
    generation, baud rate, stop bits, etc. */
}
```
<span data-ttu-id="cfbd0-177">**FIGURA 9. Inicialização simples do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-177">**FIGURE 9. Simple Driver Initialization**</span></span>

### <a name="simple-driver-input"></a><span data-ttu-id="cfbd0-178">Entrada simples do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-178">Simple Driver Input</span></span>

<span data-ttu-id="cfbd0-179">Entrada para os centros de condução simples em torno do semáforo de entrada.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-179">Input for the simple driver centers around the input semaphore.</span></span> <span data-ttu-id="cfbd0-180">Quando uma interrupção de entrada de dispositivo de série é recebida, o semáforo de entrada é definido.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-180">When a serial device input interrupt is received, the input semaphore is set.</span></span> <span data-ttu-id="cfbd0-181">Se um ou mais fios estiverem à espera de um personagem do condutor, o fio que espera mais tempo é retomado.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-181">If one or more threads are waiting for a character from the driver, the thread waiting the longest is resumed.</span></span> <span data-ttu-id="cfbd0-182">Se não houver fios à espera, o semáforo permanece simplesmente definido até que um fio chame a função de entrada de unidade.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-182">If no threads are waiting, the semaphore simply remains set until a thread calls the drive input function.</span></span>

<span data-ttu-id="cfbd0-183">Existem várias limitações ao simples manuseamento da entrada do condutor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-183">There are several limitations to the simple driver input handling.</span></span> <span data-ttu-id="cfbd0-184">O mais significativo é o potencial de deixar cair os caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-184">The most significant is the potential for dropping input characters.</span></span> <span data-ttu-id="cfbd0-185">Isto é possível porque não há capacidade de tampão de caracteres de entrada que chegam antes do personagem anterior ser processado.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-185">This is possible because there is no ability to buffer input characters that arrive before the previous character is processed.</span></span> <span data-ttu-id="cfbd0-186">Isto é facilmente manuseado adicionando um tampão de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-186">This is easily handled by adding an input character buffer.</span></span>

> [!NOTE]
> <span data-ttu-id="cfbd0-187">*Apenas fios são permitidos para chamar o*  \* **tx_sdriver_input** _ _function.\*</span><span class="sxs-lookup"><span data-stu-id="cfbd0-187">*Only threads are allowed to call the* ***tx_sdriver_input** _ _function.*</span></span>

<span data-ttu-id="cfbd0-188">A figura 10 mostra o código de origem associado à simples entrada do controlador.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-188">Figure 10 shows the source code associated with simple driver input.</span></span>

```c
UCHAR tx_sdriver_input(VOID)
{
  /* Determine if there is a character waiting. If not,
  suspend. */
  tx_semaphore_get(&tx_sdriver_input_semaphore,
  TX_WAIT_FOREVER;

  /* Return character from serial RX hardware register. */
  return(*serial_hardware_input_ptr);
}
  VOID tx_sdriver_input_ISR(VOID)
{
  /* See if an input character notification is pending. */
  if (!tx_sdriver_input_semaphore.tx_semaphore_count)
  {
    /* If not, notify thread of an input character. */
    tx_semaphore_put(&tx_sdriver_input_semaphore);
  }
}
```
<span data-ttu-id="cfbd0-189">**FIGURA 10. Entrada simples do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-189">**FIGURE 10. Simple Driver Input**</span></span>

### <a name="simple-driver-output"></a><span data-ttu-id="cfbd0-190">Saída simples do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-190">Simple Driver Output</span></span>

<span data-ttu-id="cfbd0-191">O processamento de saída utiliza o semáforo de saída para sinalizar quando o registo de transmissão do dispositivo em série está livre.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-191">Output processing utilizes the output semaphore to signal when the serial device's transmit register is free.</span></span> <span data-ttu-id="cfbd0-192">Antes de um caracter de saída ser realmente escrito para o dispositivo, o semáforo de saída é obtido.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-192">Before an output character is actually written to the device, the output semaphore is obtained.</span></span> <span data-ttu-id="cfbd0-193">Se não estiver disponível, o transmissor anterior ainda não está completo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-193">If it is not available, the previous transmit is not yet complete.</span></span>

<span data-ttu-id="cfbd0-194">A saída ISR é responsável pelo manuseamento da interrupção completa do transmissor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-194">The output ISR is responsible for handling the transmit complete interrupt.</span></span> <span data-ttu-id="cfbd0-195">O processamento da saída ISR equivale a definir o semáforo de saída, permitindo assim a saída de outro carácter.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-195">Processing of the output ISR amounts to setting the output semaphore, thereby allowing output of another character.</span></span>

> [!NOTE]
> <span data-ttu-id="cfbd0-196">*Apenas fios são permitidos para chamar o*  \* **tx_sdriver_output** _ _function.\*</span><span class="sxs-lookup"><span data-stu-id="cfbd0-196">*Only threads are allowed to call the* ***tx_sdriver_output** _ _function.*</span></span>

<span data-ttu-id="cfbd0-197">A figura 11 mostra o código fonte associado à simples saída do controlador.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-197">Figure 11 shows the source code associated with simple driver output.</span></span>

```c
VOID tx_sdriver_output(UCHAR alpha)
{
  /* Determine if the hardware is ready to transmit a
  character. If not, suspend until the previous output
  completes. */
  tx_semaphore_get(&tx_sdriver_output_semaphore,
                                          TX_WAIT_FOREVER);

  /* Send the character through the hardware. */
  *serial_hardware_output_ptr = alpha;
}
  
VOID tx_sdriver_output_ISR(VOID)
{
  /* Notify thread last character transmit is
  complete. */
  tx_semaphore_put(&tx_sdriver_output_semaphore);
}
```
<span data-ttu-id="cfbd0-198">**FIGURA 11. Saída simples do condutor**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-198">**FIGURE 11. Simple Driver Output**</span></span>

### <a name="simple-driver-shortcomings"></a><span data-ttu-id="cfbd0-199">Insuficiências simples do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-199">Simple Driver Shortcomings</span></span>

<span data-ttu-id="cfbd0-200">Este exemplo simples do controlador do dispositivo ilustra a ideia básica de um controlador de dispositivo ThreadX.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-200">This simple device driver example illustrates the basic idea of a ThreadX device driver.</span></span> <span data-ttu-id="cfbd0-201">No entanto, uma vez que o simples controlador do dispositivo não aborda o buffering de dados ou quaisquer problemas de sobrecarga, não representa totalmente os controladores threadX do mundo real.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-201">However, because the simple device driver does not address data buffering or any overhead issues, it does not fully represent real-world ThreadX drivers.</span></span> <span data-ttu-id="cfbd0-202">A secção seguinte descreve alguns dos problemas mais avançados associados aos condutores do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-202">The following section describes some of the more advanced issues associated with device drivers.</span></span>

## <a name="advanced-driver-issues"></a><span data-ttu-id="cfbd0-203">Problemas avançados do condutor</span><span class="sxs-lookup"><span data-stu-id="cfbd0-203">Advanced Driver Issues</span></span>

<span data-ttu-id="cfbd0-204">Como mencionado anteriormente, os controladores de dispositivos têm requisitos tão únicos como as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-204">As mentioned previously, device drivers have requirements as unique as their applications.</span></span> <span data-ttu-id="cfbd0-205">Algumas aplicações podem necessitar de uma enorme quantidade de buffering de dados, enquanto outra aplicação pode necessitar de ISRs do controlador otimizados devido a interrupções de dispositivos de alta frequência.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-205">Some applications may require an enormous amount of data buffering while another application may require optimized driver ISRs because of high-frequency device interrupts.</span></span>

### <a name="io-buffering"></a><span data-ttu-id="cfbd0-206">Tampão I/O</span><span class="sxs-lookup"><span data-stu-id="cfbd0-206">I/O Buffering</span></span>

<span data-ttu-id="cfbd0-207">O tampão de dados em aplicações incorporadas em tempo real requer um planeamento considerável.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-207">Data buffering in real-time embedded applications requires considerable planning.</span></span> <span data-ttu-id="cfbd0-208">Parte do design é ditado pelo dispositivo de hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-208">Some of the design is dictated by the underlying hardware device.</span></span> <span data-ttu-id="cfbd0-209">Se o dispositivo fornecer byte I/O básico, um simples tampão circular está provavelmente em ordem.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-209">If the device provides basic byte I/O, a simple circular buffer is probably in order.</span></span> <span data-ttu-id="cfbd0-210">No entanto, se o dispositivo fornecer bloco, DMA ou pacote I/O, um esquema de gestão de tampão é provavelmente justificado.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-210">However, if the device provides block, DMA, or packet I/O, a buffer management scheme is probably warranted.</span></span>

### <a name="circular-byte-buffers"></a><span data-ttu-id="cfbd0-211">Tampão Circular Byte</span><span class="sxs-lookup"><span data-stu-id="cfbd0-211">Circular Byte Buffers</span></span>

<span data-ttu-id="cfbd0-212">Os amortecedores de byte circular são normalmente utilizados em condutores que gerem um simples dispositivo de hardware em série como um UART.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-212">Circular byte buffers are typically used in drivers that manage a simple serial hardware device like a UART.</span></span> <span data-ttu-id="cfbd0-213">Dois tampão circular são mais frequentemente usados em tais situações - um para entrada e um para saída.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-213">Two circular buffers are most often used in such situations—one for input and one for output.</span></span>

<span data-ttu-id="cfbd0-214">Cada tampão de byte circular é composto por uma área de memória byte (tipicamente uma matriz de **UCHAR** s), um ponteiro de leitura e um ponteiro de escrita.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-214">Each circular byte buffer is comprised of a byte memory area (typically an array of **UCHAR** s), a read pointer, and a write pointer.</span></span> <span data-ttu-id="cfbd0-215">Um tampão é considerado vazio quando o ponteiro de leitura e os ponteiros de escrita referenciam o mesmo local de memória no tampão.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-215">A buffer is considered empty when the read pointer and the write pointers reference the same memory location in the buffer.</span></span> <span data-ttu-id="cfbd0-216">A inicialização do condutor define tanto os ponteiros de leitura como os ponteiros tampão para o endereço inicial do tampão.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-216">Driver initialization sets both the read and write buffer pointers to the beginning address of the buffer.</span></span>

### <a name="circular-buffer-input"></a><span data-ttu-id="cfbd0-217">Entrada de tampão circular</span><span class="sxs-lookup"><span data-stu-id="cfbd0-217">Circular Buffer Input</span></span>

<span data-ttu-id="cfbd0-218">O tampão de entrada é utilizado para segurar caracteres que chegam antes de a aplicação estar pronta para eles.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-218">The input buffer is used to hold characters that arrive before the application is ready for them.</span></span> <span data-ttu-id="cfbd0-219">Quando um personagem de entrada é recebido (geralmente numa rotina de serviço de interrupção), o novo carácter é recuperado do dispositivo de hardware e colocado no tampão de entrada no local apontado pelo ponteiro de escrita.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-219">When an input character is received (usually in an interrupt service routine), the new character is retrieved from the hardware device and placed into the input buffer at the location pointed to by the write pointer.</span></span> <span data-ttu-id="cfbd0-220">O ponteiro de escrita é então avançado para a posição seguinte no tampão.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-220">The write pointer is then advanced to the next position in the buffer.</span></span> <span data-ttu-id="cfbd0-221">Se a próxima posição passar do fim do tampão, o ponteiro de escrita está definido para o início do tampão.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-221">If the next position is past the end of the buffer, the write pointer is set to the beginning of the buffer.</span></span> <span data-ttu-id="cfbd0-222">A condição completa da fila é tratada cancelando o avanço do ponteiro de escrita se o novo ponteiro de escrita for o mesmo que o ponteiro de leitura.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-222">The queue full condition is handled by canceling the write pointer advancement if the new write pointer is the same as the read pointer.</span></span>

<span data-ttu-id="cfbd0-223">Os pedidos de byte de entrada de aplicação ao condutor examinam primeiro os ponteiros de leitura e escrita do tampão de entrada.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-223">Application input byte requests to the driver first examine the read and write pointers of the input buffer.</span></span> <span data-ttu-id="cfbd0-224">Se os ponteiros de leitura e de escrita forem idênticos, o tampão está vazio.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-224">If the read and write pointers are identical, the buffer is empty.</span></span> <span data-ttu-id="cfbd0-225">Caso contrário, se o ponteiro de leitura não for o mesmo, o byte apontado pelo ponteiro de leitura é copiado do tampão de entrada e o ponteiro de leitura é avançado para o local do tampão seguinte.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-225">Otherwise, if the read pointer is not the same, the byte pointed to by the read pointer is copied from the input buffer and the read pointer is advanced to the next buffer location.</span></span> <span data-ttu-id="cfbd0-226">Se o novo ponteiro de leitura passar do fim do tampão, é reposto para o início.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-226">If the new read pointer is past the end of the buffer, it is reset to the beginning.</span></span> <span data-ttu-id="cfbd0-227">A figura 12 mostra a lógica do tampão de entrada circular.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-227">Figure 12 shows the logic for the circular input buffer.</span></span>

```c
UCHAR   tx_input_buffer[MAX_SIZE];
UCHAR   tx_input_write_ptr;
UCHAR   tx_input_read_ptr;

/* Initialization. */
tx_input_write_ptr =    &tx_input_buffer[0];
tx_input_read_ptr =     &tx_input_buffer[0];

/* Input byte ISR... UCHAR alpha has character from device. */
save_ptr = tx_input_write_ptr;
*tx_input_write_ptr++ = alpha;
if (tx_input_write_ptr > &tx_input_buffer[MAX_SIZE-1])
    tx_input_write_ptr = &tx_input_buffer[0]; /* Wrap */
if (tx_input_write_ptr == tx_input_read_ptr)
    tx_input_write_ptr = save_ptr; /* Buffer full */

/* Retrieve input byte from buffer... */
if (tx_input_read_ptr != tx_input_write_ptr)
{
  alpha = *tx_input_read_ptr++;
  if (tx_input_read_ptr > &tx_input_buffer[MAX_SIZE-1])
      tx_input_read_ptr = &tx_input_buffer[0];
}
```
<span data-ttu-id="cfbd0-228">**FIGURA 12. Lógica para tampão de entrada circular**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-228">**FIGURE 12. Logic for Circular Input Buffer**</span></span>

> [!NOTE]
> <span data-ttu-id="cfbd0-229">\*Para um funcionamento fiável, pode ser necessário bloquear as interrupções ao manipular os ponteiros de leitura e escrever tanto os tampões circulares de entrada como os tampões circulares de saída.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-229">\*For reliable operation, it may be necessary to lockout interrupts when manipulating the read and write pointers of both the input and output circular buffers.</span></span> *

### <a name="circular-output-buffer"></a><span data-ttu-id="cfbd0-230">Tampão de saída circular</span><span class="sxs-lookup"><span data-stu-id="cfbd0-230">Circular Output Buffer</span></span>

<span data-ttu-id="cfbd0-231">O tampão de saída é utilizado para segurar caracteres que chegaram para a saída antes do dispositivo de hardware terminar de enviar o byte anterior.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-231">The output buffer is used to hold characters that have arrived for output before the hardware device finished sending the previous byte.</span></span> <span data-ttu-id="cfbd0-232">O processamento do tampão de saída é semelhante ao processamento do tampão de entrada, exceto que o processamento de interrupção completa de transmissão manipula o ponteiro de leitura de saída, enquanto o pedido de saída da aplicação utiliza o ponteiro de escrita de saída.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-232">Output buffer processing is similar to input buffer processing, except the transmit complete interrupt processing manipulates the output read pointer, while the application output request utilizes the output write pointer.</span></span>
<span data-ttu-id="cfbd0-233">Caso contrário, o processamento do tampão de saída é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-233">Otherwise, the output buffer processing is the same.</span></span> <span data-ttu-id="cfbd0-234">A figura 13 mostra a lógica do tampão de saída circular.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-234">Figure 13 shows the logic for the circular output buffer.</span></span>

```c
UCHAR   tx_output_buffer[MAX_SIZE];
UCHAR   tx_output_write_ptr;
UCHAR   tx_output_read_ptr;

/* Initialization. */
tx_output_write_ptr = &tx_output_buffer[0];
tx_output_read_ptr = &tx_output_buffer[0];

/* Transmit complete ISR... Device ready to send. */
if (tx_output_read_ptr != tx_output_write_ptr)
{
  *device_reg = *tx_output_read_ptr++;
  if (tx_output_read_reg > &tx_output_buffer[MAX_SIZE-1])
      tx_output_read_ptr = &tx_output_buffer[0];
}

/* Output byte driver service. If device busy, buffer! */
save_ptr = tx_output_write_ptr;
*tx_output_write_ptr++ = alpha;
if (tx_output_write_ptr > &tx_output_buffer[MAX_SIZE-1])
    tx_output_write_ptr = &tx_output_buffer[0]; /* Wrap */
if (tx_output_write_ptr == tx_output_read_ptr)
    tx_output_write_ptr = save_ptr; /* Buffer full! */
```
<span data-ttu-id="cfbd0-235">**FIGURA 13. Lógica para tampão de saída circular**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-235">**FIGURE 13. Logic for Circular Output Buffer**</span></span>

### <a name="buffer-io-management"></a><span data-ttu-id="cfbd0-236">Gestão de I/O do tampão</span><span class="sxs-lookup"><span data-stu-id="cfbd0-236">Buffer I/O Management</span></span>

<span data-ttu-id="cfbd0-237">Para melhorar o desempenho dos microprocessadores incorporados, muitos dispositivos periféricos transmitem e recebem dados com tampão fornecidos pelo software.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-237">To improve the performance of embedded microprocessors, many peripheral device devices transmit and receive data with buffers supplied by software.</span></span> <span data-ttu-id="cfbd0-238">Em algumas implementações, vários buffers podem ser usados para transmitir ou receber pacotes individuais de dados.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-238">In some implementations, multiple buffers may be used to transmit or receive individual packets of data.</span></span>

<span data-ttu-id="cfbd0-239">O tamanho e localização dos amortecedores de I/S é determinado pela aplicação e/ou software do condutor.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-239">The size and location of I/O buffers is determined by the application and/or driver software.</span></span> <span data-ttu-id="cfbd0-240">Normalmente, os tampão são fixos em tamanho e geridos dentro de um conjunto de memória de bloco ThreadX.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-240">Typically, buffers are fixed in size and managed within a ThreadX block memory pool.</span></span> <span data-ttu-id="cfbd0-241">A Figura 14 descreve um tampão de E/S típico e um conjunto de memória de bloco ThreadX que gere a sua alocação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-241">Figure 14 describes a typical I/O buffer and a ThreadX block memory pool that manages their allocation.</span></span>

```c
typedef struct TX_IO_BUFFER_STRUCT
{
      struct TX_IO_BUFFER_STRUCT *tx_next_packet;
      struct TX_IO_BUFFER_STRUCT *tx_next_buffer;
      UCHAR tx_buffer_area[TX_MAX_BUFFER_SIZE];
} TX_IO_BUFFER;

TX_BLOCK_POOL tx_io_block_pool;

/* Create a pool of I/O buffers. Assume that the pointer
"free_memory_ptr"points to an available memory area that
is 64 KBytes in size. */
tx_block_pool_create(&tx_io_block_pool,
                  "Sample IO Driver Buffer Pool",
                  free_memory_ptr, 0x10000,
                  sizeof(TX_IO_BUFFER));
```

<span data-ttu-id="cfbd0-242">**FIGURA 14. Tampão I/O**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-242">**FIGURE 14. I/O Buffer**</span></span>

### <a name="tx_io_buffer"></a><span data-ttu-id="cfbd0-243">TX_IO_BUFFER</span><span class="sxs-lookup"><span data-stu-id="cfbd0-243">TX_IO_BUFFER</span></span>

<span data-ttu-id="cfbd0-244">O TX_IO_BUFFER da tipa é composto por dois ponteiros.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-244">The typedef TX_IO_BUFFER consists of two pointers.</span></span> <span data-ttu-id="cfbd0-245">O **ponteiro tx_next_packet** é utilizado para ligar vários pacotes na lista de entradas ou saídas.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-245">The **tx_next_packet** pointer is used to link multiple packets on either the input or output list.</span></span> <span data-ttu-id="cfbd0-246">O **ponteiro tx_next_buffer** é usado para ligar tampãos que compõem um pacote individual de dados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-246">The **tx_next_buffer** pointer is used to link together buffers that make up an individual packet of data from the device.</span></span> <span data-ttu-id="cfbd0-247">Ambos os ponteiros são definidos para NU QUANDO o tampão é atribuído a partir da piscina.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-247">Both of these pointers are set to NULL when the buffer is allocated from the pool.</span></span> <span data-ttu-id="cfbd0-248">Além disso, alguns dispositivos podem necessitar de outro campo para indicar quanto da área tampão realmente contém dados.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-248">In addition, some devices may require another field to indicate how much of the buffer area actually contains data.</span></span>

### <a name="buffered-io-advantage"></a><span data-ttu-id="cfbd0-249">Vantagem de I/O tamponada</span><span class="sxs-lookup"><span data-stu-id="cfbd0-249">Buffered I/O Advantage</span></span>

<span data-ttu-id="cfbd0-250">Quais são as vantagens de um esquema de E/S de tampão?</span><span class="sxs-lookup"><span data-stu-id="cfbd0-250">What are the advantages of a buffer I/O scheme?</span></span> <span data-ttu-id="cfbd0-251">A maior vantagem é que os dados não são copiados entre os registos do dispositivo e a memória da aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-251">The biggest advantage is that data is not copied between the device registers and the application's memory.</span></span> <span data-ttu-id="cfbd0-252">Em vez disso, o controlador fornece ao dispositivo uma série de ponteiros de tampão.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-252">Instead, the driver provides the device with a series of buffer pointers.</span></span> <span data-ttu-id="cfbd0-253">O dispositivo físico I/O utiliza diretamente a memória tampão fornecida.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-253">Physical device I/O utilizes the supplied buffer memory directly.</span></span>

<span data-ttu-id="cfbd0-254">A utilização do processador para copiar pacotes de informação de entrada ou saída é extremamente dispendiosa e deve ser evitada em qualquer situação de I/O de alta produção.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-254">Using the processor to copy input or output packets of information is extremely costly and should be avoided in any high throughput I/O situation.</span></span>

<span data-ttu-id="cfbd0-255">Outra vantagem para a abordagem de E/S tamponada é que as listas de entradas e saídas não têm condições completas.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-255">Another advantage to the buffered I/O approach is that the input and output lists do not have full conditions.</span></span> <span data-ttu-id="cfbd0-256">Todos os amortecedores disponíveis podem estar em qualquer uma das listas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-256">All of the available buffers can be on either list at any one time.</span></span> <span data-ttu-id="cfbd0-257">Isto contrasta com os simples tampão circulares byte apresentados anteriormente no capítulo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-257">This contrasts with the simple byte circular buffers presented earlier in the chapter.</span></span> <span data-ttu-id="cfbd0-258">Cada um tinha um tamanho fixo determinado na compilação.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-258">Each had a fixed size determined at compilation.</span></span>

### <a name="buffered-driver-responsibilities"></a><span data-ttu-id="cfbd0-259">Responsabilidades do condutor tamponado</span><span class="sxs-lookup"><span data-stu-id="cfbd0-259">Buffered Driver Responsibilities</span></span>

<span data-ttu-id="cfbd0-260">Os controladores de dispositivos tamponados só se preocupam com a gestão de listas ligadas de tampões de I/O.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-260">Buffered device drivers are only concerned with managing linked lists of I/O buffers.</span></span> <span data-ttu-id="cfbd0-261">Mantém-se uma lista de tampão de entrada para pacotes que são recebidos antes de o software da aplicação estar pronto.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-261">An input buffer list is maintained for packets that are received before the application software is ready.</span></span> <span data-ttu-id="cfbd0-262">Inversamente, mantém-se uma lista de tampão de saída para os pacotes que são enviados mais rapidamente do que o dispositivo de hardware pode manuseá-los.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-262">Conversely, an output buffer list is maintained for packets being sent faster than the hardware device can handle them.</span></span> <span data-ttu-id="cfbd0-263">A figura 15 mostra listas simples de entradas e saídas ligadas a pacotes de dados e o(s) tampão(s) que compõem cada pacote.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-263">Figure 15 shows simple input and output linked lists of data packets and the buffer(s) that make up each packet.</span></span>

<span data-ttu-id="cfbd0-264">**Lista de Entradas**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-264">**Input List**</span></span>

![Lista de Entradas](./media/user-guide/input-list.png)

<span data-ttu-id="cfbd0-266">**Lista de saídas**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-266">**Output List**</span></span>

![Lista de saídas](./media/user-guide/output-list.png)

<span data-ttu-id="cfbd0-268">**FIGURA 15. Listas Input-Output**</span><span class="sxs-lookup"><span data-stu-id="cfbd0-268">**FIGURE 15. Input-Output Lists**</span></span>

<span data-ttu-id="cfbd0-269">Interface de aplicações com controladores tampão com os mesmos tampões de E/S.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-269">Applications interface with buffered drivers with the same I/O buffers.</span></span> <span data-ttu-id="cfbd0-270">No que diz sobre transmissão, o software de aplicação fornece ao condutor um ou mais tampões para transmitir.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-270">On transmit, application software provides the driver with one or more buffers to transmit.</span></span> <span data-ttu-id="cfbd0-271">Quando o software da aplicação solicita a entrada, o controlador devolve os dados de entrada em tampões de E/S.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-271">When the application software requests input, the driver returns the input data in I/O buffers.</span></span>

> [!NOTE]
> <span data-ttu-id="cfbd0-272">*Em algumas aplicações, pode ser útil construir uma interface de entrada do controlador que requer a aplicação para trocar um tampão gratuito por um tampão de entrada do controlador. Isto pode aliviar algum processamento de alocação de tampão dentro do condutor.*</span><span class="sxs-lookup"><span data-stu-id="cfbd0-272">*In some applications, it may be useful to build a driver input interface that requires the application to exchange a free buffer for an input buffer from the driver. This might alleviate some buffer allocation processing inside of the driver.*</span></span>

### <a name="interrupt-management"></a><span data-ttu-id="cfbd0-273">Gestão de Interrupção</span><span class="sxs-lookup"><span data-stu-id="cfbd0-273">Interrupt Management</span></span>

<span data-ttu-id="cfbd0-274">Em algumas aplicações, a frequência de interrupção do dispositivo pode proibir a escrita do ISR em C ou interagir com a ThreadX em cada interrupção.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-274">In some applications, the device interrupt frequency may prohibit writing the ISR in C or to interact with ThreadX on each interrupt.</span></span> <span data-ttu-id="cfbd0-275">Por exemplo, se for preciso 25us para salvar e restaurar o contexto interrompido, não seria aconselhável realizar um contexto completo, salvo se a frequência de interrupção fosse de 50us.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-275">For example, if it takes 25us to save and restore the interrupted context, it would not be advisable to perform a full context save if the interrupt frequency was 50us.</span></span> <span data-ttu-id="cfbd0-276">Nesses casos, uma pequena linguagem de montagem ISR é usada para manusear a maioria das interrupções do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-276">In such cases, a small assembly language ISR is used to handle most of the device interrupts.</span></span> <span data-ttu-id="cfbd0-277">Este ISR de baixa sobrecarga só interagiria com a ThreadX quando necessário.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-277">This low-overhead ISR would only interact with ThreadX when necessary.</span></span>

<span data-ttu-id="cfbd0-278">Uma discussão semelhante pode ser encontrada na discussão de gestão interrompida no final do capítulo 3.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-278">A similar discussion can be found in the interrupt management discussion at the end of Chapter 3.</span></span>

### <a name="thread-suspension"></a><span data-ttu-id="cfbd0-279">Suspensão do fio</span><span class="sxs-lookup"><span data-stu-id="cfbd0-279">Thread Suspension</span></span>

<span data-ttu-id="cfbd0-280">No exemplo simples do condutor apresentado anteriormente neste capítulo, o chamador do serviço de entrada suspende se um personagem não estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-280">In the simple driver example presented earlier in this chapter, the caller of the input service suspends if a character is not available.</span></span> <span data-ttu-id="cfbd0-281">Em algumas aplicações, isto pode não ser aceitável.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-281">In some applications, this might not be acceptable.</span></span>

<span data-ttu-id="cfbd0-282">Por exemplo, se o fio responsável pelo processamento da entrada de um condutor também tiver outras funções, suspender apenas a entrada do condutor provavelmente não vai funcionar.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-282">For example, if the thread responsible for processing input from a driver also has other duties, suspending on just the driver input is probably not going to work.</span></span> <span data-ttu-id="cfbd0-283">Em vez disso, o condutor precisa de ser personalizado para solicitar um processamento semelhante à forma como outros pedidos de processamento são feitos na linha.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-283">Instead, the driver needs to be customized to request processing similar to the way other processing requests are made to the thread.</span></span>

<span data-ttu-id="cfbd0-284">Na maioria dos casos, o tampão de entrada é colocado numa lista ligada e uma mensagem de evento de entrada é enviada para a fila de entrada da linha.</span><span class="sxs-lookup"><span data-stu-id="cfbd0-284">In most cases, the input buffer is placed on a linked list and an input event message is sent to the thread's input queue.</span></span>