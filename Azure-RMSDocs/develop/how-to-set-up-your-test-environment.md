---
title: "Testar a sua aplicação | Azure RMS"
description: "Instruções sobre como configurar a sua aplicação para fins de teste."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b01f009ec3dffbb3fe671da8a19929e53c67fb79
ms.openlocfilehash: cf86b07ba057d8999a156ae397ff7200b12a3f5e


---

# Testar a sua aplicação

Este tópico contém instruções sobre como configurar o teste de aplicações.

## Instruções

### Passo 1: Configuração para teste

Pode testar com o Azure RMS ou um servidor RMS em execução no Windows Server. Sugerimos que inicie os testes no Azure RMS e, em seguida, se for necessário para a implementação, efetue o teste com o RMS Server.

1. Para fins de teste com o Azure RMS, consulte o artigo [Procedimentos: utilizar a autenticação ADAL](how-to-use-adal-authentication.md).
2. Para fins de teste com o RMS Server, consulte o artigo [Procedimentos: instalar e configurar um servidor RMS](how-to-install-and-configure-an-rms-server.md).
3. O seguinte procedimento descreve como instalar o runtime de programador.

   Tem de ter o Rights Management Service Client 2.1 instalado no computador no qual irá testar a aplicação.
   - Se testar a aplicação num computador diferente do seu computador de desenvolvimento, pode instalar o RMS Client 2.1 nesse computador a partir da [página de transferência do AD RMS Client](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
   - Se testar a aplicação no seu computador de desenvolvimento, deve ter previamente instalado o SDK Rights Management Services 2.1. O RMS Client 2.1 terá já sido instalado silenciosamente.

    Para obter informações sobre como instalar o SDK RMS 2.1, consulte [Instalar o SDK](install-the-rms-sdk.md).

## Observações

As orientações neste tópico não são abrangentes. Para obter informações detalhadas sobre como configurar o RMS Client 2.1, consulte as [Notas de Implementação do RMS Client 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx).

### Tópicos relacionados

* [Procedimentos: instalar e configurar um servidor RMS](how-to-install-and-configure-an-rms-server.md)
* [Procedimentos: utilizar a autenticação ADAL](how-to-use-adal-authentication.md)
* [Instalar o SDK](install-the-rms-sdk.md)
* [Notas de Implementação do RMS Client 2.1](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 



<!--HONumber=Jun16_HO4-->


