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
experimental: true
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: ac7f8296149b93be803165ebde5144b0f78fa0c8
ms.openlocfilehash: 9f722463eca408527cb8e39798eb6719d1f57804


---

# Como: usar direitos internos

Este tópico descreve os direitos internos que o Microsoft Rights Management SDK 4.2 fornece, e as restrições de uso que um aplicativo deve impor para respeitar essas restrições. O exemplo a seguir mostra os direitos internos; direitos comuns, direitos de documento editável e direitos de email, com uma descrição e seus valores de acordo com o sistema operacional na sequência.

**Observação** - Para o SDK do Linux, veja o arquivo de origem *rights.h* para obter detalhes.

## Direitos comuns ##

**All** - Uma coleção de todos os direitos comuns.
- Android: [CommonRights.All](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL)
- iOS e OS X: [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store e Windows Phone: [CommonRights.All</strong>](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)
- Linux: [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Proprietário** - O direito do Proprietário concede controle total sobre o conteúdo protegido.
- Android: [<strong>CommonRights.Owner](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner)
- iOS e OS X: [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store e Windows Phone: [CommonRights.Owner](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner)
- Linux: [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**View** - O direito de exibir conteúdo protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário abra e exiba o conteúdo protegido. No entanto, é necessário ter direitos adicionais para modificar, extrair, encaminhar ou salvar o conteúdo.

- Android: [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- iOS e OS X: [MSCommonRights view](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows Store e Windows Phone: [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- Linux: [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## Direitos de documento editável ##
**All** - Uma coleção que contém todos os direitos do documento editável.
- Android:[EditableDocumentRights.All](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL)
- iOS e OS X: [MSEditableDocumentRights all](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.All](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all)
- Linux: [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Comment** - O direito de fazer comentários no documento.
- Android: [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)
- iOS e OS X: [MSEditableDocumentRights comment](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)
- Linux: [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Edit** - O direito de editar conteúdo protegido e salvá-lo no mesmo formato protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário altere o conteúdo protegido e salve-o no mesmo arquivo.
- Android: [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit)
- iOS e OS X: [MSEditableDocumentRights edit](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit)
- Linux: [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Export** - o direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato diferente protegido pelo AD RMS. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário salve o conteúdo protegido em outros formatos protegidos pelo AD RMS; por exemplo, se o aplicativo implementar uma funcionalidade *Salvar como*.

- Android: [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export)
- iOS e OS X: [MSEditableDocumentRights exportable](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export)
- Linux: [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Extract** - O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato não protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário copie e cole informações do conteúdo protegido. Se o aplicativo implementa uma funcionalidade <em>Salvar como</em>, também pode permitir que o usuário salve o conteúdo protegido em formatos desprotegidos e em outros formatos protegidos. Esse direito tem o mesmo valor que o direito Extract para email.

- Android: [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract)
- iOS e OS X: [MSEditableDocumentRights extract](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract)
- Linux: [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Print** - O direito de imprimir conteúdo protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que o usuário imprima o conteúdo protegido. Esse direito tem o mesmo valor que o direito Print para email.

- Android: [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print)
- iOS e OS X: [MSEditableDocumentRights print](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows Store e Windows Phone: [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print)
- Linux: [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## Direitos de email ##

**All** - Uma coleção que contém todos os direitos de email.
- Android: [EmailRights.All](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL)
- iOS e OS X: [MSEmailRights all](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.All](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)
- Linux: [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Extract** - O direito de extrair o conteúdo de um formato protegido e colocá-lo em um formato não protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email copie e cole informações da mensagem protegida. Se o aplicativo implementa uma funcionalidade <em>Salvar como</em>, também pode permitir que o destinatário salve o conteúdo protegido em formatos desprotegidos e em outros formatos protegidos. Esse direito tem o mesmo valor que o direito Extract para documentos editáveis.

- Android: [EmailRights.Extract](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract)
- iOS e OS X: [MSEmailRights extract](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Extract</strong>](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract)
- Linux: [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Forward** - O direito de encaminhar uma mensagem protegida. Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email encaminhe a mensagem protegida.
- Android: [<strong>EmailRights.Forward</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward)
- iOS e OS X: [MSEmailRights forward](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Forward](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward)
- Linux: [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Print** - O direito de imprimir conteúdo protegido. Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email imprima uma mensagem protegida. Esse direito tem o mesmo valor que o direito Print para documentos editáveis.

- Android: [EmailRights.Print](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print)
- iOS e OS X: [MSEmailRights print](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Print](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print)
- Linux: [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Reply** - Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email responda a uma mensagem protegida e inclua uma cópia da mensagem original.

- Android: [EmailRights.Reply](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply)
- iOS e OS X: [MSEmailRights reply](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.Reply](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply)
- Linux: [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll** - Normalmente, quando esse direito é concedido, o aplicativo permite que um destinatário de email responda a todos os destinatários de uma mensagem protegida e inclua uma cópia da mensagem original.

- Android: [EmailRights.ReplyAll</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll)
- iOS e OS X: [MSEmailRights replyAll](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows Store e Windows Phone: [EmailRights.ReplyAll](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall)
- Linux: [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 



<!--HONumber=Aug16_HO2-->


