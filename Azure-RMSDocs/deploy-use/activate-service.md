---
# required metadata

title: Ativando o Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Ativando o Azure Rights Management
Quando você ativa o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), sua organização pode começar a proteger dados importantes por meio de aplicativos e serviços que dão suporte a essa solução de proteção de informações. Os administradores também podem gerenciar e monitorar arquivos protegidos e emails que sua organização possui. Você deve habilitar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] antes de começar a usar os recursos de IRM (Gerenciamento de Direitos de Informação) no Office, no SharePoint e no Exchange e proteger qualquer arquivo sensível ou confidencial.

Se você quiser saber mais sobre o Azure Rights Management antes de ativar o serviço - por exemplo, quais problemas de negócios ele resolve, alguns casos típicos de uso e como funciona - consulte [O que é o Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Antes de ativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], certifique-se de que sua organização tenha um plano de serviço que inclua serviços [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Caso contrário, você não poderá ativar o Azure RMS.
>
> Para obter mais informações, consulte [Assinaturas de nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).

Depois de ter ativado o Azure RMS, todos os usuários em sua organização podem aplicar proteção de informações aos seus arquivos e todos os usuários podem abrir (consumir) os arquivos que foram protegidos pelo Azure RMS. No entanto, se você preferir, pode restringir quem pode aplicar proteção de informações por meio de controles de integração para uma implantação em fases. Para obter mais informações, consulte a seção [Configurando controles de integração para uma implantação em fases](#configuring-onboarding-controls-for-a-phased-deployment) neste artigo.

Para obter instruções como ativar o Rights Management, selecione se você usará o centro de administração do Office 365 (preview ou clássico) ou o portal de gerenciamento clássico do Azure:


- [Centro de administração do Office 365 - preview](activate-office365-preview.md)
- [Centro de administração do Office 365 - clássico](activate-office365-classic.md)
- [Portal clássico do Azure](activate-azure-classic.md)

> [!TIP]
> Você também pode usar o cmdlet do Windows PowerShell, [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx), para ativar [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

## Configurando controles de integração para uma implantação em fases
Se você não deseja que todos os usuários consigam proteger os arquivos imediatamente usando o Azure RMS, poderá configurar os controles de integração usando o comando Windows PowerShell [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) . Você pode executar esse comando antes ou depois de ativar o Azure RMS.

> [!IMPORTANT]
> Para usar esse comando, você deve ter pelo menos a versão **2.1.0.0** do módulo [RMS Windows PowerShell do Azure](http://go.microsoft.com/fwlink/?LinkId=257721).
>
> Para verificar a versão instalada, execute: **(Get-Module aadrm –ListAvailable).Version**

Por exemplo, se você deseja inicialmente que os administradores no grupo “Departamento de TI” (que tem uma ID de objeto de fbb99ded-32a0-45f1-b038-38b519009503) consigam proteger o conteúdo para fins de teste, use o seguinte comando:

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
Observe que para essa opção de configuração, você deve especificar um grupo; você não pode especificar os usuários individuais.

Ou, se você quiser garantir que apenas os usuários que estão corretamente licenciados para usar o Azure RMS podem proteger o conteúdo:

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
Quando você usa esses controles de integração, todos os usuários da organização sempre podem consumir o conteúdo protegido que tenha sido protegido por seu subconjunto de usuários, mas eles não conseguirão aplicar a proteção de informações sozinhos a partir de aplicativos cliente. Por exemplo, eles não verão em seus clientes Office os modelos padrão que são publicados automaticamente quando o Azure RMS é ativado ou modelos personalizados que você possa configurar.  Aplicativos do lado do servidor, como o Exchange, podem implementar seus próprios controles de usuário para integração do RMS para obter o mesmo resultado.


## Próximas etapas
Agora que você ativou o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para sua organização, use o [Mapa de Implantação do Azure Rights Management](../plan-design/deployment-roadmap.md) para verificar se existem outras etapas de configuração que você possa precisar executar antes de implantar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para os usuários e administradores. 

Por exemplo, você talvez queira usar [modelos personalizados](configure-custom-templates.md) para facilitar que os usuários apliquem a proteção de informações a arquivos, conectem os servidores locais para usar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] por meio da instalação do [conector RMS](deploy-rms-connector.md), e implantem o [aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-windows.md) que dá suporte à proteção de todos os tipos de arquivo em todos os dispositivos. 

Serviços do Office, como o Exchange Online e o SharePoint Online, exigem configuração adicional antes de usar os recursos do IRM (Information Rights Management). 
Para obter informações sobre como os aplicativos funcionam com o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Como os aplicativos dão suporte ao Azure Rights Management](../understand-explore/applications-support.md).



<!--HONumber=Apr16_HO3-->


