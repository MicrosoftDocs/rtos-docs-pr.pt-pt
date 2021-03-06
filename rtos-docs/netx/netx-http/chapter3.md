---
title: Capítulo 3 - Descrição dos serviços NetX HTTP
description: Este capítulo contém uma descrição de todos os serviços NetX HTTP (listados abaixo) por ordem alfabética.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: eabb455b6e21b4fe51db944a0da12afa85ee390a78db633ee670de5aadcde07b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791521"
---
# <a name="chapter-3---description-of-netx-http-services"></a>Capítulo 3 - Descrição dos serviços NetX HTTP

Este capítulo contém uma descrição de todos os serviços NetX HTTP (listados abaixo) por ordem alfabética.

Na secção "Valores de Retorno" nas seguintes descrições da API, os valores em **BOLD** não são afetados pelo **NX_DISABLE_ERROR_CHECKING** definem que é utilizado para desativar a verificação de erros de API, enquanto os valores não arrojados são completamente desactivos.

**Serviços de clientes HTTP:**

- nx_http_client_create Criar *uma instância http do cliente*
- nx_http_client_delete Eliminar *uma instância do cliente HTTP*
- nx_http_client_get_start Iniciar *um pedido HTTP GET*
- nx_http_client_get_start_extended Iniciar *um pedido HTTP GET*
- nx_http_client_get_packet *Obtenha o próximo pacote de dados de recursos*
- nx_http_client_put_start Iniciar *um pedido HTTP PUT*
- nx_http_client_put_start_extended Iniciar *um pedido HTTP PUT*
- nx_http_client_put_packet Enviar *o próximo pacote de dados de recursos*
- *nx_http_client_set_connect_port* *Alterar a porta para ligar ao servidor HTTP*

**Serviços de servidorES HTTP:**

- nx_http_server_cache_info_callback_set Definir *chamada para recuperar a idade e última data modificada do URL especificado*
- nx_http_server_callback_data_send Enviar *dados HTTP da função de retorno*
- nx_http_server_callback_generate_response_header Criar *cabeçalho de resposta em funções de retorno*
- nx_http_server_callback_generate_response_header_extended Criar *cabeçalho de resposta em funções de retorno*
- nx_http_server_callback_packet_send *Enviar um pacote HTTP a partir de uma chamada HTTP*
- nx_http_server_callback_response_send Enviar *resposta da função de retorno*
- nx_http_server_callback_response_send_extended *Enviar resposta da função de retorno*
- nx_http_server_content_get Obter *conteúdo do pedido*
- nx_http_server_content_get_extended Obtenha *conteúdo do pedido; suporta pedidos vazios (duração zero de conteúdo)*
- nx_http_server_content_length_get *Obtenha a duração do conteúdo no pedido*
- nx_http_server_content_length_get_extended *Obtenha a duração do conteúdo no pedido; suporta pedidos vazios (duração zero de conteúdo)*
- nx_http_server_create Criar *uma instância do servidor HTTP*
- nx_http_server_delete Eliminar *uma instância do servidor HTTP*
- nx_http_server_get_entity_content *Tamanho e localização do conteúdo da entidade em URL*
- nx_http_server_get_entity_header *Extrair cabeçalho da entidade URL em tampão especificado*
- nx_http_server_gmt_callback_set *Definir a chamada para recuperar a data e a hora do GMT*
- nx_http_server_invalid_userpassword_notify_set Definir *o retorno para quando o nome de utilizador e a palavra-passe inválidos são recebidos num pedido do Cliente*
- nx_http_server_mime_maps_additional_set Definir *mapas de mímica adicionais para HTML*
- nx_http_server_packet_content_find *Extrair o comprimento do conteúdo no cabeçalho HTTP e definir o ponteiro para iniciar os dados de conteúdo*
- nx_http_server_packet_get Receber *pacote de cliente diretamente*
- nx_http_server_param_get Obtenha *o parâmetro do pedido*
- nx_http_server_query_get Obter *consulta do pedido*
- nx_http_server_start *Iniciar o servidor HTTP*
- nx_http_server_stop Parar *o servidor HTTP*
- nx_http_server_type_get *Extrato HTTP tipo HTTP, por exemplo, texto/planície do cabeçalho*
- nx_http_server_type_get_extended *Extrato HTTP tipo HTTP, por exemplo, texto/planície do cabeçalho*
- nx_http_server_digest_authenticate_notify_set Definir *digerir função de retorno autenticado*
- nx_http_server_authentication_check_set *Definir função de verificação de autenticação*

## <a name="nx_http_client_create"></a>nx_http_client_create

### <a name="create-an-http-client-instance"></a>Criar uma instância de cliente HTTP

**Protótipo**

```c
UINT nx_http_client_create(NX_HTTP_CLIENT *client_ptr,
                          CHAR *client_name, NX_IP *ip_ptr, 
                          NX_PACKET_POOL *pool_ptr,
                          ULONG window_size);
```

**Descrição**

Este serviço cria uma instância http cliente na instância IP especificada.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **client_name** Nome da instância do cliente HTTP.
- **ip_ptr** Ponteiro para a instância IP.
- **pool_ptr** Ponteiro para piscina de pacote padrão. Note que os pacotes desta piscina devem ter uma carga útil suficientemente grande para manusear o cabeçalho de resposta completo. Isto é definido por NX_HTTP_CLIENT_MIN_PACKET_SIZE em *nx_http_client.h*.
- **window_size** O tamanho da tomada TCP do Cliente recebe a janela.

**Valores de devolução**

- **NX_SUCCESS** (0x00) Sucesso http cliente criar
- NX_PTR_ERROR (0x16) Inválido HTTP, ip_ptr ou ponteiro de piscina de pacotes
- NX_HTTP_POOL_ERROR (0xE9) Tamanho da carga útil inválida na piscina de pacotes

**Permitido a partir de**

Inicialização, Threads

**Exemplo**

```c
/* Create the HTTP Client instance “my_client” on “ip_0”. */
status = nx_http_client_create(&my_client, “my client”, &ip_0, &pool_0, 100);
  
/* If status is NX_SUCCESS an HTTP Client instance was successfully  created. */
```

## <a name="nx_http_client_delete"></a>nx_http_client_delete

### <a name="delete-an-http-client-instance"></a>Excluir uma instância de cliente HTTP

**Protótipo**

```c
UINT nx_http_client_delete(NX_HTTP_CLIENT *client_ptr);
```

**Descrição**

Este serviço elimina uma instância do cliente HTTP previamente criada.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.

**Valores de devolução**

- **NX_SUCCESS** (0x00) Com sucesso HTTP Cliente delete
- NX_PTR_ERROR (0x16) Ponteiro HTTP inválido
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Delete the HTTP Client instance “my_client.” */
status = nx_http_client_delete(&my_client);

/* If status is NX_SUCCESS an HTTP Client instance was successfully  deleted. */
```

## <a name="nx_http_client_get_start"></a>nx_http_client_get_start

### <a name="start-an-http-get-request"></a>Inicie um pedido HTTP GET

**Protótipo**

```c
UINT nx_http_client_get_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource, CHAR *input_ptr,
                             UINT input_size, CHAR *username, CHAR *password,
                             ULONG wait_option);
```

**Descrição**

Este serviço tenta obter o recurso especificado por "recurso" na instância do cliente HTTP anteriormente criada. Se esta rotina voltar NX_SUCCESS, a aplicação pode então fazer várias chamadas para *nx_http_client_get_packet* para recuperar pacotes de dados correspondentes ao conteúdo de recursos solicitado.

Note que o string de recursos pode referir-se a um ficheiro local, por exemplo, "/index.htm" ou pode referir-se a outro URL, por exemplo, `http://abc.website.com/index.htm` se o SERVIDOR HTTP indicar que suporta pedidos GET de referência.

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para *nx_http_client_get_start_extended()*

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **ip_address** Endereço IP do servidor HTTP.
- **recurso** Ponteiro para cadeia URL para recurso solicitado.
- **input_ptr** Ponteiro para dados adicionais para o pedido GET. Isto é opcional. Se válido, a entrada especificada é colocada na área de conteúdo da mensagem e um POST é utilizado em vez de uma operação GET.
- **input_size** Número de bytes em entrada adicional opcional apontada por input_ptr.
- **nome de utilizador** Ponteiro para o nome de utilizador opcional para a autenticação.
- **senha** Ponteiro para senha opcional para autenticação.
-**wait_option** Define quanto tempo o serviço irá esperar pelo pedido de início do cliente HTTP. As opções de espera são definidas da seguinte forma:
  - **valor de saída de tempo** (0x00000001 através de 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />A seleção TX_WAIT_FOREVER faz com que o fio de chamada suspenda indefinidamente até que o Servidor HTTP responda ao pedido.<br />A seleção de um valor numérico (0x1-0xFFFFFFFE) especifica o número máximo de temporizadores para permanecer suspenso enquanto se aguarda a resposta do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso mensagem de início do cliente HTTP GET
- **NX_HTTP_ERROR** (0xE0) Erro interno do cliente HTTP
- **NX_HTTP_NOT_READY** (0xEA) HTTP Cliente não está pronto
- **NX_HTTP_FAILED** (0xE2) HTTP Erro do cliente que comunica com o servidor HTTP.
- **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome inválido e/ou senha.
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço.

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  NX_NULL, 0, “myname”, “mypassword”, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5), “/TEST.HTM”,
                                  POST_MESSAGE, sizeof(POST_MESSAGE),
                                  “myname”, “mypassword”, 1000);
 
/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```


## <a name="nx_http_client_get_start_extended"></a>nx_http_client_get_start_extended

### <a name="start-an-http-get-request"></a>Inicie um pedido HTTP GET

**Protótipo**

```c
UINT nx_http_client_get_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *input_ptr, UINT input_size, CHAR *username,
     UINT username_length, CHAR *password, UINT password_length,
     ULONG wait_option);
