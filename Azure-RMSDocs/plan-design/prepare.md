---
# required metadata

title: Preparar para o Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Preparar para o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Depois de se inscrever numa subscrição na nuvem e criar uma conta do [!INCLUDE[o365_1](../includes/o365_1_md.md)] ou do Azure Active Directory para a sua organização, está pronto para ativar o serviço [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

No entanto, antes de o fazer, certifique-se de que o seguinte está correto:

-   Grupos e contas de utilizadores na nuvem que pode criar manualmente ou que são automaticamente criados e sincronizados nos Serviços de Domínio do Active Directory (AD DS).

    Quando sincroniza os seus grupos e contas no local, não é necessário sincronizar todos os atributos. Para obter uma lista dos atributos que têm de ser sincronizados com o Azure RMS, consulte a secção [Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) na documentação do Azure Active Directory. Para facilitar a implementação, recomendamos que utilize o [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) para ligar os seus diretórios no local ao Azure Active Directory, mas pode utilizar qualquer método de sincronização de diretórios que alcance o mesmo resultado.

-   Os grupos com capacidade de correio na nuvem que irá utilizar com o Rights Management. Estes podem ser grupos incorporados ou grupos criados manualmente que contêm utilizadores que irão utilizar o Rights Management.

    Se tiver o Exchange Online, pode criar e utilizar grupos com capacidade de correio utilizando o centro de administração do Exchange. Se tiver o AD DS no local e estiver a sincronizar com o Azure AD, pode criar e utilizar grupos com capacidade de correio que são grupos de segurança ou grupos de distribuição.

## Ativar o Rights Management
Por predefinição, o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está desativado quando se inscreve no [!INCLUDE[o365_2](../includes/o365_2_md.md)] ou na conta do Azure AD. Para ativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização, tem de ativar o serviço. Para mais informações, consulte [Ativar o Azure Rights Management](../deploy-use/activate-service.md).





<!--HONumber=Apr16_HO4-->


