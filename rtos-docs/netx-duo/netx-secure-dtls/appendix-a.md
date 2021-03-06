---
title: Apêndice A - Azure RTOS NetX Secure DTLS códigos de devolução/erro
description: Lista os possíveis códigos de erro que podem ser devolvidos pelos serviços DTLS Seguros Azure RTOS NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: reference
ms.service: rtos
ms.openlocfilehash: f4994a5014d3691b4a78f225fb68b475bf5a8cdab630162a94130f321be09da5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782443"
---
# <a name="appendix-a-azure-rtos-netx-secure-dtls-returnerror-codes"></a>Apêndice A: Azure RTOS NetX Secure DTLS códigos de devolução/erro

## <a name="netx-secure-tlsdtls-return-codes"></a>Códigos de devolução NetX Secure TLS/DTLS

O quadro 1 abaixo lista os possíveis códigos de erro que podem ser devolvidos pelos serviços DTLS Seguros Azure RTOS NetX. Note que os serviços também podem devolver códigos de erro UDP ou IP – Os valores TLS começam em 0x101 e os valores TCP/IP/UDP estão abaixo 0x100. Os valores de retorno X.509 começam em 0x181. Consulte a documentação NetX TCP/IP/UDP para obter informações sobre valores de devolução IP e UDP e ver abaixo os valores de X.509.

