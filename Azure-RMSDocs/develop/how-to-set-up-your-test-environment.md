---
# required metadata

title: Testando seu aplicativo | Azure RMS
description: Instruções sobre como configurar seu aplicativo para testes.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Testando seu aplicativo

Este tópico contém instruções sobre a configuração dos testes para seu aplicativo.

## Instruções

### Etapa 1: Configurar para os testes

Você pode testar com o Azure RMS ou um Servidor RMS em execução no Windows Server e sugerimos que você inicie os testes no Azure RMS e, se for necessário para sua implantação, teste com o Servidor RMS.

1. Para testar com o Azure RMS, consulte [How-to: use ADAL authentication](how-to-use-adal-authentication.md) (Como usar a autenticação de ADAL).
2. Para testar com o servidor RMS, consulte [Como instalar e configurar um servidor RMS](how-to-install-and-configure-an-rms-server.md).
3. O exemplo a seguir descreve como instalar o tempo de execução do desenvolvedor.

   Você deve ter o Rights Management Service Client 2.1 instalado no computador no qual testará seu aplicativo.
   - Se você for testar seu aplicativo em um computador diferente do computador de desenvolvimento, instale o RMS Client 2.1 no computador na [página de download do AD RMS Client 2.1](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Se você for testar seu aplicativo no computador de desenvolvimento, você já deve ter instalado o Rights Management Services SDK 2.1. O RMS Client 2.1 já terá sido instalado silenciosamente.

    Para saber mais sobre como instalar o SDK 2.1 do RMS, confira [Instalação do SDK](create-your-first-rights-aware-application.md).

## Comentários

As diretrizes neste tópico não são abrangentes. Para saber mais sobre como configurar o RMS Client 2.1, confira [RMS Client 2.1 Deployment Notes](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx) (Notas de implantação do RMS Client 2.1).

### Tópicos relacionados

* [Como instalar e configurar um servidor RMS](how-to-install-and-configure-an-rms-server.md)
* [Como usar a autenticação de ADAL](how-to-use-adal-authentication,md)
* [Instalar o SDK](create-your-first-rights-aware-application.md)
* [Notas de Implantação do RMS Client 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 


<!--HONumber=Jun16_HO2-->


