---
title: Como usar o rastreamento de documentos | Azure RMS
description: "O recurso de rastreamento de documentos requer algumas noções básicas simples sobre como gerenciar os metadados associados e o registro com o serviço."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ca4982cc86d9c006486540055de7c165adca21da
ms.openlocfilehash: 9872317c2d5f5f56f28ed2683d7ebc9743041a37


---

# Como: usar o rastreamento de documentos

O uso do recurso de rastreamento de documentos requer algumas noções básicas simples sobre como gerenciar os metadados associados e o registro com o serviço.

## Gerenciamento de metadados de rastreamento de documentos

Cada um dos sistemas operacionais com suporte para rastreamento de documentos tem implementações semelhantes. Isso inclui um conjunto de propriedades que representam os metadados, um novo parâmetro adicionado para os métodos de criação de política de usuário e um método para registrar a política para que ela seja rastreada com o serviço de rastreamento de documentos.

Operacionalmente, somente as propriedades **nome do conteúdo** e o **tipo de notificação** são necessárias para o rastreamento de documentos.

A sequência de etapas que você usará para configurar o rastreamento de documentos para uma determinada parte do conteúdo é:

-   Criar um objeto de **metadados de licença**.

    Consulte [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) ou [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) para obter mais informações.

-   Defina o **nome do conteúdo** e o **tipo de notificação**. Essas são as únicas propriedades necessárias.

    Para obter mais informações, consulte os métodos de acesso de propriedade para a classe de metadados de licença adequada de plataforma, [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) ou [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc).

-   Por tipo de política; modelo ou ad-hoc:

    -   Para o rastreamento de documentos com base em um modelo, crie um objeto de **política de usuário** passando os metadados de licença como um parâmetro.

        Para obter mais informações, consulte [**UserPolicy.create**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) e [**MSUserPolicy.userPolicyWithTemplateDescriptor**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc).

    -   Para o rastreamento de documentos com base em ad-hoc, defina a propriedade **metadados de licença** do objeto **descritor de política**.

        Para obter mais informações, consulte [**PolicyDescriptor.getLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java), [**PolicyDescriptor.setLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) e [**MSPolicyDescriptor.licenseMetadata**](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc).

    **Observação**: o objeto de metadados de licença pode ser acessado diretamente somente durante o processo de configuração de rastreamento de documentos da política de usuário específica. Depois de criar o objeto de política de usuário, os metadados de licença associados não estão acessíveis, ou seja, alterar os valores de metadados de licença não tem nenhum efeito.

     

-   Chame o método de registro de plataforma para o rastreamento de documentos.

    Consulte [**MSUserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) ou [**UserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc).

 

 



<!--HONumber=Jun16_HO4-->


