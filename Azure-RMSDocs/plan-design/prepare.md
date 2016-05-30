---
# required metadata

title: Preparando o Azure Rights Management | Azure RMS
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

# Preparando o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Depois que você se inscreveu para uma assinatura na nuvem e estabeleceu uma conta para sua organização do [!INCLUDE[o365_1](../includes/o365_1_md.md)] ou do Azure Active Directory, você está pronto para habilitar o serviço do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

No entanto, antes de fazê-lo, certifique-se de que o seguinte esteja em vigor:

-   Contas de usuário e grupos na nuvem que você cria manualmente ou que são criados e sincronizados automaticamente a partir dos Serviços de Domínio do Active Directory (AD DS).

    Quando você sincroniza seu grupos e contas locais, nem todos os atributos precisam ser sincronizados. Para obter uma lista dos atributos que devem ser sincronizados para o Azure RMS, consulte esta [seção do Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) na documentação do Azure Active Directory. Para facilitar a implantação, recomendamos que você use o [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) para conectar seu diretórios locais ao Azure Active Directory, mas você pode usar qualquer método de sincronização de diretório que atinja o mesmo resultado.

-   Grupos habilitados para email na nuvem que você irá usar com o Rights Management. Eles podem ser grupos internos ou criados manualmente contendo usuários que usarão o Rights Management.

    Se você tiver o Exchange Online, crie e use grupos habilitados para email usando o Centro de administração do Exchange. Se você tiver o Active Directory local e estiver sincronizando ao AD do Azure AD, use grupos habilitados para email que sejam grupos de segurança ou grupos de distribuição.

## Habilitar o Rights Management
Por padrão, o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está desabilitado quando você se inscreve na conta do [!INCLUDE[o365_2](../includes/o365_2_md.md)] ou do Azure AD. Para habilitar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização, você deve ativar o serviço. Para obter mais informações, consulte [Ativando o Azure Rights Management](../deploy-use/activate-service.md).





<!--HONumber=Apr16_HO4-->


