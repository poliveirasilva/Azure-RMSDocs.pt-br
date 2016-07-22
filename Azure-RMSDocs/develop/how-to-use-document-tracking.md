---
title: Como utilizar o controlo de documentos | Azure RMS
description: "A funcionalidade de controlo de documentos requer alguns conhecimentos simples sobre a gestão dos metadados associados e o registo do serviço."
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

# Como: utilizar o controlo de documentos

A utilização da funcionalidade de controlo de documentos requer alguns conhecimentos simples sobre a gestão dos metadados associados e o registo do serviço.

## Gerir metadados de controlo de documentos

Todos os sistemas operativos que suportam o controlo de documentos têm implementações semelhantes. Estes incluem um conjunto de propriedades que representam os metadados, um novo parâmetro adicionado aos métodos de criação de políticas de utilizador e um método para registar a política a controlar com o serviço de controlo de documentos.

Operacionalmente, apenas as propriedades **nome do conteúdo** e **tipo de notificação** são necessárias para o controlo de documentos.

A sequência de passos que irá utilizar para configurar o controlo de documentos para um determinado conteúdo é a seguinte:

-   Crie um objeto **metadados de licença**.

    Consulte [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) ou [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) para obter mais informações.

-   Defina o **nome do conteúdo** e o **tipo de notificação**. Estas são as únicas propriedades necessárias.

    Para obter mais informações, consulte os métodos de acesso às propriedades da classe de metadados de licença adequada da plataforma, seja [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) ou [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc).

-   Por tipo de política, modelo ou ad hoc:

    -   Para o controlo de documentos com base em modelos, crie um objeto **política de utilizador** passando os metadados de licença como um parâmetro.

        Para obter mais informações, consulte [**UserPolicy.create**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) e [**MSUserPolicy.userPolicyWithTemplateDescriptor**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc).

    -   Para o controlo de documentos com base em ad hoc, defina a propriedade **metadados de licença** no objeto **descritor de política**.

        Para obter mais informações, consulte [**PolicyDescriptor.getLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java), [**PolicyDescriptor.setLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) e [**MSPolicyDescriptor.licenseMetadata**](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc).

    **Nota** O objeto de metadados de licença só é acessível diretamente durante o processo de configuração do controlo de documentos da política de utilizador especificada. Quando o objeto de política de utilizador tiver sido criado, os metadados de licença associados não estão acessíveis, ou seja, alterar os valores dos metadados de licença não tem qualquer efeito.

     

-   Chame o método de registo de plataforma para o controlo de documentos.

    Consulte [**MSUserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) ou [**UserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc).

 

 



<!--HONumber=Jun16_HO4-->


