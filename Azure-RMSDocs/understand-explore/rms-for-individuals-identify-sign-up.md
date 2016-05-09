---
# required metadata

title: Como saber se os usuários se inscreveram para o RMS para pessoas físicas | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Como saber se os usuários se inscreveram para o RMS para pessoas físicas
Como administrador, como você sabe se os usuários se inscreveram para o RMS para pessoas físicas? Você pode usar qualquer um dos seguintes métodos ou uma combinação deles:

-   Pergunte aos usuários como eles protegem arquivos altamente confidenciais, especialmente quando colaboram com pessoas de fora da organização.

-   Se você tiver uma assinatura do Azure para sua organização, use o cmdlet [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) para ver se **RIGHTSMANAGEMENT_ADHOC** é retornado como uma das assinaturas. Se for, essa é a assinatura do RMS para pessoas físicas que foi concedida para a empresa, com um pool de unidades ativas disponível para os usuários usarem o processo de inscrição de autoatendimento.

-   Use uma solução de gerenciamento do sistema, como o System Center Configuration Manager, para o software de inventário instalado e o software em uso. O aplicativo de compartilhamento Rights Management é executado usando o programa **ipviewer.exe** e você pode [Baixar e instalar o aplicativo](http://go.microsoft.com/fwlink/?LinkId=303970) gratuitamente para identificar outras características desse aplicativo que é usado para o inventário de software.

-   Esteja atento às extensões de nome de arquivo que criadas pelo aplicativo de compartilhamento Rights Management. As extensões de nome de arquivo .pfile e .ppdf são os exemplos mais óbvios, mas há outros arquivos que alteram sua extensão de nome de arquivo quando são protegidos nativamente pelo Rights Management. Para obter mais informações, consulte a seção [Tipos de arquivo e extensões de nome de arquivo com suporte](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) no [Guia de administrador do aplicativo de compartilhamento Rights Management](http://technet.microsoft.com/library/dn339003.aspx).



<!--HONumber=Apr16_HO3-->


