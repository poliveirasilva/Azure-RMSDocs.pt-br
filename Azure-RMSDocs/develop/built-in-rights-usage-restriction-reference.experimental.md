---
title: Como&#58; usar direitos internos | Azure RMS
description: "Descreve os direitos internos que o RMS SDK 4.2 fornece e as restrições de uso que um aplicativo deve impor para respeitar essas restrições."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: ac7f8296149b93be803165ebde5144b0f78fa0c8
ms.openlocfilehash: 25bfc768aba30be7f81ce659ca90e71266c599ba


---

# Como: usar direitos internos

Este tópico descreve os direitos internos que o Microsoft Rights Management SDK 4.2 fornece, e as restrições de uso que um aplicativo deve impor para respeitar essas restrições. A tabela a seguir mostra os direitos internos; direitos comuns, direitos de documento editável e direitos de email, seguido de uma descrição e seus valores por sistema operacional.

**Observação** - Para o SDK do Linux, veja o arquivo de origem *rights.h* para obter detalhes.

## Direitos comuns ##

| Right | Descrição | Android | iOS e OSX | Windows Store e Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **Todos** | Uma coleção de todos os direitos comuns. | [CommonRights.All](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL) | [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)| [CommonRights.All</strong>](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)| [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **Proprietário**| Conceder controle total sobre o conteúdo protegido |  [CommonRights.Owner](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner) |[MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_) |[CommonRights.Owner](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner) |  [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **Exibição** | O direito de exibir conteúdo protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário abra e exiba o conteúdo protegido. No entanto, é necessário ter direitos adicionais para modificar, extrair, encaminhar ou salvar o conteúdo. |  [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [MSCommonRights view](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)|[CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html) |


## Direitos de documento editável ##

| Right | Descrição | Android | iOS e OSX | Windows Store e Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **Todos** | Uma coleção que contém todos os direitos do documento editável.| [EditableDocumentRights.All](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL) | [MSEditableDocumentRights all](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.All](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all) |[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Comentário** | O direito de fazer comentários no documento. | [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)|[MSEditableDocumentRights comment](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)| [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Editar** | O direito de editar conteúdo protegido e salvá-lo no mesmo formato protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário altere o conteúdo protegido e salve-o no mesmo arquivo. | [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit) | [MSEditableDocumentRights edit](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit) | [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html) |
| **Exportar** | O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato protegido do AD RMS diferente. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário salve o conteúdo protegido em outros formatos protegidos pelo AD RMS; por exemplo, se o aplicativo implementar uma funcionalidade *Salvar como*. | [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export) | [MSEditableDocumentRights exportable](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Export](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export) | [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Extrair** | O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato não protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário copie e cole informações do conteúdo protegido. Se o aplicativo implementa uma funcionalidade <em>Salvar como</em>, também pode permitir que o usuário salve o conteúdo protegido em formatos desprotegidos e em outros formatos protegidos. Esse direito tem o mesmo valor que o direito Extract para email. |  [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract) |[MSEditableDocumentRights extract](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract) |  [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Imprimir** | O direito de imprimir conteúdo protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário imprima o conteúdo protegido. Esse direito tem o mesmo valor que o direito Print para email. | [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print) |  [MSEditableDocumentRights print](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)| [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print) | [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
 

## Direitos de email ##

| Right | Descrição | Android | iOS e OSX | Windows Store e Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **Todos** |Uma coleção que contém todos os direitos de email. |  [EmailRights.All](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL) | [MSEmailRights all](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.All](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)|[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Extrair** | O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato não protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email copie e cole informações da mensagem protegida. Se o aplicativo implementa uma funcionalidade <em>Salvar como</em>, também pode permitir que o destinatário salve o conteúdo protegido em formatos desprotegidos e em outros formatos protegidos. Esse direito tem o mesmo valor que o direito Extract para documentos editáveis. | [EmailRights.Extract](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract) | [MSEmailRights extract](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Extract</strong>](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract) | [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**Encaminhar**| O direito de encaminhar uma mensagem protegida. Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email encaminhe a mensagem protegida.| [<strong>EmailRights.Forward</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward) | [MSEmailRights forward](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Forward](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward) | [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**Imprimir** | O direito de imprimir conteúdo protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email imprima uma mensagem protegida. Esse direito tem o mesmo valor que o direito Print para documentos editáveis. | [EmailRights.Print](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print) |[MSEmailRights print](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Print](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print) | [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Responder** | Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email responda a uma mensagem protegida e inclua uma cópia da mensagem original. | [EmailRights.Reply](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply) | [MSEmailRights reply](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Reply](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply) | [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Respondera todos** | Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email responda a todos os destinatários de uma mensagem protegida e inclua uma cópia da mensagem original. | [EmailRights.ReplyAll</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll) | [MSEmailRights replyAll](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.ReplyAll](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall) | [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|



<!--HONumber=Aug16_HO2-->


