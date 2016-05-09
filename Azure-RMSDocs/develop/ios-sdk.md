---
# required metadata

title: Configuração do iOS e OS X | Azure RMS
description: Os aplicativos iOS e OS X podem usar o RMS SDK 4.2 para habilitar a proteção integrada de informações em seus aplicativos usando o AAD RM.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 23f64fc8-d0f3-49ee-8d8a-b34ef26878a7

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Configuração do iOS e OS X

Os aplicativos iOS e OS X podem usar o Microsoft Rights Management SDK 4.2 para habilitar a proteção integrada de informações em seus aplicativos usando o AAD RM (Azure Active Directory Rights Management).

Este tópico orientará você durante a configuração de seu ambiente para criação de seus próprios aplicativos novos.

**Observação**: esse SDK não dá suporte para o iPod Touch.


-   [Pré-requisitos](#prerequisites)
-   [Opcional](#optional)
-   [Configurando o ambiente de desenvolvimento](#configuring_your_development_environment)
-   [Consulte também](#see_also)

## Pré-requisitos

Recomendamos o seguinte software em seu sistema de desenvolvimento:

-   O OS X é necessário para todo o desenvolvimento do iOS.
-   Xcode versão 6.0 e posterior

    O Xcode está disponível na [Mac App Store](https://developer.apple.com/technologies/mac/).

-   O pacote do MS RMS SDK 4.2 para iOS e OS X. Para obter mais informações, consulte [Introdução](get-started.md).

    Esse SDK pode ser usado para desenvolver para o iOS 7.0 e OS X 10.8 e posterior.

-   Biblioteca de autenticação: recomendamos o uso da [ADAL (Azure AD Authentication Library)](https://msdn.microsoft.com/en-us/library/jj573266.aspx). No entanto, outras bibliotecas de autenticação que dão suporte ao OAuth 2.0 também podem ser usadas.

    Para saber mais, consulte [ADAL para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) ou [ADAL para OS X](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)

Leia o tópico [Novidades](release-notes.md) para saber mais sobre as atualizações de API, notas de versão e perguntas frequentes.

## Opcional

Nossa biblioteca de interface do usuário fornece uma interface de usuário reutilizável para operações de consumo e proteção para desenvolvedores que não querem criar sua própria interface do usuário personalizada - [Biblioteca de interface do usuário e exemplo de aplicativo para iOS](https://github.com/AzureAD/rms-sdk-ui-for-ios).

## Configurando o ambiente de desenvolvimento

-   Para criar um novo projeto, no menu **Arquivo**, clique em **Novo** e, em seguida, **Projeto**.
-   Selecione **Aplicativo de Exibição Única**.

    ![](../media/iOS-Project.png)

-   Insira um nome e um identificador para o novo projeto.

    ![](../media/iOS-project-options.png)

-   Clique em **Avançar** e selecione o local do seu projeto.
-   Para adicionar a estrutura **MSRightsManagement** para iOS Frameworks, arraste a pasta .framework da pasta de instalação do SDK para a seção **Estruturas** de seu **Navegador de Projeto**.

    ![](../media/ios-add-dependencies-01a.png)

-   Selecione o botão de opção **Criar grupos para qualquer pasta adicionada** e desmarque a caixa de seleção **Copiar itens na pasta do grupo de destino (se necessário)**.

    Essa ação mantém a referência para a pasta de instalação do SDK em vez de criar uma cópia.

    ![](../media/iOS-create-groups.png)

-   Para adicionar o MS RMS SDK 4.2 ao grupo de recursos, arraste o arquivo MSRightsManagementResources.bundle da pasta MSRightsManagement.framework/Resources para a seção **Estruturas** do seu navegador de projeto.

    ![](../media/iOS-add-resource-bundle-02a.png)

-   Como você fez quando copiou a estrutura, selecione o botão de opção **Criar grupos para qualquer pasta adicionada** e desmarque a caixa de seleção **Copiar itens na pasta do grupo de destino (se necessário)**.
-   O SDK depende de outras estruturas, incluindo: **CoreData**, **MessageUI**, **SystemConfiguration**, **Libresolv** e **Segurança**. Para adicionar essas estruturas, navegue até a seção **Estruturas e bibliotecas vinculadas** do painel **Resumo** do destino e expanda essa seção para adicioná-las.

    As estruturas **UIKit** e **Foundation** são necessárias e, geralmente, estão presentes por padrão.

    ![](../media/iOS-add-libraries.png)

-   Adicione o sinalizador **- ObjC** como **Outros Sinalizadores do Vinculador** ao seu destino **Configurações da Compilação**.

    ![](../media/iOS-linker-flags.png)

-   Agora seu **Navegador de Projeto** deve estar parecido com essa árvore.

    ![](../media/iOS-verify-setup-01a.png)

-   Agora você está pronto para criar seus próprios aplicativos novos do iOS/OS.

### Consulte também

* [Introdução](get-started.md)

* [Novidades](release-notes.md)

* [Termos e conceitos de desenvolvedor](core-concepts.md)

* [Referência de API do iOS/OS X](/rights-management/sdk/4.2/api/ios/ios)

 

 





<!--HONumber=Apr16_HO3-->


