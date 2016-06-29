---
# required metadata

title: Como&#58; obter uma ID da Aplicação Azure | Azure RMS
description: Criar uma aplicação ativada com capacidade para RMS com o SDK Microsoft Rights Management 4.2 exige que crie um contrato com a Equipa do RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0fe9dc-bc91-4018-b28d-2db293a3eaa2
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como: obter uma ID da Aplicação Azure

Criar uma aplicação ativada com capacidade para RMS com o SDK Microsoft Rights Management 4.2 exige que crie um contrato com a Equipa do RMS.

## Descrição Geral

Criar e lançar uma aplicação com capacidade para RMS com o SDK MS RMS 4.2 exige que crie também um contrato de utilização de serviços com a Equipa do RMS. Este contrato, também conhecido como Contrato de Licença Rights Management (RMLA), descreve como honrar o contrato em relação à proteção de conteúdo que irá preservar em nome do utilizador e/ou do proprietário do conteúdo pelos comportamentos (respeito pelas regras de negócio) da sua aplicação. Na qualidade de criador de uma aplicação com capacidade para RMS, o seu contrato com a Equipa do RMS será aplicado pela existência de uma “ID da Aplicação Azure ” que representa o presente contrato e que permite que a sua aplicação estabeleça ligação com o Serviço de Autenticação do Azure AD.

## Processo

Utilize os passos seguintes para criar a ID da sua aplicação e assinar o contrato de utilização com a Equipa do RMS.

-   Siga as orientações no tópico [Como criar uma ID da Aplicação no Azure](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx) para criar a sua ID da aplicação.
-   Escreva à Equipa do RMS para iniciar o processo de RMLA enviando a sua “ID da Aplicação” para <askipteam@microsoft.com>.
-   Assine o RMLA e devolva-o à Equipa do RMS.
-   Agora que tem um RMLA assinado, deverá passar a ID da Aplicação ao chamar a biblioteca de autenticação através do parâmetro *clientID*.

    Este é o aspeto da chamada de autenticação no nosso tópico [Exemplos de códigos do iOS/OS X](ios-os-x-code-examples.md).


    // Obter token ao utilizar a ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**Nota** Se a Equipa do RMS não receber o RMLA assinado num período de 60 dias, a sua aplicação não poderá ser autenticada com o Sistema de Autenticação do Azure.

 

 

 


<!--HONumber=Apr16_HO4-->


