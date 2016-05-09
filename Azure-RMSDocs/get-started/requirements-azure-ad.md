---
# required metadata

title: Requisitos do Azure RMS& #58; Diretório do Azure AD | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Requisitos do Azure RMS: diretório do Azure AD

É necessário ter um diretório do Azure AD para usar o Azure RMS (Azure Rights Management). Você pode usar a conta da sua organização deste diretório para acessar o Portal clássico do Azure, onde, por exemplo, é possível configurar e gerenciar modelos do Rights Management.

Se você ainda não tiver uma assinatura do Azure para sua organização, poderá obtê-la se inscrevendo em uma avaliação gratuita: vá para a página [Introdução ao Azure](https://account.windowsazure.com/organization) e siga as instruções.

Para obter mais informações, consulte os seguintes recursos na documentação do Azure Active Directory:

-   [O que é um diretório do Azure AD?](/active-directory/active-directory-whatis)

-   [Como as assinaturas do Azure estão associadas ao Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Se deseja integrar seu diretório do Azure AD com as florestas do AD local, consulte [Integração de entidades locais com o Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Se você tem dispositivos móveis ou computadores Mac que autenticam localmente usando AD FS ou um provedor de autenticação equivalente:
> 
> -   Você deve usar o AD FS na versão mínima do servidor **Windows Server 2012 R2** ou um provedor de autenticação alternativo que dê suporte ao protocolo OAuth 2.0.

## Multi-Factor Authentication (MFA) e Azure RMS
Para usar o Multi-Factor Authentication (MFA) com o Azure RMS, é necessária uma das seguintes opções:

-   Office 2013 (versão mínima):

    -   Se você tiver o Office 2013, instale também a [atualização para o Office 2013 (KB3054853) de 9 de junho de 2015](https://support.microsoft.com/kb/3054853). Para obter mais informações sobre esta atualização e sobre como a autenticação moderna traz a conexão baseada na ADAL (Active Directory Authentication Library) para o Office 2013, consulte [Preview pública de autenticação moderna do Office 2013 anunciada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) no blog do Office.

-   Aplicativo Rights Management sharing para Windows:

    -   Você deve ter instalada a versão mínima do 1.0.1908.0, que pode ser confirmada através do Painel de controle, Programas e Recursos. Para obter mais informações sobre o aplicativo de compartilhamento, consulte [Aplicativo de compartilhamento do Rights Management para Windows](../rms-client/sharing-app-windows.md).

-   Aplicativo Rights Management sharing para dispositivos móveis e computadores Mac:

    -   Certifique-se de que tenha a versão mais recente instalada. O suporte a MFA entrou em vigor na versão de setembro de 2015 do aplicativo RMS sharing.

Em seguida, configure sua solução MFA:

-   Para locatários gerenciados pela Microsoft (necessário Active Directory do Azure ou Office 365):

    -   Configure o Azure MFA para impor o MFA para usuários. Para obter instruções, consulte [Introdução ao Azure Multi-Factor Authentication na nuvem](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) na documentação do Multi-factor Authentication.

        Para obter mais informações sobre o Azure MFA, consulte [O que é o Azure Multi-Factor Authentication?](/multi-factor-authentication/multi-factor-authentication)

-   Para locatários federados (você opera servidores de federação no local):

    -   Configure seus servidores de federação para o Active Directory do Azure ou o Office 365. Por exemplo, se você estiver usando o AD FS, consulte [Configurar métodos de autenticação adicionais do AD FS](https://technet.microsoft.com/library/dn758113.aspx) no TechNet.

        Para obter mais informações sobre esse cenário, consulte [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) (O Works with Office 365 – Programa de identidade agora simplificado) no blog do Office.

## Próximas etapas
Para verificar se há outros requisitos, consulte [Requisitos do Azure Rights Management](requirements-azure-rms.md).



<!--HONumber=Apr16_HO4-->