| **Nome de erro**                                        | **Valor** | **Descrição**                                                                                                                                               |
| ----------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_TLS_SUCCESS                              | 0x00      | A função voltou com sucesso. (O mesmo que NX_SUCCESS).                                                                                                        |
| NX_SECURE_TLS_SESSION_UNINITIALIZED               | 0x101     | Loop principal TLS chamado com tomada não-disserializada.                                                                                                               |
| NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE          | 0x102     | A camada de registo TLS recebeu um tipo de mensagem não reconhecido.                                                                                                       |
| NX_SECURE_TLS_INVALID_STATE                       | 0x103     | Erro interno - estado não reconhecido.                                                                                                                        |
| NX_SECURE_TLS_INVALID_PACKET                      | 0x104     | Erro interno - o pacote recebido não continha dados TLS.                                                                                                    |
| NX_SECURE_TLS_UNKNOWN_CIPHERSUITE                 | 0x105     | A cifrasuite escolhida não é suportada - erro interno para o servidor, para o cliente significa que o hospedeiro remoto enviou uma má cifrasuite (erro ou ataque).            |
| NX_SECURE_TLS_UNSUPPORTED_CIPHER                  | 0x106     | Ao fazer uma encriptação ou desencriptação, a cifra escolhida é desativada ou indisponível.                                                                           |
| NX_SECURE_TLS_HANDSHAKE_FAILURE                   | 0x107     | Algo no processamento de mensagens durante o aperto de mão falhou.                                                                                              |
| NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE           | 0x108     | Um registo de entrada tinha um MAC que não correspondia ao que gerámos.                                                                                         |
| NX_SECURE_TLS_TCP_SEND_FAILED                    | 0x109     | O envio de um registo da TCP de saída falhou por alguma razão.                                                                                                     |
| NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH           | 0x10A     | Uma mensagem recebida tinha um comprimento que estava incorreto (geralmente um comprimento diferente de um no cabeçalho, como em mensagens de certificado)                               |
| NX_SECURE_TLS_BAD_CIPHERSPEC                      | 0x10B     | Uma mensagem ChangeCipherSpec estava incorreta.                                                                                                           |
| NX_SECURE_TLS_INVALID_SERVER_CERT                | 0x10C     | Um certificado de servidor de entrada não analisou corretamente.                                                                                                       |
| NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER          | 0x10D     | Um certificado fornecido por um servidor especificou uma operação de chave pública que não apoiamos.                                                                        |
| NX_SECURE_TLS_NO_SUPPORTED_CIPHERS               | 0x10E     | Recebeu um ClientHello sem cifrasuites suportados.                                                                                                        |
| NX_SECURE_TLS_UNKNOWN_TLS_VERSION                | 0x10F     | Um disco de entrada tinha uma versão TLS que não é reconhecida.                                                                                                   |
| NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION            | 0x110     | Um registo de entrada tinha uma versão TLS válida, mas que não é suportada.                                                                                     |
| NX_SECURE_TLS_ALLOCATE_PACKET_FAILED             | 0x111     | Uma atribuição interna de pacotes para uma mensagem TLS falhou.                                                                                                       |
| NX_SECURE_TLS_INVALID_CERTIFICATE                 | 0x112     | Um certificado X509 não analisou corretamente.                                                                                                                  |
| NX_SECURE_TLS_NO_CLOSE_RESPONSE                  | 0x113     | Durante uma sessão TLS encerrar, não recebeu um CloseNotify do anfitrião remoto.                                                                               |
| NX_SECURE_TLS_ALERT_RECEIVED                      | 0x114     | O anfitrião remoto enviou um alerta, indicando um erro e fechando a ligação.                                                                                |
| NX_SECURE_TLS_FINISHED_HASH_FAILURE              | 0x115     | A mensagem Finish hash recebida não corresponde ao haxixe gerado local - corrupção de aperto de mão.                                                              |
| NX_SECURE_TLS_UNKNOWN_CERT_SIG_ALGORITHM        | 0x116     | Um certificado durante a verificação tinha um algoritmo de assinatura não suportado.                                                                                     |
| NX_SECURE_TLS_CERTIFICATE_SIG_CHECK_FAILED      | 0x117     | Uma verificação de verificação de assinatura de certificado falhou - os dados do certificado não correspondiam à assinatura.                                                                 |
| NX_SECURE_TLS_BAD_COMPRESSION_METHOD             | 0x118     | Recebeu uma mensagem Hello com um método de compressão não suportado.                                                                                              |
| NX_SECURE_TLS_CERTIFICATE_NOT_FOUND              | 0x119     | Numa operação numa lista de certificados, não foi encontrado nenhum certificado correspondente.                                                                                     |
| NX_SECURE_TLS_INVALID_SELF_SIGNED_CERT          | 0x11A     | O anfitrião remoto enviou um certificado auto-assinado e NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES não está definido.                                              |
| NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND      | 0x11B     | Um certificado remoto foi recebido com um emitente não na loja de confiança local.                                                                              |
| NX_SECURE_TLS_OUT_OF_ORDER_MESSAGE              | 0x11C     | Uma mensagem DTLS foi recebida na ordem errada - um datagrama abandonado é o culpado provável.                                                                    |
| NX_SECURE_TLS_INVALID_REMOTE_HOST                | 0x11D     | Um pacote foi recebido de um hospedeiro remoto que não reconhecemos.                                                                                            |
| NX_SECURE_TLS_INVALID_EPOCH                       | 0x11E     | Uma mensagem DTLS foi recebida e correspondida a uma sessão de DTLS, mas tinha a época errada e deve ser ignorada.                                                   |
| NX_SECURE_TLS_REPEAT_MESSAGE_RECEIVED            | 0x11F     | Uma mensagem DTLS foi recebida com um número de sequência que já vimos, ignore-a.                                                                           |
| NX_SECURE_TLS_NEED_DTLS_SESSION                  | 0x120     | Foi utilizada uma sessão TLS numa API DTLS que não foi inicializada para dTLS.                                                                                       |
| NX_SECURE_TLS_NEED_TLS_SESSION                   | 0x121     | Foi utilizada uma sessão TLS numa API TLS que foi inicializada para DTLS e não TLS.                                                                                |
| NX_SECURE_TLS_SEND_ADDRESS_MISMATCH              | 0x122     | O chamador tentou enviar dados sobre uma sessão de DTLS com um endereço IP ou porta que não correspondia à sessão.                                                  |
| NX_SECURE_TLS_NO_FREE_DTLS_SESSIONS             | 0x123     | Uma nova ligação tentou obter uma sessão de DTLS da cache, mas não havia nenhuma grátis.                                                                        |
| NX_SECURE_DTLS_SESSION_NOT_FOUND                 | 0x124     | O chamador procurou uma sessão de DTLS, mas o endereço IP e a porta não correspondem a nenhuma entrada na cache.                                             |
| NX_SECURE_TLS_NO_MORE_PSK_SPACE                 | 0x125     | O chamador tentou adicionar uma PSK a uma sessão de TLS, mas não havia mais espaço na sessão dada.                                                          |
| NX_SECURE_TLS_NO_MATCHING_PSK                    | 0x126     | Um anfitrião remoto forneceu uma dica de identidade PSK que não correspondia a nenhuma na nossa loja local.                                                                         |
| NX_SECURE_TLS_CLOSE_NOTIFY_RECEIVED              | 0x127     | Uma sessão de TLS recebeu um alerta CloseNotify do anfitrião remoto indicando que a sessão está completa.                                                           |
| NX_SECURE_TLS_NO_AVAILABLE_SESSIONS              | 0x128     | Não estão disponíveis sessões TLS num objeto TLS para manusear uma ligação.                                                                                         |
| NX_SECURE_TLS_NO_CERT_SPACE_ALLOCATED           | 0x129     | Não foi atribuído nenhum espaço de certificado para os certificados remotos de entrada.                                                                                          |
| NX_SECURE_TLS_PADDING_CHECK_FAILED               | 0x12A     | O afildamento de encriptação numa mensagem recebida não estava correto.                                                                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_TYPE        | 0x12B     | No processamento de um CertificadoVerifyRequest, nenhum tipo de certificado suportado foi fornecido pelo servidor remoto.                                                    |
| NX_SECURE_TLS_UNSUPPORTED_CERT_SIGN_ALG         | 0x12C     | No processamento de um CertificadoVerifyRequest, nenhum algoritmo de assinatura suportado foi fornecido pelo servidor remoto.                                                 |
| NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE            | 0x12D     | Não há espaço tampão de certificado suficiente para um certificado.                                                                                              |
| NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED           | 0x12E     | A versão protocolar num registo TLS de entrada não corresponde à versão da sessão estabelecida.                                                          |
| NX_SECURE_TLS_NO_RENEGOTIATION_ERROR             | 0x12F     | Foi recebida uma mensagem da HelloRequest, mas não estamos a renegociar.                                                                                           |
| NX_SECURE_TLS_UNSUPPORTED_FEATURE                 | 0x130     | Uma funcionalidade que foi desativada foi encontrada durante uma sessão de TLS ou aperto de mão.                                                                                |
| NX_SECURE_TLS_CERTIFICATE_VERIFY_FAILURE         | 0x131     | Uma mensagem CertificadoVer uma mensagem de um Cliente remoto não verificou o certificado cliente.                                                                     |
| NX_SECURE_TLS_EMPTY_REMOTE_CERTIFICATE_RECEIVED | 0x132     | O anfitrião remoto enviou uma mensagem de certificado vazia.                                                                                                            |
| NX_SECURE_TLS_RENEGOTIATION_EXTENSION_ERROR      | 0x133     | Ocorreu um erro no processamento de uma extensão de indicação de renegotação segura ou de pagamento.                                                                     |
| NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE     | 0x134     | Uma sessão de renegociação estava a tentar com uma sessão de TLS que não estava ativa.                                                                                |
| NX_SECURE_TLS_PACKET_BUFFER_TOO_SMALL           | 0x135     | TLS recebeu um registo que era muito grande para o amortecedor de pacotes designado. O registo não pôde ser processado.                                                   |
| NX_SECURE_TLS_EXTENSION_NOT_FOUND                | 0x136     | Uma extensão especificada não foi recebida do anfitrião remoto durante o aperto de mão TLS.                                                                         |
| NX_SECURE_TLS_SNI_EXTENSION_INVALID              | 0x137     | TLS recebeu uma extensão inválida de indicação de nome do servidor.                                                                                                     |
| NX_SECURE_TLS_CERT_ID_INVALID                    | 0x138     | A aplicação tentou adicionar um certificado de servidor com um valor de ID de certificado inválido (provavelmente 0).                                                                |
| NX_SECURE_TLS_CERT_ID_DUPLICATE                  | 0x139     | A aplicação tentou adicionar um certificado de servidor com um certificado de identificação já presente na loja local.                                                       |
| NX_SECURE_TLS_RENEGOTIATION_FAILURE               | 0x13A     | O anfitrião remoto não forneceu a extensão de indicação de renegociação segura ou a pseudo-cifrasuite SCSV para que não seja realizada uma renegociação segura.     |
| NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE             | 0x13B     | Na tentativa de realizar uma operação criptográfica, uma das entradas na tabela cifrasumita (ou um dos seus ponteiros de função) foi incorretamente definida como NU. |