```

**Descrição**

Este serviço tenta obter o recurso especificado por "recurso" na instância do cliente HTTP anteriormente criada. Se esta rotina voltar NX_SUCCESS, a aplicação pode então fazer várias chamadas para *nx_http_client_get_packet* para recuperar pacotes de dados correspondentes ao conteúdo de recursos solicitado.

Note que o string de recursos pode referir-se a um ficheiro local, por exemplo, "/index.htm" ou pode referir-se a outro URL, por exemplo, `http://abc.website.com/index.htm` se o SERVIDOR HTTP indicar que suporta pedidos GET de referência.

Este serviço substitui *nx_http_client_get_start()*. Requer que o chamador especifique o comprimento do recurso, nome de utilizador e senha.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **ip_address** Endereço IP do servidor HTTP.
- **recurso** Ponteiro para cadeia URL para recurso solicitado.
- **resource_length** Comprimento da cadeia URL para recurso solicitado.
- **input_ptr** Ponteiro para dados adicionais para o pedido GET. Isto é opcional. Se válido, a entrada especificada é colocada na área de conteúdo da mensagem e um POST é utilizado em vez de uma operação GET.
- **input_size** Número de bytes em entrada adicional opcional apontada por input_ptr.
- **nome de utilizador** Ponteiro para o nome de utilizador opcional para a autenticação.
- **username_length** Duração do nome de utilizador opcional para autenticação.
- **senha** Ponteiro para senha opcional para autenticação.
- **password_length** Duração da senha opcional para autenticação.
- **wait_option** Define quanto tempo o serviço irá esperar pelo pedido de início do cliente HTTP. As opções de espera são definidas da seguinte forma:
  - **valor de saída de tempo** (0x00000001 através de 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />A seleção TX_WAIT_FOREVER faz com que o fio de chamada suspenda indefinidamente até que o Servidor HTTP responda ao pedido.<br />A seleção de um valor numérico (0x1-0xFFFFFFFE) especifica o número máximo de temporizadores para permanecer suspenso enquanto se aguarda a resposta do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso mensagem de início do cliente HTTP GET
- **NX_HTTP_ERROR** (0xE0) Erro interno do cliente HTTP
- **NX_HTTP_NOT_READY** (0xEA) HTTP Cliente não está pronto
- **NX_HTTP_FAILED** (0xE2) HTTP Erro do cliente que comunica com o servidor HTTP.
- **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome inválido e/ou senha.
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço.

**Permitido a partir de**

Fios

**Exemplo**
            
```c
/* Start the GET operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5),
                                           “/TEST.HTM”,
                                           9, NX_NULL, 0, “myname”, 6,
                                           “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the GET request for TEST.HTM is started and is so
far successful. The client must now call *nx_http_client_get_packet* multiple
times to retrieve the content associated with TEST.HTM. */

#define POST_MESSAGE   “Add this data to the message content”

/* Start the POST operation on the HTTP Client “my_client.”  */
status =  nx_http_client_get_start_extended(&my_client, IP_ADDRESS(1,2,3,5), 
                                           “/TEST.HTM”,
                                           9, POST_MESSAGE, sizeof(POST_MESSAGE),
                                           “myname”, 6, “mypassword”, 10, 1000);

/* If status is NX_SUCCESS, the POST_MESSAGE is added to the message in the POST 
request for TEST.HTM and successfully sent. */
```

## <a name="nx_http_client_get_packet"></a>nx_http_client_get_packet

### <a name="get-next-resource-data-packet"></a>Obtenha o próximo pacote de dados de recursos

**Protótipo**

```c
UINT nx_http_client_get_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET **packet_ptr,
                              ULONG wait_option);
```

**Descrição**

Este serviço recupera o próximo pacote de conteúdo do recurso solicitado pela *chamada nx_http_client_get_start* anterior. Devem ser feitas sucessivas chamadas para esta rotina até que seja recebida a situação de devolução do NX_HTTP_GET_DONE.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **packet_ptr** Destino para ponteiro de pacotes que contenha conteúdo parcial de recursos.
- **wait_option** Define quanto tempo o serviço irá esperar pelo pacote http Cliente. As opções de espera são definidas da seguinte forma:
  - **valor de tempo limite** (0x00000001 através de 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />A seleção TX_WAIT_FOREVER faz com que o fio de chamada suspenda indefinidamente até que o Servidor HTTP responda ao pedido.<br />A seleção de um valor numérico (0x1-0xFFFFFFFE) especifica o número máximo de temporizadores para permanecer suspenso enquanto se aguarda a resposta do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) pacote de cliente HTTP com sucesso.
- **NX_HTTP_GET_DONE** (0xEC) HTTP O pacote de obter do cliente está feito
- **NX_HTTP_NOT_READY** (0xEA) HTTP Cliente não está em modo get.
- **NX_HTTP_BAD_PACKET_LENGTH** (0xED) Comprimento do pacote inválido
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Get the next packet of resource content on the HTTP Client “my_client.”
Note that the nx_http_client_get_start routine must have been called
previously. */
status = nx_http_client_get_packet(&my_client, &next_packet, 1000);
 
/* If status is NX_SUCCESS, the next packet of content is pointed to by 
“next_packet”. */
```

## <a name="nx_http_client_put_start"></a>nx_http_client_put_start

### <a name="start-an-http-put-request"></a>Inicie um pedido HTTP PUT 

**Protótipo**

```c
UINT nx_http_client_put_start(NX_HTTP_CLIENT *client_ptr,
                             ULONG ip_address, CHAR *resource,
                             CHAR *username, CHAR *password,
                             ULONG total_bytes, ULONG wait_option);
```

**Descrição**

Este serviço tenta enviar um pedido PUT com o recurso especificado para o Servidor HTTP no endereço IP fornecido. Se esta rotina for bem sucedida, o código de aplicação deve escoar chamadas sucessivas para a rotina *nx_http_client_put_packet* para enviar os conteúdos de recursos para o Servidor HTTP.

Note que o string de recursos pode referir-se a um ficheiro local, por exemplo, "/index.htm" ou pode referir-se a outro URL, por exemplo, `http://abc.website.com/index.htm` se o SERVIDOR HTTP indicar que suporta pedidos PUT de referência.

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para *nx_http_client_put_start_extended()*.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **ip_address** Endereço IP do servidor HTTP.
- **recurso** Ponteiro para cadeia URL para recurso para enviar para Server.
- **nome de utilizador** Ponteiro para o nome de utilizador opcional para a autenticação.
- **senha** Ponteiro para senha opcional para autenticação.
- **total_bytes** Total de bytes de recursos sendo enviados. Note que o comprimento combinado de todos os pacotes enviados através de chamadas *subsequentes* para nx_http_client_put_packet deve ser igual a este valor.
- **wait_option** Define quanto tempo o serviço vai esperar pelo início do HTTP Client PUT. As opções de espera são definidas da seguinte forma:
  - **valor de tempo limite** (0x00000001 através de 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />A seleção TX_WAIT_FOREVER faz com que o fio de chamada suspenda indefinidamente até que o Servidor HTTP responda ao pedido.<br />A seleção de um valor numérico (0x1-0xFFFFFFFE) especifica o número máximo de temporizadores para permanecer suspenso enquanto se aguarda a resposta do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso pedido PUT
- **NX_HTTP_USERNAME_TOO_LONG**
- **(0xF1) Nome de utilizador demasiado grande para tampão**
- **NX_HTTP_NOT_READY** (0xEA) HTTP Cliente não está pronto
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_SIZE_ERROR (0x09) Tamanho total inválido de recursos
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                 “/TEST.HTM”, “myname”, “mypassword”, 20, 
                                 NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_start_extended"></a>nx_http_client_put_start_extended

### <a name="start-an-http-put-request"></a>Inicie um pedido HTTP PUT

**Protótipo**

```c
UINT nx_http_client_put_start_extended(NX_HTTP_CLIENT *client_ptr,
     ULONG ip_address, CHAR *resource, UINT resource_length,
     CHAR *username,UINT username_length, CHAR *password,
     UINT password_length, ULONG total_bytes, ULONG wait_option);
```

**Descrição**

Este serviço tenta enviar um pedido PUT com o recurso especificado para o Servidor HTTP no endereço IP fornecido. Se esta rotina for bem sucedida, o código de aplicação deve escoar chamadas sucessivas para a rotina *nx_http_client_put_packet* para enviar os conteúdos de recursos para o Servidor HTTP.

Note que o string de recursos pode referir-se a um ficheiro local, por exemplo, "/index.htm" ou pode referir-se a outro URL, por exemplo, `http://abc.website.com/index.htm` se o SERVIDOR HTTP indicar que suporta pedidos PUT de referência.

Este serviço substitui *nx_http_client_put_start()*. Requer que o chamador especifique o comprimento do recurso, nome de utilizador e senha.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **ip_address** Endereço IP do servidor HTTP.
- **recurso** Ponteiro para cadeia URL para recurso para enviar para Server.
- **resource_length** Comprimento da cadeia URL para o recurso enviar para o Servidor.
- **nome de utilizador** Ponteiro para o nome de utilizador opcional para a autenticação.
- **username_length** Duração do nome de utilizador opcional para autenticação.
- **senha** Ponteiro para senha opcional para autenticação.
- **password_length** Duração da senha opcional para autenticação.
- **total_bytes** Total de bytes de recursos sendo enviados. Note que o comprimento combinado de todos os pacotes enviados através de chamadas *subsequentes* para nx_http_client_put_packet deve ser igual a este valor.
- **wait_option** Define quanto tempo o serviço vai esperar pelo início do HTTP Client PUT. As opções de espera são definidas da seguinte forma:
  - **valor de tempo limite** (0x00000001 através de 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />A seleção TX_WAIT_FOREVER faz com que o fio de chamada suspenda indefinidamente até que o Servidor HTTP responda ao pedido.<br />A seleção de um valor numérico (0x1-0xFFFFFFFE) especifica o número máximo de temporizadores para permanecer suspenso enquanto se aguarda a resposta do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso pedido PUT
- **NX_HTTP_USERNAME_TOO_LONG** (0xF1) Nome de utilizador demasiado grande para tampão
- **NX_HTTP_NOT_READY** (0xEA) HTTP Cliente não está pronto
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_SIZE_ERROR (0x09) Tamanho total inválido de recursos
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Start an HTTP PUT to place the 20-byte resource “/TEST.HTM” on the HTTP 
Server at IP address 1.2.3.5. */
status = nx_http_client_put_start_extended(&my_client, IP_ADDRESS(1, 2, 3, 5),
                                          “/TEST.HTM”, 9, “myname”, 6, 
                                          “mypassword”, 
                                          10, 20, NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the PUT operation for TEST.HTM has successfully 
been started. */
```

## <a name="nx_http_client_put_packet"></a>nx_http_client_put_packet

### <a name="send-next-resource-data-packet"></a>Enviar o próximo pacote de dados de recursos

**Protótipo**

```c
UINT nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                              NX_PACKET *packet_ptr,
                              ULONG wait_option);
```

**Descrição**

Este serviço tenta enviar o próximo pacote de conteúdo de recursos para o servidor HTTP. Note que esta rotina deve ser chamada repetidamente até que o comprimento combinado dos pacotes enviados seja igual ao "total_bytes" especificado na chamada *nx_http_client_put_start anterior().*

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **packet_ptr** Ponteiro para o próximo conteúdo do recurso a ser enviado para o Servidor HTTP.
- **wait_option** Define quanto tempo o serviço esperará internamente para processar o pacote HTTP Client PUT. As opções de espera são definidas da seguinte forma:
  - **valor de tempo limite** (0x00000001 através de 0xFFFFFFFE)
  - **TX_WAIT_FOREVER** (0xFFFFFFFF)<br />A seleção TX_WAIT_FOREVER faz com que o fio de chamada suspenda indefinidamente até que o Servidor HTTP responda ao pedido.<br /> A seleção de um valor numérico (0x1-0xFFFFFFFE) especifica o número máximo de temporizadores para permanecer suspenso enquanto se aguarda a resposta do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso o pacote do cliente HTTP.
- **NX_HTTP_NOT_READY** (0xEA) HTTP Cliente não está pronto
- **NX_HTTP_REQUEST_UNSUCCESSFUL_CODE** (0xEE) Recebeu código de erro do servidor** -**NX_HTTP_BAD_PACKET_LENGTH** (0xED) Comprimento do pacote inválido
- **NX_HTTP_AUTHENTICATION_ERROR** (0xEB) Nome inválido e/ou senha
- **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) O servidor responde antes de PUT estar completo
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_INVALID_PACKET (0x12) Pacote demasiado pequeno para cabeçalho TCP
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Send a 20-byte packet representing the content of the resource
“/TEST.HTM” to the HTTP Server. */
status = nx_http_client_put_packet(NX_HTTP_CLIENT *client_ptr,
                                  NX_PACKET *packet_ptr,
                                  ULONG wait_option);

/* If status is NX_SUCCESS, the 20-byte resource contents of TEST.HTM
has successfully been sent. */
```

## <a name="nx_http_client_set_connect_port"></a>nx_http_client_set_connect_port

### <a name="set-the-connection-port-to-the-server"></a>Definir a porta de ligação para o Servidor

**Protótipo**

```c
UINT nx_http_client_set_connect_port(NX_HTTP_CLIENT *client_ptr,
                                    UINT port);
```

**Descrição**

Este serviço altera a porta de ligação quando se liga ao servidor HTTP à porta especificada em tempo de execução. Caso contrário, a porta de ligação está em padrão para 80. Isto deve ser chamado antes *nx_http_client_get_start*() e *nx_http_client_put_start*() por exemplo, quando o Cliente HTTP se conecta com o Servidor.

**Parâmetros de Entrada**

- **client_ptr** Ponteiro para http bloco de controlo do cliente.
- **porto** Porta para ligação ao Servidor.

**Valores de devolução**

- **NX_SUCCESS** (0x00) Mudou com sucesso a porta de ligação
- **NX_INVALID_PORT** (0x46) Porto excede o máximo (0xFFFF) ou é zero.
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Threads, Inicialização

**Exemplo**

```c
NX_HTTP_CLIENT *client_ptr;

/* Change the connect port to 114. */
status = nx_http_client_set_connect_port(client_ptr, 114);

/* If status is NX_SUCCESS, the connect port is successfully changed. */
```

## <a name="nx_http_server_cache_info_callback_set"></a>nx_http_server_cache_info_callback_set

### <a name="set-the-callback-to-retrieve-url-max-age-and-date"></a>Desa esta hora de chamada para recuperar a idade máxima e a data do URL

**Protótipo**

```c
UINT nx_http_server_cache_info_callback_set(NX_HTTP_SERVER *server_ptr,
                                           UINT (*cache_info_get)(CHAR *resource,
                                           UINT *max_age,
                                           NX_HTTP_SERVER_DATE *date));
```

**Descrição**

Este serviço define o serviço de retorno invocado para obter a idade máxima e última data modificada do recurso especificado.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **cache_info_get** Ponteiro para a chamada
- **max_age** Ponteiro para a idade máxima de um recurso
- **dados** Ponteiro para a última data modificada devolvida.

**Valores de devolução**

- **NX_SUCCESS** (0x00) definiu com sucesso a chamada
- **NX_PTR_ERROR** (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Inicialização

**Exemplo**

```c
NX_HTTP_SERVER my_server;
UINT cache_info_get(CHAR *resource, UINT *max_age,
                   NX_HTTP_SERVER_DATE *last_modified);

/* After my_server is created with nx_http_server_create and before the HTTP
server is set by nx_http_server_start(), set the cache info callback: */
status = nx_http_server_cache_info_callback_set(&my_server, cache_info_get);

/* If status is NX_SUCCESS, the callback was successfully sent. */
```

## <a name="nx_http_server_callback_data_send"></a>nx_http_server_callback_data_send

### <a name="send-data-from-callback-function"></a>Enviar dados da função de retorno

**Protótipo**

```c
UINT nx_http_server_callback_data_send(NX_HTTP_SERVER *server_ptr,
                                      VOID *data_ptr,
                                      ULONG data_length);
```

**Descrição**

Este serviço envia os dados no pacote fornecido da rotina de chamada da aplicação. Isto é normalmente usado para enviar dados dinâmicos associados a pedidos GET/POST. Note que se esta função for utilizada, a rotina de retorno é responsável pelo envio de toda a resposta no formato adequado. Além disso, a rotina de retorno deve devolver o estado de NX_HTTP_CALLBACK_COMPLETED.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **data_ptr** Ponteiro para os dados a enviar.
- **data_length** Número de bytes para enviar.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso dados do Servidor
- **NX_PTR_ERROR** (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
    if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
       (strcmp(resource, "/test.htm") == 0))
    {
        /* Found it, override the GET processing by sending the resource
        contents directly. */

        nx_http_server_callback_data_send(server_ptr,
                                         "HTTP/1.0 200 \r\nContent-Length:
                                         103\r\nContent-Type: text/html\r\n\r\n",
                                         63);
        nx_http_server_callback_data_send(server_ptr, "<HTML>> r\n<HEAD><TITLE>NetX
                                         HTTP Test </TITLE></HEAD>\r\n
                                         <BODY>\r\n<H1>NetX Test Page
                                         </H1>\r\n</BODY>> r\n</HTML>\r\n", 103);
        /* Return completion status. */
        return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_generate_response_header"></a>nx_http_server_callback_generate_response_header

### <a name="create-a-response-header-in-a-callback-function"></a>Criar um cabeçalho de resposta numa função de retorno

**Protótipo**

```c
UINT nx_http_server_callback_generate_response_header(NX_HTTP_SERVER *server_ptr,
     NX_PACKET **packet_pptr, CHAR *status_code, UINT content_length,
     CHAR *content_type, CHAR* additional_header);
```

**Descrição**

Este serviço chama a função interna _ *nx_http_server_generate_response_header* quando o servidor HTTP responde ao Cliente obter, colocar e apagar pedidos. Destina-se a ser utilizado em funções de chamada do servidor HTTP quando a aplicação do servidor HTTP estiver a desenhar a sua resposta ao Cliente.

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para *nxd_http_server_callback_generate_response_header_extended()*.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **packet_pptr** Ponteiro um ponteiro de pacote atribuído para mensagem
- **status_code** Indicar o estado do recurso. Exemplos:
- **NX_HTTP_STATUS_OK**
- **NX_HTTP_STATUS_MODIFIED**
- **NX_HTTP_STATUS_INTERNAL_ERROR**
- **content_length** Tamanho do conteúdo em bytes
- **content_type** Tipo de HTTP, por exemplo, "texto/planície"
- **additional_header** Ponteiro para texto adicional do cabeçalho

**Valores de devolução**

- **NX_SUCCESS** (0x00) Com sucesso criado cabeçalho HTML
- **NX_PTR_ERROR** (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
CHAR demotestbuffer[] = “<html>\r\n\r\n<head> r\n\r\n<title>Main                 \
                        Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n  \ 
                        </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
the HTTP server in nx_http_server_create, creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *recv_packet_ptr)
{
    NX_PACKET     *sresp_packet_ptr;
    ULONG         string_length;
    CHAR          temp_string[30];
    ULONG         length = 0;

        length = sizeof(demotestbuffer) - 1;

/* Derive the client request type from the client request. */
   string_length = (ULONG) nx_http_server_type_get(server_ptr, server_ptr ->
                   nx_http_server_request_resource, temp_string);

/* Null terminate the string. */
   temp_string[temp] = 0;

/* Now build a response header with server status is OK and no additional header info. */
   status = nx_http_server_callback_generate_response_header(http_server_ptr,
            &resp_packet_ptr, NX_HTTP_STATUS_OK,
            length, temp_string, NX_NULL);

/* If status is NX_SUCCESS, the header was successfully appended. */

/* Now add data to the packet. */
   status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
            length, server_ptr >>
            nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
   if (status != NX_SUCCESS)
   {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

/* Now send the packet! */
   status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
            resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);

   if (status != NX_SUCCESS)
   {
        nx_packet_release(resp_packet_ptr);
        return status;
    }
/* Let HTTP server know the response has been sent. */
   return NX_HTTP_CALLBACK_COMPLETED;
}
```

## <a name="nx_http_server_callback_generate_response_header_extended"></a>nx_http_server_callback_generate_response_header_extended

### <a name="create-a-response-header-in-a-callback-function"></a>Criar um cabeçalho de resposta numa função de retorno

**Protótipo**

```c
UINT nx_http_server_callback_generate_response_header_extended(
     NX_HTTP_SERVER *server_ptr,
     NX_PACKET **packet_pptr,
     CHAR *status_code, UINT status_code_length,
     UINT content_length,
     CHAR *content_type, UINT content_type_length,
     CHAR *additional_header,
     UINT additional_header_length);
```

**Descrição**

Este serviço chama a função interna _ *nx_http_server_generate_response_header()* quando o servidor HTTP responde a solicitações de obter, colocar e apagar pedidos do Cliente. Destina-se a ser utilizado em funções de chamada do servidor HTTP quando a aplicação do servidor HTTP estiver a desenhar a sua resposta ao Cliente.

Este serviço substitui *nx_http_server_callback_generate_response_header()*. Esta versão fornece informações adicionais de comprimento à função de retorno.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **packet_pptr** Ponteiro um ponteiro de pacote atribuído para mensagem
- **status_code** Indicar o estado do recurso. Exemplos:
  - **NX_HTTP_STATUS_OK**
  - **NX_HTTP_STATUS_MODIFIED**
  - **NX_HTTP_STATUS_INTERNAL_ERROR**
- **status_code** Duração do código de estado
- **content_length** Tamanho do conteúdo em bytes
- **content_type** Tipo de HTTP, por exemplo, "texto/planície"
- **content_type_length** Comprimento do tipo HTTP
- **additional_header** Ponteiro para texto adicional do cabeçalho
- **additional_header_length** Comprimento do texto adicional do cabeçalho

**Valores de devolução**

- **NX_SUCCESS** (0x00) Cabeçalho criado com sucesso
- **NX_PTR_ERROR** (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
  CHAR demotestbuffer[] = “<html>\r\n\r\n<head>\r\n\r\n<title>Main                    \
                          Window</title>\r\n</head>\r\n\r\n<body>Test message\r\n     \
                          </body>\r\n</html>\r\n";

/* my_request_notify is the application request notify callback registered with
   the HTTP server in nx_http_server_create, creates a response to the received
   Client request. */

   UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, NX_PACKET *recv_packet_ptr)
   {
     NX_PACKET *sresp_packet_ptr;
     ULONG string_length;
     CHAR temp_string[30];
     ULONG length = 0;

     length = sizeof(demotestbuffer) - 1;

    /* Derive the client request type from the client request. */
       string_length = (ULONG) nx_http_server_type_retrieve(server_ptr, server_ptr >>
                       nx_http_server_request_resource, temp_string,
                       sizeof(temp_string));

    /* Null terminate the string. */
       temp_string[temp] = 0;

    /* Now build a response header with server status is OK and no additional header
      info. */
      status = nx_http_server_callback_generate_response_header_extended(
               http_server_ptr, &resp_packet_ptr, NX_HTTP_STATUS_OK,
               sizeof(NX_HTTP_STATUS_OK) - 1, length,
               temp_string, string_length, NX_NULL, 0);

    /* If status is NX_SUCCESS, the header was successfully appended. */

    /* Now add data to the packet. */
       status = nx_packet_data_append(resp_packet_ptr, &demotestbuffer[0],
                length, server_ptr ->
                nx_http_server_packet_pool_ptr, NX_WAIT_FOREVER);
    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }

    /* Now send the packet! */
       status = nx_tcp_socket_send(&(server_ptr -> nx_http_server_socket),
                                   resp_packet_ptr, NX_HTTP_SERVER_TIMEOUT_SEND);
    if (status != NX_SUCCESS)
    {
        nx_packet_release(resp_packet_ptr);
        return status;
    }
    /* Let HTTP server know the response has been sent. */
       return NX_HTTP_CALLBACK_COMPLETED;
}
```

## <a name="nx_http_server_callback_packet_send"></a>nx_http_server_callback_packet_send

### <a name="send-an-http-packet-from-callback-function"></a>Envie um pacote HTTP da função de retorno

**Protótipo**

```c
UINT nx_http_server_callback_packet_send(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr);
```

**Descrição**

Este serviço envia uma resposta completa do servidor HTTP a partir de uma chamada HTTP. O servidor HTTP enviará o pacote com o NX_HTTP_SERVER _TIMEOUT_SEND. O cabeçalho HTTP e os dados devem ser anexados ao pacote. Se o estado de devolução indicar um erro, a aplicação HTTP deve libertar o pacote.

A chamada deve voltar NX_HTTP_CALLBACK_COMPLETED.

Consulte *nx_http_server_callback_generate_response_header para* um exemplo mais detalhado.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para bloco de controlo do servidor HTTP
- **packet_ptr** Ponteiro para o pacote para enviar

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso o pacote do servidor HTTP
- **NX_PTR_ERROR** (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
/* The packet is appended with HTTP header and data and is ready to send to the
Client directly. */

   status = nx_http_server_callback_response_send**(server_ptr, packet_ptr);
   
   if (status != NX_SUCCESS)
   {
        nx_packet_release(packet_ptr);
   }
    return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_callback_response_send"></a>nx_http_server_callback_response_send

### <a name="send-response-from-callback-function"></a>Enviar resposta da função de retorno

**Protótipo**

```c
UINT nx_http_server_callback_response_send(NX_HTTP_SERVER *server_ptr,
     CHAR *header, CHAR *information, CHAR additional_info);
```

**Descrição**

Este serviço envia as informações de resposta fornecidas da rotina de retorno da aplicação. Isto é normalmente usado para enviar respostas personalizadas associadas a pedidos GET/POST. Note que se esta função for utilizada, a rotina de retorno deve devolver o estado de NX_HTTP_CALLBACK_COMPLETED.

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para *nx_http_server_callback_response_send_extended().*

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **cabeçalho** Ponteiro para a corda do cabeçalho de resposta.
- **informação** Ponteiro para a cadeia de informação.
- **additional_info** Ponteiro para a cadeia de informações adicionais.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso a resposta do servidor HTTP

**Permitido a partir de**

Fios

**Exemplo**

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
       if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
          (strcmp(resource, "/test.htm") == 0))
       {

            /* In this example, we will complete the GET processing with
               a resource not found response. */
               nx_http_server_callback_response_send(server_ptr,
                                                    "HTTP/1.0 404 ",
                                                    "NetX HTTP Server unable to find
                                                    file: ", resource);
            /* Return completion status. */
               return(NX_HTTP_CALLBACK_COMPLETED);
        }
        return(NX_SUCCESS);
}
```

## <a name="nx_http_server_callback_response_send_extended"></a>nx_http_server_callback_response_send_extended

### <a name="send-response-from-callback-function"></a>Enviar resposta da função de retorno

**Protótipo**

```c
UINT nx_http_server_callback_response_send_extended(
     NX_HTTP_SERVER *server_ptr, CHAR *heade
     UINT header_length, CHAR *information,
     UINT information_length, CHAR *additional_info,
     UINT additional_info_length);
```

**Descrição**

Este serviço envia as informações de resposta fornecidas da rotina de retorno da aplicação. Isto é normalmente usado para enviar respostas personalizadas associadas a pedidos GET/POST. Note que se esta função for utilizada, a rotina de retorno deve devolver o estado de NX_HTTP_CALLBACK_COMPLETED.

Este serviço substitui *nx_http_server_callback_response_send.* Esta versão requer informação de comprimento como argumento de entrada.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **cabeçalho** Ponteiro para a corda do cabeçalho de resposta.
- **header_length** Comprimento da corda do cabeçalho de resposta.
- **informação** Ponteiro para a cadeia de informação.
- **information_length** Comprimento da cadeia de informação.
- **additional_info** Ponteiro para a cadeia de informações adicionais.
- **additional_info_length** Comprimento da cadeia de informações adicionais.

**Valores de devolução**

- **NX_SUCCESS** (0x00) enviou com sucesso a resposta do Servidor

**Permitido a partir de**

Fios

**Exemplo**

```c
UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

    /* Look for the test resource! */
       if ((request_type == NX_HTTP_SERVER_GET_REQUEST) &&
          (strcmp(resource, "/test.htm") == 0))
    {
        /* In this example, we will complete the GET processing with
           a resource not found response. */
           nx_http_server_callback_response_send_extended(server_ptr,
                                                         "HTTP/1.0 404 ", 12,
                                                         "NetX HTTP Server unable to find
                                                         file: ", 38, resource, 9);
        /* Return completion status. */
           return(NX_HTTP_CALLBACK_COMPLETED);
    }
    return(NX_SUCCESS);
}
```

## <a name="nx_http_server_content_get"></a>nx_http_server_content_get

### <a name="get-content-from-the-request"></a>Obtenha conteúdo do pedido

**Protótipo**

```c
UINT nx_http_server_content_get(NX_HTTP_SERVER *server_ptr,
                                NX_PACKET *packet_ptr,
                                ULONG byte_offset,
                                CHAR *destination_ptr,
                                UINT destination_size,
                                UINT *actual_size);
```

**Descrição**

Este serviço tenta recuperar a quantidade especificada de conteúdo do pedido do CLIENTE POST ou PUT HTTP. Deve ser chamado a partir do pedido da aplicação notificar a chamada especificada durante a criação do SERVIDOR HTTP *(nx_http_server_create()*).

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para nx_http_server_content_get_extended().

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **packet_ptr** Ponteiro para o pacote de pedido do cliente HTTP. Note que este pacote não deve ser divulgado pelo pedido notificar o retorno.
- **byte_offset** Número de bytes para compensar na área de conteúdo.
- **destination_ptr** Ponteiro para a área de destino para o conteúdo.
- **destination_size** Número máximo de bytes disponíveis na área de destino.
- **atual_size** Ponteiro para a variável de destino que será definida para o tamanho real do conteúdo copiado.

**Valores de devolução**

- **NX_SUCCESS** (0x00) conteúdo satisfatório do servidor HTTP
- **NX_HTTP_ERROR** (0xE0) HTTP Erro interno do servidor
- **NX_HTTP_DATA_END** (0xE7) Conteúdo de fim do pedido
- **NX_HTTP_TIMEOUT** (0xE1) HTTP Servidor tempo limite para obter o próximo pacote de conteúdo
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get(&my_server, packet_ptr,
                                   0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_get_extended"></a>nx_http_server_content_get_extended

### <a name="get-content-from-the-requestsupports-zero-length-content-length"></a>Obtenha conteúdo a partir do pedido/suporta comprimento de conteúdo zero comprimento

**Protótipo**

```c
UINT nx_http_server_content_get_extended(NX_HTTP_SERVER *server_ptr,
                                        NX_PACKET *packet_ptr,
                                        ULONG byte_offset,
                                        CHAR *destination_ptr,
                                        UINT destination_size,
                                        UINT *actual_size);
```

**Descrição**

Este serviço é quase idêntico ao *nx_http_server_content_get()*; tenta recuperar a quantidade especificada de conteúdo do pedido do CLIENTE POST ou PUT HTTP. No entanto, trata os pedidos com contentamento comprimento de valor zero ('pedido vazio') como um pedido válido. Deve ser chamado a partir do pedido da aplicação notificar a chamada especificada durante a criação do SERVIDOR HTTP *(nx_http_server_create()*).

Este serviço substitui *nx_http_server_content_get.* Esta versão requer que o chamador forneça informações adicionais sobre o comprimento.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **packet_ptr** Ponteiro para o pacote de pedido do cliente HTTP. Note que este pacote não deve ser divulgado pelo pedido notificar o retorno.
- **byte_offset** Número de bytes para compensar na área de conteúdo.
- **destination_ptr** Ponteiro para a área de destino para o conteúdo.
- **destination_size** Número máximo de bytes disponíveis na área de destino.
- **atual_size** Ponteiro para a variável de destino que será definida para o tamanho real do conteúdo copiado.

**Valores de devolução**

- **NX_SUCCESS** (0x00) conteúdo HTTP bem sucedido obtém
- **NX_HTTP_ERROR** (0xE0) HTTP Erro interno do servidor
- **NX_HTTP_DATA_END** (0xE7) Conteúdo de fim do pedido
- **NX_HTTP_TIMEOUT** (0xE1) HTTP Servidor tempo limite na obtenção do próximo pacote
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Assuming we are in the application’s request notify callback
routine, retrieve up to 100 bytes of content starting at offset 0. */
status = nx_http_server_content_get_extended(&my_server, packet_ptr,
                                            0, my_buffer, 100, &actual_size);

/* If status is NX_SUCCESS, “my_buffer” contains “actual_size” bytes of
request content. */
```

## <a name="nx_http_server_content_length_get"></a>nx_http_server_content_length_get

### <a name="get-length-of-content-in-the-request"></a>Obtenha a duração do conteúdo no pedido

**Protótipo**

```c
UINT nx_http_server_content_length_get(NX_PACKET *packet_ptr);
```
**Descrição**

Este serviço tenta recuperar o comprimento do conteúdo HTTP no pacote fornecido. Se não houver conteúdo HTTP, esta rotina devolve um valor de zero. Deve ser chamado a partir do pedido da aplicação notificar a chamada especificada durante a criação do SERVIDOR HTTP *(nx_http_server_create()*).

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para nx_http_server_content_length_get_extended().

**Parâmetros de Entrada**

- **packet_ptr** Ponteiro para o pacote de pedido do cliente HTTP. Note que este pacote não deve ser divulgado pelo pedido notificar o retorno.

**Valores de devolução**

- **comprimento do conteúdo** Por engano, um valor de zero é devolvido

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
length = nx_http_server_content_length_get(packet_ptr);

/* The “length” variable now contains the length of the HTTP Client
request content area. */
```

## <a name="nx_http_server_content_length_get_extended"></a>nx_http_server_content_length_get_extended

### <a name="get-length-of-content-in-the-requestsupports-content-length-of-zero-value"></a>Obtenha o comprimento do conteúdo no pedido/suporta o comprimento do conteúdo de valor zero

**Protótipo**

```c
UINT nx_http_server_content_length_get_extended(NX_PACKET *packet_ptr,
                                               UINT *content_length);
```

**Descrição**

Este serviço é semelhante ao *nx_http_server_content_length_get;;* tentativas de recuperar o comprimento do conteúdo HTTP no pacote fornecido. No entanto, o valor de retorno indica o estado de conclusão bem-sucedido, e o valor real do comprimento é devolvido no ponteiro de entrada content_length. Se não houver conteúdo/comprimento de conteúdo HTTP = 0, esta rotina ainda devolve um estado de conclusão bem-sucedido e o ponteiro de entrada content_length aponta para um comprimento válido (zero). Deve ser chamado a partir do pedido da aplicação notificar a chamada especificada durante a criação do SERVIDOR HTTP *(nx_http_server_create()*).

Este serviço substitui *nx_http_server_content_length_get*().

**Parâmetros de Entrada**

- **packet_ptr** Ponteiro para o pacote de pedido do cliente HTTP. Note que este pacote não deve ser divulgado pelo pedido notificar o retorno.
- **content_length** Ponteiro para valor recuperado do campo Content Length

**Valores de devolução**

- **NX_SUCCESS** (0x00) conteúdo satisfatório do servidor HTTP
- **NX_HTTP_INCOMPLETE_PUT_ERROR** (0xEF) Formato de cabeçalho HTTP impróprio
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Assuming we are in the application’s request notify callback
routine, get the content length of the HTTP Client request. */
ULONG content_length;

status = nx_http_server_content_length_get_extended(packet_ptr, &content_length);

/* If the “status” variable indicates successful completion, the“length” variable
contains the length of the HTTP Client request content area. */
```

## <a name="nx_http_server_create"></a>nx_http_server_create

### <a name="create-an-http-server-instance"></a>Criar uma instância do servidor HTTP

**Protótipo**

```c
UINT nx_http_server_create(NX_HTTP_SERVER *http_server_ptr,
     CHAR *http_server_name, NX_IP *ip_ptr, FX_MEDIA *media_ptr,
     VOID *stack_ptr, ULONG stack_size, NX_PACKET_POOL *pool_ptr,
     UINT (*authentication_check)(NX_HTTP_SERVER *server_ptr,
     UINT request_type, CHAR *resource, CHAR **name,
     CHAR **password, CHAR **realm),
     UINT (*request_notify)(NX_HTTP_SERVER *server_ptr,
     UINT request_type, CHAR *resource, NX_PACKET *packet_ptr));
```

**Descrição**

Este serviço cria uma instância http server, que funciona no contexto da sua própria linha ThreadX. As rotinas de *chamada de authentication_check* e *request_notify* de aplicações opcionais dão ao software de aplicação controlo sobre as operações básicas do Servidor HTTP.

**Parâmetros de Entrada**

- **http_server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.
- **http_server_name** Ponteiro para o nome do servidor HTTP.
- **ip_ptr** Ponteiro para instância IP previamente criada.
- **media_ptr** Ponteiro para a instância de media filex previamente criada.
- **stack_ptr** Ponteiro para a área da pilha de fio do servidor HTTP.
- **stack_size** Ponteiro para o tamanho da pilha de fio do servidor HTTP.
- **authentication_check** Função ponteiro para a rotina de verificação de autenticação da aplicação. Se especificado, esta rotina é chamada para cada pedido do Cliente HTTP. Se este parâmetro for NU, não será efetuada qualquer autenticação.
- **request_notify** Ponteiro de função para pedido de pedido de aplicação notificar rotina. Se especificado, esta rotina é chamada antes do processamento do servidor HTTP do pedido. Isto permite que o nome do recurso seja redirecionado ou campos dentro de um recurso a ser atualizado antes de completar o pedido do Cliente HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) o servidor HTTP com sucesso cria.
- NX_PTR_ERROR (0x07) Inválido HTTP Servidor, IP, meios de comunicação, stack ou ponteiro de piscina de pacotes.
- NX_HTTP_POOL_ERROR (0xE9) A carga útil do pacote não é suficientemente grande para conter o pedido HTTP completo.

**Permitido a partir de**

Inicialização, Threads

**Exemplo**

```c
/* Create an HTTP Server instance called “my_server.” */
status = nx_http_server_create(&my_server, “my server”, &ip_0, &ram_disk,
                              stack_ptr, stack_size, &pool_0,
                              my_authentication_check, my_request_notify);

/* If status equals NX_SUCCESS, the HTTP Server creation was successful. */
```

## <a name="nx_http_server_delete"></a>nx_http_server_delete

### <a name="delete-an-http-server-instance"></a>Excluir uma instância do servidor HTTP

**Protótipo**

```c
UINT nx_http_server_delete(NX_HTTP_SERVER *http_server_ptr);
```

**Descrição**

Este serviço elimina uma instância do servidor HTTP anteriormente criada.

**Parâmetros de Entrada**

- **http_server_ptr** Ponteiro para o bloco de controlo do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) Com sucesso no servidor HTTP
- NX_PTR_ERROR (0x07) Ponteiro do servidor HTTP Inválido
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Delete the HTTP Server instance called “my_server.” */
status = nx_http_server_delete(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server delete was successful. */
```

## <a name="nx_http_server_get_entity_content"></a>nx_http_server_get_entity_content

### <a name="retrieve-the-location-and-length-of-entity-data"></a>Recuperar a localização e a duração dos dados da entidade

**Protótipo**

```c
UINT nx_http_server_get_entity_content(NX_HTTP_SERVER *server_ptr,
                                      NX_PACKET **packet_pptr,
                                      ULONG *available_offset,
                                      ULONG *available_length);
```

**Descrição**

Este serviço determina a localização do início dos dados dentro da atual entidade multipartidária nas mensagens do Cliente recebidas e o comprimento dos dados que não incluem a cadeia de limites. Internamente, o servidor HTTP atualiza as suas próprias compensações para que esta função possa ser novamente chamada no mesmo datagrama do Cliente para mensagens com várias entidades. O ponteiro do pacote é atualizado para o próximo pacote onde a mensagem cliente é um datagrama de vários pacotes.

Note que NX_HTTP_MULTIPART_ENABLE devem ser habilitados a utilizar este serviço.

Consulte *nx_http_server_get_entity_header* para mais detalhes.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o servidor HTTP
- **packet_pptr** Ponteiro para a localização do ponteiro do pacote. Note que o pedido não deve libertar este pacote.
- **available_offset** Ponteiro para compensar os dados da entidade a partir do ponteiro pré-final do pacote
- **available_length** Ponteiro para o comprimento dos dados da entidade

**Valores de devolução**

- **NX_SUCCESS** (0x00) recuperou com sucesso o tamanho e localização do conteúdo da entidade
- **NX_HTTP_BOUNDARY_ALREADY_FOUND** (0xF4) O conteúdo dos marcadores multipartais internos do servidor HTTP já está encontrado
- NX_HTTP_ERROR (0xE0) HTTP Erro interno do servidor
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
NX_HTTP_SERVER my_server;

UINT         offset, length;
NX_PACKET    *packet_ptr;

/* Inside the request notify callback, the HTTP server application first obtains
the entity header to determine details about the multipart data. If
successful, it then calls this service to get the location of entity data: */
status = nx_http_server_get_entity_content(&my_server, &packet_ptr, *offset,
                                          &length);

/* If status equals NX_SUCCESS, offset and location determine the location of the
entity data. */
```

## <a name="nx_http_server_get_entity_header"></a>nx_http_server_get_entity_header

### <a name="retrieve-the-contents-of-entity-header"></a>Recuperar o conteúdo do cabeçalho da entidade

**Protótipo**

```c
UINT nx_http_server_get_entity_header(NX_HTTP_SERVER *server_ptr,
                                     NX_PACKET **packet_pptr,
                                     UCHAR *entity_header_buffer,
                                     ULONG buffer_size);
```

**Descrição**

Este serviço recupera o cabeçalho da entidade no tampão especificado. Internamente HTTP Server atualiza os seus próprios ponteiros para localizar a próxima entidade multipartida num datagrama do Cliente com vários cabeçalhos de entidade. O ponteiro do pacote é atualizado para o próximo pacote onde a mensagem cliente é um datagrama de vários pacotes.

Note que NX_HTTP_MULTIPART_ENABLE devem ser habilitados a utilizar este serviço.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o servidor HTTP
- **packet_pptr** Ponteiro para a localização do ponteiro do pacote. Note que o pedido não deve libertar este pacote.
- **entity_header_buffer** Ponteiro para localização para armazenar cabeçalho da entidade
- **buffer_size** Tamanho do tampão de entrada

**Valores de devolução**

- **NX_SUCCESS** (0x00) conseguiu recuperar o chefe da entidade
- **NX_HTTP_NOT_FOUND (0xE6)** Campo de cabeçalho de entidade não encontrado
- **NX_HTTP_TIMEOUT (0xE1)** O tempo expirou para receber o próximo pacote para mensagem de cliente multipacket 
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço
- NX_HTTP_ERROR (0xE0) Erro HTTP Interno

**Permitido a partir de**

Fios

**Exemplo**

```c
/* my_request_notify* is the application request notify callback registered with
the HTTP server in *nx_http_server_create,* creates a response to the received
Client request. */

UINT my_request_notify(NX_HTTP_SERVER *server_ptr, UINT request_type,
                      CHAR *resource, NX_PACKET *packet_ptr)
{

NX_PACKET     *sresp_packet_ptr;
UINT          offset, length;**
NX_PACKET     *response_pkt;
UCHAR         buffer[1440];

/* Process multipart data. */
if(request_type == NX_HTTP_SERVER_POST_REQUEST)
{

    /* Get the content header. */
    while(nx_http_server_get_entity_header(server_ptr, &packet_ptr, buffer,
                                          sizeof(buffer)) == NX_SUCCESS)
    {

        /* Header obtained successfully. Get the content data location. */
        while(nx_http_server_get_entity_content(server_ptr, &packet_ptr, &offset,
                                               &length) == NX_SUCCESS)
        {

            /* Write content data to buffer. */
            nx_packet_data_extract_offset(packet_ptr, offset, buffer, length,
                                         &length);
            buffer[length] = 0;
        }
    }
    /* Generate HTTP header. */
    status = nx_http_server_callback_generate_response_header(server_ptr,
             &response_pkt, NX_HTTP_STATUS_OK, 800, "text/html",
             "Server: NetX HTTP 5.3\r\n");

    if(status == NX_SUCCESS)
    {
        if(nx_http_server_callback_packet_send(server_ptr, response_pkt) !=
                                              NX_SUCCESS)
        {
            nx_packet_release(response_pkt);
        }
    }
}
Else
{

        /* Indicate we have not processed the response to client yet.*/        
        return(NX_SUCCESS);
}

/* Indicate the response to client is transmitted. */
return(NX_HTTP_CALLBACK_COMPLETED);
```

## <a name="nx_http_server_gmt_callback_set"></a>nx_http_server_gmt_callback_set

### <a name="set-the-callback-to-obtain-gmt-date-and-time"></a>Desa esta hora de chamada para obter a data e hora de GMT

**Protótipo**

```c
UINT nx_http_server_gmt_callback_set(NX_HTTP_SERVER *server_ptr,
                                    VOID (*gmt_get)(NX_HTTP_SERVER_DATE *date);
```

**Descrição**

Este serviço define a chamada para obter data e hora DE GMT com um servidor HTTP previamente criado. Este serviço é invocado com o servidor HTTP está a criar um cabeçalho em respostas do servidor HTTP ao Cliente.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o servidor HTTP
- **gmt_get** Ponteiro para retorno GMT
- **data** Ponteiro para a data recuperada

**Valores de devolução**

- **NX_SUCCESS** (0x00) definiu com sucesso a chamada
- NX_PTR_ERROR (0x07) Pacote inválido ou ponteiro de parâmetros.

**Permitido a partir de**

Fios

**Exemplo**

```c
NX_HTTP_SERVER my_server;

VOID get_gmt(NX_HTTP_SERVER_DATE *now);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the GMT
retrieve callback: */

status = nx_http_server_gmt_callback_set(&my_server, gmt_get);

/* If status equals NX_SUCCESS, the gmt_get will be called to set the HTTP server
response header date. */
```

## <a name="nx_http_server_invalid_userpassword_notify_set"></a>nx_http_server_invalid_userpassword_notify_set

### <a name="set-the-callback-to-to-handle-invalid-userpassword"></a>Desloque a chamada para lidar com o utilizador/senha inválido

**Protótipo**

```c
UINT nx_http_server_invalid_userpassword_notify_set(
     NX_HTTP_SERVER *http_server_ptr,
     UINT (*invalid_username_password_callback)
     (CHAR *resource,
     ULONG client_address,
     UINT request_type));
```

**Descrição**

Este serviço define a chamada invocada quando um nome de utilizador e palavra-passe inválidos é recebido num Pedido de Cliente obter, colocar ou apagar, seja por digestão ou autenticação básica. O servidor HTTP deve ser previamente criado.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para o servidor HTTP
- **invalid_username_password_callback** Ponteiro para chamada inválida do utilizador/passe
- **recurso** Ponteiro para o recurso especificado pelo cliente
- **client_address** Endereço do cliente
- **request_type** Indica o tipo de pedido do cliente. Pode ser:
  - NX_HTTP_SERVER_GET_REQUEST
  - NX_HTTP_SERVER_POST_REQUEST NX_HTTP_SERVER_HEAD_REQUEST
  - NX_HTTP_SERVER_PUT_REQUEST NX_HTTP_SERVER_DELETE_REQUEST

**Valores de devolução**

- **NX_SUCCESS** (0x00) definiu com sucesso a chamada
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
NX_HTTP_SERVER my_server;
VOID invalid_username_password_callback (NX_ CHAR *resource,
                                        ULONG client_address,
                                        UINT request_type);

/* After the HTTP server is created by calling nx_http_server_create, and before
starting HTTP services when nx_http_server_start is called, set the invalid
username password callback: */

status = nx_http_server_gmt_callback_set(&my_server,
                                        invalid_username_password_callback);

/* If status equals NX_SUCCESS, the invalid_username_password_callback function
will be called when the HTTP server receives an invalid username/password. */
```

## <a name="nx_http_server_mime_maps_additional_set"></a>nx_http_server_mime_maps_additional_set

### <a name="set-additional-mime-maps-for-html"></a>Definir mapas MIME adicionais para HTML 

**Protótipo**

```c
UINT nx_http_server_mime_maps_additional_set(
     NX_HTTP_SERVER *server_ptr,
     NX_HTTP_SERVER_MIME_MAP *mime_maps,
     UINT mime_maps_num);
```

**Descrição**

Este serviço permite ao desenvolvedor de aplicações HTTP adicionar tipos de MIME adicionais dos tipos de MIME predefinidos fornecidos pelo NetX HTTP Server (ver *nx_http_server_get_type* para lista de tipos definidos).

Quando um pedido de cliente é recebido, por exemplo, um pedido GET, o servidor HTTP analisa o tipo de ficheiro solicitado a partir do cabeçalho HTTP utilizando preferencialmente o conjunto de mapas MIME adicional e se não for encontrado, procura uma correspondência no mapa padrão do servidor HTTP. Se não for encontrado qualquer correspondência, o tipo MIME predefine para "texto/planície".

Se a função de notificação de pedido estiver registada no servidor HTTP, o pedido de notificação de chamada pode ligar *nx_http_server_type_get* para analisar o tipo de ficheiro.

**Parâmetros de Entrada**

- **server_ptr** Ponteiros para a instância do servidor HTTP
- **mime_maps** Ponteiro para uma matriz de mapa MIME
- **mime_map_num** Número de mapas MIME na matriz

**Valores de devolução**

- **NX_SUCCESS** (0x00) conjunto de mapas MIME do servidor HTTP Server
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Inicialização, Threads

**Exemplo**

```c
/* my_server is an NX_HTTP_SERVER previously created. */

NX_HTTP_SERVER_MIME_MAP my_mime_maps [2];

static NX_HTTP_SERVER_MIME_MAP my_mime_maps[] =
{
    {"abc", "yourtype/abc"},
    {"xyz", "mytype/xyz"},
};

status = nx_http_server_mime_maps_additional_set(&my_server,
                                                &my_mime_maps[0], 2);

/* If status equals NX_SUCCESS, two additional MIME types are added to the HTTP
server MIME map set.” */
```

## <a name="nx_http_server_packet_content_find"></a>nx_http_server_packet_content_find

### <a name="extract-content-length-and-set-pointer-to-start-of-data"></a>Extrair o comprimento do conteúdo e definir o ponteiro para o início dos dados

**Protótipo**

```c
UINT nx_http_server_packet_content_find(NX_HTTP_SERVER *server_ptr,
                                       NX_PACKET **packet_ptr,
                                       UINT *content_length);
```

**Descrição**

Este serviço extrai o comprimento do conteúdo do cabeçalho HTTP. Também atualiza o pacote fornecido da seguinte forma: o ponteiro pré-final do pacote (início da localização do tampão do pacote para escrever) é definido para o conteúdo HTTP (dados) acabado de passar o cabeçalho HTTP.

Se o início do conteúdo não for encontrado no pacote atual, a função aguarda que o próximo pacote seja recebido utilizando a opção de espera NX_HTTP_SERVER_TIMEOUT_RECEIVE.

Note que isto não deve ser chamado antes de chamar *nx_http_server_get_entity_header()* porque modifica o ponteiro pré-final para além do cabeçalho da entidade.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para a instância do servidor HTTP
- **packet_ptr** Ponteiro para ponter pacote para devolver o pacote com ponteiro pré-final atualizado
- **content_length** Ponteiro para content_length extraído

**Valores de devolução**

- **NX_SUCCESS** (0x00) comprimento de conteúdo HTTP encontrado e pacote atualizado com sucesso
- **NX_HTTP_TIMEOUT** (0xE1) O tempo expirou à espera do próximo pacote
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
/* The HTTP server pointed to by server_ptr is previously created and started.
The server has received a Client request packet, recv_packet_ptr, and the packet
content find service is called from the request notify callback function 
registere with the HTTP server. */

UINT content_length;

status = nx_http_server_packet_content_find(server_ptr, recv_packet_ptr,
                                           &content_length);

/* If status equals NX_SUCCESS, the content length specifies the content length
and the packet pointer prepend pointer is set to the HTTP content (data). */
```

## <a name="nx_http_server_packet_get"></a>nx_http_server_packet_get

### <a name="receive-the-next-http-packet"></a>Receba o próximo pacote HTTP

**Protótipo**

```c
UINT nx_http_server_packet_get(NX_HTTP_SERVER *server_ptr,
                              NX_PACKET **packet_ptr);
```

**Descrição**

Este serviço devolve o próximo pacote recebido na tomada do servidor HTTP. A opção de espera para receber um pacote é NX_HTTP_SERVER_TIMEOUT_RECEIVE.

**Parâmetros de Entrada**

- **server_ptr** Ponteiro para a instância do servidor HTTP
- **packet_ptr** Ponteiro para pacote recebido

**Valores de devolução**

- **NX_SUCCESS** (0x00) recebeu com sucesso o próximo pacote HTTP
- **NX_HTTP_TIMEOUT** (0xE1) O tempo expirou à espera do próximo pacote
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Fios

**Exemplo**

```c
/* The HTTP server pointed to by server_ptr is previously created and started. */

UINT content_length;
NX_PACKET *recv_packet_ptr;

status = nx_http_server_packet_get(server_ptr, &recv_packet_ptr);

/* If status equals NX_SUCCESS, a Client packet is obtained. */
```

## <a name="nx_http_server_param_get"></a>nx_http_server_param_get

### <a name="get-parameter-from-the-request"></a>Obtenha o parâmetro do pedido

**Protótipo**

```c
UINT nx_http_server_param_get(NX_PACKET *packet_ptr,
                             UINT param_number, CHAR *param_ptr,
                             UINT max_param_size);
```

**Descrição**

Este serviço tenta recuperar o parâmetro HTTP URL especificado no pacote de pedido fornecido. Se o parâmetro HTTP solicitado não estiver presente, esta rotina devolve um estado de NX_HTTP_NOT_FOUND. Esta rotina deve ser chamada a partir do pedido da aplicação notificar a chamada especificada durante a criação do SERVIDOR HTTP *(nx_http_server_create).).*

**Parâmetros de Entrada**

- **packet_ptr** Ponteiro para pacote de pedido do cliente HTTP. Note que o pedido não deve libertar este pacote.
- **param_number** Número lógico do parâmetro a partir de zero, da esquerda para a direita na lista de parâmetros.
- **param_ptr** Área de destino para copiar o parâmetro.
- **max_param_size** Tamanho máximo da área de destino do parâmetro.

**Valores de devolução**

- **NX_SUCCESS** (0x00) O parâmetro do servidor HTTP com sucesso obtém
- **NX_HTTP_NOT_FOUND** (0xE6) Parâmetro especificado não encontrado
- **NX_HTTP_IMPROPERLY_TERMINATED_PARAM** (0xF3) Parâmetro de pedido não devidamente terminado
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Assuming we are in the application’s request notify callback
routine, get the first parameter of the HTTP Client request. */

status = nx_http_server_param_get(request_packet_ptr, 0, param_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first parameter can be found
in “param_destination.” */
```

## <a name="nx_http_server_query_get"></a>nx_http_server_query_get

### <a name="get-query-from-the-request"></a>Obtenha consulta a partir do pedido

**Protótipo**

```c
UINT nx_http_server_query_get(NX_PACKET *packet_ptr, UINT query_number,
                             CHAR *query_ptr, UINT max_query_size);
```

**Descrição**

Este serviço tenta recuperar a consulta de URL HTTP especificada no pacote de pedido fornecido. Se a consulta HTTP solicitada não estiver presente, esta rotina devolve um estado de NX_HTTP_NOT_FOUND. Esta rotina deve ser chamada a partir do pedido da aplicação notificar a chamada especificada durante a criação do SERVIDOR HTTP *(nx_http_server_create).).*

**Parâmetros de Entrada**

- **packet_ptr** Ponteiro para pacote de pedido do cliente HTTP. Note que o pedido não deve libertar este pacote.
- **query_number** Número lógico do parâmetro a partir de zero, da esquerda para a direita na lista de consultas.
- **query_ptr** Área de destino para copiar a consulta.
- **max_query_size** Tamanho máximo da área de destino de consulta.

**Valores de devolução**

- **NX_SUCCESS** (0x00) Consulta de servidor HTTP com sucesso obter
- **NX_HTTP_FAILED** (0xE2) Tamanho da consulta muito pequeno.
- **NX_HTTP_NOT_FOUND** (0xE6) Consulta especificada não encontrada
- **NX_HTTP_NO_QUERY_PARSED** (0xF2) Sem consulta no pedido do Cliente
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Assuming we are in the application’s request notify callback
routine, get the first query of the HTTP Client request. */
status = nx_http_server_query_get(request_packet_ptr, 0, query_destination, 30);

/* If status equals NX_SUCCESS, the NULL-terminated first query can be found
in “query_destination.” */
```

##   
nx_http_server_start

### <a name="start-the-http-server"></a>Inicie o servidor HTTP

**Protótipo**

```c
UINT nx_http_server_start(NX_HTTP_SERVER *http_server_ptr);
```

**Descrição**

Este serviço inicia a instância do servidor HTTP anteriormente.

**Parâmetros de Entrada**

- **http_server_ptr** Indicação para a instância do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) início do servidor HTTP com sucesso
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Inicialização, Threads

**Exemplo**

```c
/* Start the HTTP Server instance “my_server.” */
status = nx_http_server_start(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been started. */
```

## <a name="nx_http_server_stop"></a>nx_http_server_stop

### <a name="stop-the-http-server"></a>Parar o servidor HTTP

**Protótipo**

```c
UINT nx_http_server_stop(NX_HTTP_SERVER *http_server_ptr);
```

**Descrição**

Este serviço para a instância do servidor HTTP anteriormente criado. Esta rotina deve ser chamada antes de eliminar uma instância do servidor HTTP.

**Parâmetros de Entrada**

- **http_server_ptr** Indicação para a instância do servidor HTTP.

**Valores de devolução**

- **NX_SUCCESS** (0x00) paragem de servidor HTTP com sucesso
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_CALLER_ERROR (0x11) Inválido deste serviço

**Permitido a partir de**

Fios

**Exemplo**

```c
/* Stop the HTTP Server instance “my_server.” */

status = nx_http_server_stop(&my_server);

/* If status equals NX_SUCCESS, the HTTP Server has been stopped. */
```

## <a name="nx_http_server_type_get"></a>nx_http_server_type_get

### <a name="extract-file-type-from-client-http-request"></a>Extrair o tipo de ficheiro do pedido do Cliente HTTP

**Protótipo**

```c
UINT nx_http_server_type_get(NX_HTTP_SERVER *http_server_ptr,
                            CHAR *name, CHAR *http_type_string);
```

**Descrição**

Este serviço extrai o tipo de pedido HTTP no *http_type_string* tampão e o seu comprimento no valor de retorno a partir do *nome* do tampão de entrada , normalmente o URL. Se não for encontrado nenhum mapa MIME, este desrescume do tipo "texto/planície". Caso contrário, compara o tipo extraído com os mapas MIME padrão do servidor HTTP para uma correspondência. Os mapas MIME predefinidos no Servidor HTTP NetX são:

- html texto/html
- texto/html
- texto txt/planície
- gif imagem/gif
- jpg imagem/jpeg
- ico imagem/x-ícone

Se for fornecido, também procurará um conjunto definido pelo utilizador de mapas MIME adicionais. Consulte *nx_http_server_mime_maps_addtional_set para* obter mais detalhes sobre os mapas definidos pelo utilizador.

Este serviço é precotado. Os desenvolvedores são encorajados a migrar para *nx_http_server_type_get_extended().*

**Parâmetros de Entrada**

- **http_server_ptr** Ponteiros para a instância do servidor HTTP
- **nome** Ponteiro para tampão para pesquisar
- **http_type_string** (Ponteiro para o tipo HTML extraído)

**Valores de devolução**

- **Comprimento da corda em bytes** Não valor zero é sucesso
- **Zero indica erro**

**Permitido a partir de**

Aplicação

**Exemplo**

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

CHAR temp_string[20];
UINT string_length;

/* Extract the HTTP type. */
string_length = nx_http_server_type_get(&my_server_ptr,
                my_server.nx_http_server_request_resource, temp_string);

/* If string_length is non zero, the HTTP string is extracted. */
```

Para um exemplo mais detalhado, consulte a descrição para

*nx_http_server_callback_generate_response_header.*

## <a name="nx_http_server_type_get_extended"></a>nx_http_server_type_get_extended

### <a name="extract-file-type-from-client-http-request"></a>Extrair o tipo de ficheiro do pedido do Cliente HTTP

**Protótipo**

```c
UINT nx_http_server_type_get_extended(
     NX_HTTP_SERVER *http_server_ptr,
     CHAR *name, CHAR *http_type_string,
     UINT http_type_string_max_size);
```

**Descrição**

Este serviço extrai o tipo de pedido HTTP no *http_type_string* tampão e o seu comprimento no valor de retorno a partir do *nome* do tampão de entrada , normalmente o URL. Se não for encontrado nenhum mapa MIME, este desrescume do tipo "texto/planície". Caso contrário, compara o tipo extraído com os mapas MIME padrão do servidor HTTP para uma correspondência. Os mapas MIME padrão no NetX Duo HTTP Server são:

- html texto/html
- texto/html
- texto txt/planície
- gif imagem/gif
- jpg imagem/jpeg
- ico imagem/x-ícone

Se for fornecido, também procurará um conjunto definido pelo utilizador de mapas MIME adicionais. Consulte *nx_http_server_mime_maps_addtional_set para* obter mais detalhes sobre os mapas definidos pelo utilizador.

Este serviço substitui *nx_http_server_type_get.* Esta versão fornece informações adicionais sobre o comprimento.

**Parâmetros de Entrada**

- **http_server_ptr** Ponteiros para a instância do servidor HTTP
- **nome** Ponteiro para tampão para pesquisar
- **name_length** Comprimento do tampão para pesquisar
- **http_type_string** (Ponteiro para o tipo HTML extraído)
- **http_type_string_max_size**

Tamanho do tampão *http_type_string*

**Valores de devolução**

- **Comprimento da corda em bytes** Não valor zero é sucesso<br />Zero indica erro

**Permitido a partir de**

Aplicação

**Exemplo**

```c
/* my_server is a previously created HTTP server, which starts accepting 
client requests when *nx_http_server_start* is called*/

CHAR temp_string[20];
UINT string_length;

/* Get the length of request resource. */
    if (_nx_utility_string_length_check(
       my_server.nx_http_server_request_resource, &resource_length,
       sizeof(my_server.nx_http_server_request_resource) - 1))
    {
        return;
    }
/* Extract the HTTP type. */
string_length = nx_http_server_type_get_extended(&my_server,
                my_server.nx_http_server_request_resource, resource_length,
                temp_string, sizeof(temp_string));

/* If string_length is non zero, the HTTP string is extracted. */
```

Para um exemplo mais detalhado, consulte a descrição para

*nx_http_server_callback_generate_response_header.*

## <a name="nx_http_server_digest_authenticate_notify_set"></a>nx_http_server_digest_authenticate_notify_set

### <a name="set-digest-authenticate-callback-function"></a>Detenda a função de retorno autenticado da digestão

**Protótipo**

```c
UINT nx_http_server_digest_authenticate_notify_set(
     NX_HTTP_SERVER *http_server_ptr,
     UINT (*digest_authenticate_callback)(NX_HTTP_SERVER *server_ptr,
                                         CHAR *name_ptr,
                                         CHAR *realm_ptr,
                                         CHAR *password_ptr,
                                         CHAR *method,
                                         CHAR *authorization_uri,
                                         CHAR *authorization_nc,
                                         CHAR *authorization_cnonce
                                         ));
```

**Descrição**

Este serviço define a chamada invocada quando a digestão autenticada é realizada.

**Parâmetros de Entrada**

- **http_server_ptr** Ponteiros para a instância do servidor HTTP
- **digest_authenticate_callback** Ponteiro para digerir chamada autenticada

**Valores de devolução**

- **NX_SUCCESS** (0x00) definiu com sucesso a chamada
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro
- NX_NOT_SUPPORTED (0x4B) Digerir autenticado não habilitado

**Permitido a partir de**

Aplicação

**Exemplo**

```c
UINT digest_authenticate_callback(NX_HTTP_SERVER *server_ptr, CHAR *name_ptr,
                                 CHAR *realm_ptr, CHAR *password_ptr,
                                 CHAR *method,CHAR *authorization_uri,
                                 CHAR *authorization_nc,
                                 CHAR *authorization_cnonce)
{
    return(NX_SUCCESS);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set the
digest authenticate callback: */

status = nx_http_server_digest_authenticate_notify_set (&my_server,
                                                       digest_authenticate_callback);

/* If status equals NX_SUCCESS, the digest_authenticate_callback function
will be called when the HTTP server performs digest authenticate. */
```

## <a name="nx_http_server_authentication_check_set"></a>nx_http_server_authentication_check_set

### <a name="set-authentication-checking-callback-function"></a>Definir função de verificação de autenticação

**Protótipo**

```c
UINT nx_http_server_authentication_check_set(
     NX_HTTP_SERVER *http_server_ptr,
     UINT (*authentication_check_extended)(
                                          NX_HTTP_SERVER *server_ptr,
                                          UINT request_type,
                                          CHAR *resource,
                                          CHAR **name,
                                          UINT *name_length,
                                          CHAR **password,
                                          UINT *password_length,
                                          CHAR **realm,
                                          UINT *realm_length
                                          ));
```

**Descrição**

Este serviço define a função de retorno de chamada da verificação de autenticação.

**Parâmetros de Entrada**

- **http_server_ptr** Ponteiros para a instância do servidor HTTP
- **authentication_check_extended** Ponteiro para verificação de autenticação da aplicação

**Valores de devolução**

- **NX_SUCCESS** (0x00) definiu com sucesso a chamada
- NX_PTR_ERROR (0x07) Entrada inválida do ponteiro

**Permitido a partir de**

Aplicação

**Exemplo**

```c
static UINT authentication_check_extended(NX_HTTP_SERVER *server_ptr,
                                         UINT request_type, CHAR *resource,
                                         CHAR **name, UINT *name_length,
                                         CHAR **password, 
                                         UINT *password_length,
                                         CHAR **realm, UINT *realm_length)
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */

    *name = "name";
    *password = "password";
    *realm = "NetX Duo HTTP demo";
    *name_length = 4;
    *password_length = 8;
    *realm_length = 18;

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

NX_HTTP_SERVER my_server;

/* After the HTTP server is created by calling nx_http_server_create, and
before starting HTTP services when nx_http_server_start is called, set 
the authentication checking callback: */

nx_http_server_authentication_check_set (&my_server,
                                        authentication_check_extended);
```