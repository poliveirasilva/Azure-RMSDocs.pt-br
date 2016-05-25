---
# required metadata

title: Condições de erro comuns e soluções | Azure RMS
description: Esse tópico inclui as mensagens de erro mais comuns que você pode encontrar ao usar as ferramentas de desenvolvedor do RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: A5B95EB8-3528-4CFF-86FC-166613A5F4A3
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Condições de erro comuns e soluções
Esse tópico inclui as mensagens de erro mais comuns que você pode encontrar ao usar as ferramentas de desenvolvedor do Rights Management Services SDK 2.1. Ele também fornece uma ação recomendada para corrigir o erro, quando aplicável.

**Importante** - para processamento de condição de erro, sempre use uma chamada para [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) logo depois que uma chamada à API do SDK falhar, para que você obtenha informações completas sobre a natureza do erro.

 

## Erro e ação ##
A lista a seguir contém uma lista de constantes de erro, sua descrição associada e uma ação sugerida para tratar da condição de erro.

**ERROR** - *IPCERROR_DEBUGGER_DETECTED* - um depurador foi detectado pelo RMS SDK 2.1

**AÇÃO** - a versão do desenvolvedor do RMS SDK 2.1 não verifica a presença de um depurador. Se possível, depure seu aplicativo usando esta versão do RMS SDK 2.1.
Se você deve depurar a versão de produção do RMS SDK 2.1, use as diretrizes a seguir.

Algumas funções do RMS SDK 2.1 são projetadas para falhar em um depurador:
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

Para depurar o código que segue essas chamadas de função, você deve interromper o processo e anexar um depurador após a conclusão das chamadas de função. Uma maneira de fazer isso é usar uma instrução assert para invadir o depurador. A macro ASSERTE está incluída no cabeçalho *Crtdbg.h*.
Para obter mais informações sobre \_ASSERTE, consulte [\_ASSERT, \_ASSERTE Macros](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)

**ERROR** - *IPCERROR_BROKEN_CERT_CHAIN* - cadeia de certificados não coincide.

**AÇÃO** - verifique se a chave de hierarquia contém o valor correto com base na chave usada para assinar o manifesto do aplicativo do AD RMS.
Essas são as chaves de assinatura e seus valores associados (hierarquia **DWORD**):
- ISV—1
- Production—0 ou não está presente

**ERROR** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED* - você está usando um aplicativo assinado com a chave de assinatura de ISV, mas ele está tentando se comunicar com um servidor de produção AD RMS, ou vice-versa.

- Se você estiver usando a versão de desenvolvedor do servidor AD RMS, certifique-se de que você está usando a chave de assinatura do ISV para assinar seu aplicativo.
- Se você estiver usando a versão de produção do servidor AD RMS, certifique-se de que você está usando a chave de assinatura de produção para assinar seu aplicativo.

**ERROR** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST* - o manifesto do aplicativo não é válido. Isso pode ser causado quando o binário (aplicativo) foi recriado e o manifesto não foi regenerado.

**AÇÃO** - certifique-se de regenerar seu manifesto do aplicativo sempre que recriar seu aplicativo.

## Tópicos relacionados ##
* [Notas do desenvolvedor](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [\_ASSERT, \_ASSERTE macros](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Apr16_HO4-->