**Quadro 1 – Códigos de devolução de erros NetX Secure TLS**

## <a name="netx-secure-x509-return-codes"></a>NetX Secure X.509 Códigos de devolução

O quadro 2 abaixo lista os possíveis códigos de erro que podem ser devolvidos pelos serviços NetX Secure X.509. Note que os serviços também podem devolver outros códigos de erro. Os valores de retorno X.509 começam em 0x181, os valores TLS começam em 0x101 e os valores TCP/IP estão abaixo 0x100. Consulte a documentação NetX TCP/IP para obter informações sobre os valores de devolução TCP/IP e acima para valores de devolução de TLS.

| **Nome de erro**                                   | **Valor** | **Descrição**                                                                                                        |
| ------------------------------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| NX_SECURE_X509_SUCCESS                        | 0x00      | Estado de retorno bem sucedido. (O mesmo que NX_SUCCESS)                                                                        |
| NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED    | 0x181     | Deparámo-nos com uma etiqueta ASN.1 multi-byte - não suportada atualmente.                                                       |
| NX_SECURE_X509_ASN1_LENGTH_TOO_LONG        | 0x182     | Encontrei um valor de comprimento mais longo do que podemos suportar.                                                                  |
| NX_SECURE_X509_FOUND_NON_ZERO_PADDING      | 0x183     | Esperava-se um valor de enchimento de 0 - conseguiu algo diferente.                                                               |
| NX_SECURE_X509_MISSING_PUBLIC_KEY           | 0x184     | X509 esperava uma chave pública, mas não encontrou uma.                                                                        |
| NX_SECURE_X509_INVALID_PUBLIC_KEY           | 0x185     | Encontrei uma chave pública, mas é inválida ou tem um formato incorreto.                                                      |
| NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE | 0x186     | O bloco ASN.1 de nível superior não é uma sequência - certificado X509 inválido.                                                |
| NX_SECURE_X509_MISSING_SIGNATURE_ALGORITHM  | 0x187     | À espera de um identificador de algoritmo de assinatura, não o encontrou.                                                           |
| NX_SECURE_X509_INVALID_CERTIFICATE_DATA     | 0x188     | Os dados de identidade do certificado estão num formato inválido.                                                                     |
| NX_SECURE_X509_UNEXPECTED_ASN1_TAG          | 0x189     | Esperávamos uma etiqueta ASN.1 específica para o formato X509, mas temos outra coisa.                                      |
| NX_SECURE_PKCS1_INVALID_PRIVATE_KEY         | 0x18A     | Um ficheiro de chave privada PKCS#1 foi passado, mas a formatação estava incorreta.                                            |
| NX_SECURE_X509_CHAIN_TOO_SHORT              | 0x18B     | Uma cadeia de certificados X509 era demasiado curta para manter toda a cadeia durante a construção em cadeia.                                |
| NX_SECURE_X509_CHAIN_VERIFY_FAILURE         | 0x18C     | Uma cadeia de certificados X509 não pôde ser verificada (erro de captura).                                                 |
| NX_SECURE_X509_PKCS7_PARSING_FAILED         | 0x18D     | A análise de uma assinatura codificada X.509 PKCS#7 falhou.                                                                     |
| NX_SECURE_X509_CERTIFICATE_NOT_FOUND        | 0x18E     | Ao procurar um certificado, não foi encontrada nenhuma entrada correspondente.                                                              |
| NX_SECURE_X509_INVALID_VERSION               | 0x18F     | Um certificado incluía um campo que não é compatível com a versão dada.                                           |
| NX_SECURE_X509_INVALID_TAG_CLASS            | 0x190     | Um certificado incluía uma etiqueta ASN.1 com um valor de classe de etiqueta inválida.                                                   |
| NX_SECURE_X509_INVALID_EXTENSIONS            | 0x191     | Um certificado incluía uma extensão TLV, mas que não continha uma sequência.                                          |
| NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE   | 0x192     | Um certificado incluía uma sequência de extensão que era inválida X.509.                                                   |
| NX_SECURE_X509_CERTIFICATE_EXPIRED           | 0x193     | Um certificado tinha um campo "não depois" que era menos do que o tempo atual.                                             |
| NX_SECURE_X509_CERTIFICATE_NOT_YET_VALID   | 0x194     | Um certificado tinha um campo "não antes" que era maior do que o tempo atual.                                         |
| NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH     | 0x195     | Um certificado Nome Comum ou Nome Alt Sujeito não corresponde a um dado DNS TLD.                                           |
| NX_SECURE_X509_INVALID_DATE_FORMAT          | 0x196     | Um certificado continha um campo de data que não está num formato reconhecível.                                               |
| NX_SECURE_X509_CRL_ISSUER_MISMATCH          | 0x197     | A mesma Autoridade de Certificados e um certificado fornecido não foram emitidos pela mesma Autoridade de Certificados.                                      |
| NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED  | 0x198     | Um cheque de assinatura CRL falhou contra o seu emitente.                                                                       |
| NX_SECURE_X509_CRL_CERTIFICATE_REVOKED      | 0x199     | Um certificado foi encontrado num CRL válido e, por conseguinte, foi revogado.                                                 |
| NX_SECURE_X509_WRONG_SIGNATURE_METHOD       | 0x19A     | Ao tentar validar uma assinatura, o método de assinatura não corresponde ao método esperado.                          |
| NX_SECURE_X509_EXTENSION_NOT_FOUND          | 0x19B     | Ao procurar uma extensão, não foi encontrada nenhuma extensão com um ID correspondente.                                                |
| NX_SECURE_X509_ALT_NAME_NOT_FOUND          | 0x19C     | Um nome foi procurado numa extensão de Nome de Nome, mas não foi encontrado.                                               |
| NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE    | 0x19D     | O tipo de chave privada dado era desconhecido ou inválido.                                                                         |
| NX_SECURE_X509_NAME_STRING_TOO_LONG        | 0x19E     | Passou uma cadeia de nomes que era demasiado longa para um tampão interno (nome DNS, etc...).                                        |
| NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND    | 0x19F     | Ao pesquisar uma extensão de utilização da chave estendida, o OID de utilização da chave especificado não foi encontrado.                               |
| NX_SECURE_X509_KEY_USAGE_ERROR              | 0x1A0     | Para ser devolvido pelo callback da aplicação se houver uma falha na utilização da chave durante uma verificação de verificação do certificado. |

**Quadro 2 – Códigos de devolução de erros NetX Secure X.509**
