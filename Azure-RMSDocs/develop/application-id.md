---
# required metadata

title: Como &#58; Obter uma ID do aplicativo do Azure | Azure RMS
description: Criar um aplicativo habilitado para RMS com o Microsoft Rights Management SDK 4.2 exige criar um contrato com a equipe do RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 834c5943-a724-4322-9035-060c1112fe22

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Como: obter uma ID do aplicativo do Azure

Criar um aplicativo habilitado para RMS com o Microsoft Rights Management SDK 4.2 exige criar um contrato com a equipe do RMS.

## Visão geral

Criar e lançar um aplicativo habilitado para RMS com o RMS SDK MS 4.2 exige criar um contrato de uso de serviços com a equipe do RMS. Este contrato, também conhecido como um RMLA (Contrato de Licença do Rights Management), o orienta para cumprir o contrato para proteção de conteúdo que será mantido em nome do usuário e/ou do proprietário do conteúdo pelos comportamentos (aderência às regras de negócio) do seu aplicativo. Como um criador de um aplicativo habilitado para RMS, o contrato com a equipe de RMS será imposto pela existência de uma "ID do aplicativo do Azure" que representa este contrato e permite que seu aplicativo se conecte ao serviço de autenticação do Azure AD.

## Processar

Use as seguintes etapas para criar sua ID do aplicativo e assinar o contrato de uso com a equipe do RMS.

-   Siga as diretrizes no tópico [como criar uma ID do aplicativo no Azure](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx) para criar sua ID do aplicativo.
-   Escreva para a equipe do RMS para iniciar o processo de RMLA, enviando sua "ID do aplicativo" para <askipteam@microsoft.com>.
-   Assine o RMLA e devolva-o à equipe do RMS.
-   Agora que você assinou o RMLA, deve passar a ID do aplicativo ao chamar a biblioteca de autenticação por meio do parâmetro *clientID*.

    Esta é a aparência da chamada de autenticação no nosso tópico de [Exemplos de código do iOS/OS X](ios-os-x-code-examples.md).


    // Retrieve token using ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**Observação** se a equipe do RMS não receber seu RMLA assinado dentro de 60 dias, seu aplicativo será impedido de autenticar-se com o Sistema de Autenticação do Azure.

 

 

 


<!--HONumber=Apr16_HO3-->


