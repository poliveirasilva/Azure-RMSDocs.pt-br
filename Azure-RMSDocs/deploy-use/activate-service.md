---
title: Ativar o Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bf5e3561ef24d8f44e791ff7bdc8450a73f79705
ms.openlocfilehash: d66e4e6bca253bc2bf9d12ba22ed0202cba2edaf


---

# Ativar o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Quando ativar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), a sua organização pode começar a proteger dados importantes através da utilização de aplicações e serviços que suportam esta solução de proteção de informações. Os administradores também podem gerir e monitorizar e-mails e ficheiros protegidos de que a sua organização é proprietária. Tem de ativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] antes de poder começar a utilizar as funcionalidades de gestão de direitos de informação (IRM) no Office, no SharePoint e no Exchange, e proteger um ficheiro sensível ou confidencial.

Se pretender saber mais acerca do Azure Rights Management antes de ativar o serviço (por exemplo, os problemas empresariais que resolve, alguns casos de utilização típicos e como funciona), consulte [O que é o Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Antes de ativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], certifique-se de que a sua organização tem um plano de serviço que inclui serviços do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Caso contrário, não será possível ativar o Azure RMS.
>
> Para mais informações, consulte [Subscrições na nuvem que suportam o Azure RMS](../get-started/requirements-subscriptions.md).

Depois de ter ativado o Azure RMS, todos os utilizadores na sua organização podem aplicar a proteção de informações aos respetivos ficheiros e todos os utilizadores podem abrir (consumir) ficheiros que foram protegidos pelo Azure RMS. No entanto, se preferir, pode restringir quem pode aplicar a proteção de informações, ao utilizar controlos de inclusão para uma implementação faseada. Para obter mais informações, consulte a secção [Configurar os controlos de inclusão para uma implementação faseada](#configuring-onboarding-controls-for-a-phased-deployment) neste artigo.

Para obter instruções acerca de como ativar o Rights Management a partir do portal de gestão, selecione se irá utilizar o centro de administração do Office 365 (pré-visualização ou clássico) ou o portal de gestão clássico do Azure:


- [Centro de administração do Office 365 – pré-visualização](activate-office365-preview.md)
- [Centro de administração do Office 365 – clássico](activate-office365-classic.md)
- [Portal clássico do Azure](activate-azure-classic.md)

Em alternativa, pode utilizar o Windows PowerShell para ativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]:

1. Instale a Ferramenta de Administração do Azure Rights Management, a qual instala o módulo de administração do Azure Rights Management. Para obter instruções, consulte [Instalar o Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

2. A partir de uma sessão do Windows PowerShell, execute [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) e, quando solicitado, forneça os detalhes da conta de administrador global do inquilino do Azure RMS.

3. Execute [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), o qual ativa o serviço Azure RMS.

## Configurar os controlos de inclusão para uma implementação faseada
Se não pretender que todos os utilizadores possam proteger ficheiros imediatamente ao utilizar o Azure RMS, pode configurar os controlos de inclusão do utilizador ao utilizar o comando do Windows PowerShell [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx). Pode executar este comando antes ou depois de ativar o Azure RMS.

> [!IMPORTANT]
> Para executar este comando, tem de ter no mínimo a versão **2.1.0.0** do [módulo do Windows PowerShell para o Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Para verificar a versão que instalou, execute: **Get-Module aadrm –ListAvailable).Version**

Por exemplo, se pretender inicialmente que apenas os administradores no grupo “Departamento de TI” (que tem uma ID de objeto de fbb99ded-32a0-45f1-b038-38b519009503) possam proteger conteúdo para fins de teste, utilize o seguinte comando:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Tenha em atenção que para esta opção de configuração, tem de especificar um grupo. Não é possível especificar utilizadores individuais.

Em alternativa, se pretender certificar-se de que apenas os utilizadores que são licenciados corretamente para utilizar o Azure RMS podem proteger conteúdo:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Quando utilizar estes controlos de inclusão, todos os utilizadores na organização podem sempre consumir conteúdo protegido que foi protegido pelo seu subconjunto de utilizadores, mas não poderão aplicar a proteção de informações a partir de aplicações de cliente. Por exemplo, não poderão ver nos seus clientes do Office os modelos predefinidos que são automaticamente publicados quando o Azure RMS está ativado, ou modelos personalizados que pode configurar.  As aplicações do lado do servidor, como o Exchange, podem implementar os seus próprios controlos por utilizador para a integração do RMS alcançar o mesmo resultado.


## Passos seguintes
Uma vez que ativou o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para a sua organização, utilize o [plano de implementação do Azure Rights Management](../plan-design/deployment-roadmap.md) para verificar se existem outros passos de configuração que necessite de realizar antes de implementar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para utilizadores e administradores. 

Por exemplo, pode querer utilizar [modelos personalizados](configure-custom-templates.md) para que os utilizadores possam mais facilmente aplicar a proteção de informações a ficheiros, ligar os servidores no local para utilizar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] ao instalar o [conector RMS](deploy-rms-connector.md) e implementar a [aplicação de partilha Rights Management](../rms-client/sharing-app-windows.md) que suporta a proteção de todos os tipos de ficheiro em todos os dispositivos. 

Os serviços do Office, como o Exchange Online e o SharePoint Online, necessitam de configuração adicional antes de poder utilizar as respetivas funcionalidades de Gestão de Direitos de Informação (IRM). Para obter informações acerca de como as suas aplicações trabalham com o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [De que forma as aplicações suportam o Azure Rights Management](../understand-explore/applications-support.md).




<!--HONumber=Jun16_HO4-->


