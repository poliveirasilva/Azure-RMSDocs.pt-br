---
# required metadata

title: Requisitos do Azure RMS&#58; Assinaturas de nuvem | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/25/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6a16e890-3c3e-4f47-80ca-176a34bdf8bc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisitos do Azure RMS: assinaturas de nuvem | que dão suporte ao Azure RMS

*Aplica-se a: Azure Rights Management, Office 365*

Para usar o Azure RMS (Azure Rights Management), sua organização deve ter pelo menos uma das seguintes assinaturas com um número suficiente de licenças para usuários e serviços que protegerão arquivos e mensagens de email. Se você tiver um serviço que aplique a proteção para os usuários (os proprietários dos arquivos ou mensagens de email), os usuários precisam de uma dessas licenças. Os usuários que só irão consumir (por exemplo, ler e editar) esses dados protegidos não precisam de uma licença.

-   Office 365

-   Azure Rights Management Premium (anteriormente Azure RMS Standalone)

-   Enterprise Mobility Suite

-   RMS para pessoas físicas

Use as seções a seguir para obter mais informações e opções de inscrição.

Para obter uma comparação do licenciamento dos recursos do Azure RMS para as assinaturas pagas, consulte [Comparação das ofertas de RMS (Rights Management Services)](http://technet.microsoft.com/dn858608).

Você tem mais dúvidas sobre o licenciamento para Azure RMS? Baixe o documento **Perguntas frequentes sobre o licenciamento para o Azure Rights Management** na página [Compra do Azure Rights Management](https://www.microsoft.com/en-us/server-cloud/products/azure-rights-management/Purchasing.aspx). 

## Assinatura do Office 365
[Avaliação de 30 dias gratuita: Enterprise E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

Essa assinatura foi desenvolvida para organizações que desejam utilizar os serviços online do Office e usar o recurso IRM (Gerenciamento de Direitos de Informação), que usa o Azure RMS. No entanto, nem todas as assinaturas do Office 365 incluem o Azure RMS.

Assinatura  |Inclui o IRM 
------------- | ------------- |
Office 365 Business Essentials|Não|
Office 365 Business Premium|Não|
Office 365 Enterprise E1 <br /><br /> Office 365 Education A1|Não <br /><br /> Não|
Office 365 Enterprise E3 <br /><br /> Office 365 Education A3 <br /><br /> Office 365 Government G3|Sim <br /><br /> Sim <br /><br /> Sim|
Office 365 Enterprise E4 <br /><br /> Office 365 Education A4 <br /><br /> Office 365 Government G4|Sim <br /><br /> Sim <br /><br /> Sim|
Office 365 Enterprise E5 <br /><br /> Office 365 Education A5|Sim <br /><br /> Sim|
Office 365 Enterprise K1|Não|
SharePoint Plan 1 <br /><br /> SharePoint Plan 2|Não <br /><br /> Não|
Exchange Online Plan 1 <br /><br /> Exchange Online Plan 2|Não <br /><br /> Não|


## Assinatura Premium do Azure Rights Management
[Avaliação gratuita de 30 dias](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

Essa assinatura era conhecida anteriormente como Azure RMS Standalone e foi projetada para organizações que desejam usar o Azure RMS para Office 365, mas que ainda não têm uma assinatura do Office que inclua o Azure RMS. Por exemplo, se tiver uma assinatura do Office 365 Business Essentials ou Office 365 Enterprise E1, essas assinaturas não incluirão o Azure RMS (consulte a tabela na seção anterior). 

Para usar o Azure RMS com qualquer uma das assinaturas do Office que não incluem o Azure RMS, você pode comprar uma assinatura Premium do Azure Rights Management. Ou comprar outra assinatura do Office que inclui o Azure RMS, como o Office 365 Enterprise E4.

> [!NOTE]
> Ao usar essa assinatura com o Office 365 Business Premium, há algumas restrições de cliente. Você pode proteger o conteúdo e consumir conteúdo protegido com o RMS usando o Outlook Web App e o aplicativo RMS sharing. Você pode consumir o conteúdo protegido, mas não pode proteger conteúdo, usando todos os outros aplicativos do Office, o que inclui o Office Online e os aplicativos cliente do Office 365 Business Premium.

Para obter mais informações sobre a assinatura Premium do Azure Rights Management, consulte [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management).

Essa assinatura também oferece um período de avaliação para testar o Azure RMS para 25 usuários, sem custo. 

### O quê acontece quando a assinatura de avaliação expira?
Se sua assinatura de avaliação expirar, você perderá acesso ao conteúdo que foi protegido usando sua assinatura de avaliação para o Azure RMS. No entanto, se você compra uma assinatura que dá suporte ao Azure RMS, o acesso é automaticamente restaurado.

Uma exceção à perda de acesso após a expiração é se a sua organização usou o Azure RMS com o RMS para assinaturas de pessoa física antes de ter obtido a assinatura de avaliação. Depois, o acesso à conteúdo anteriormente protegido permanece, mesmo depois que a assinatura de avaliação expira.

## Assinatura do Enterprise Mobility Suite
[Avaliação gratuita de 30 dias](http://go.microsoft.com/fwlink/?LinkId=615385)

Essa assinatura foi desenvolvida para organizações que querem usar uma combinação do Azure Active Directory Premium, do Windows Intune e do Azure Rights Management. O suporte para usar o Azure Rights Management com o Office é o mesmo que usar a assinatura Premium do Azure Rights Management. Para obter mais informações sobre a assinatura do Enterprise Mobility Suite, consulte a [Visão geral do Microsoft Enterprise Mobility](http://go.microsoft.com/fwlink/?LinkId=615386).

## Assinatura do RMS para indivíduos
Esta assinatura foi desenvolvida para indivíduos de uma organização que não implantou o Azure RMS ou o AD RMS. Ela permite que essas pessoas leiam conteúdo protegido por uma organização que use o Azure RMS, e também podem proteger seus próprios conteúdos.

Você pode ver isso listado no portal de administração do Office 365 como **Ad hoc do Rights Management** e atribuído automaticamente aos usuários. Não atribua manualmente esta licença aos usuários e não use esta licença para administrar o Azure RMS para sua organização. 

Para saber mais, confira [RMS para pessoas físicas e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## Próximas etapas
Para verificar se há outros requisitos, consulte [Requisitos do Azure Rights Management](requirements-azure-rms.md).

<!--HONumber=May16_HO5-->


