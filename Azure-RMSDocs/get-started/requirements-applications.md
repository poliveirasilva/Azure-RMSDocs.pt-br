---
# required metadata

title: "Requisitos do Azure RMS: aplicativos | Azure RMS"
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisitos do Azure RMS: aplicativos

*Aplica-se a: Azure Rights Management, Office 365*


Use a tabela a seguir para identificar os aplicativos que oferecem suporte nativo ao Azure RMS nativamente, ou seja, o RMS é totalmente integrado a esses aplicativos usando as APIs do RMS a fim de oferecer suporte às restrições de uso. Esses aplicativos também são conhecidos como aprimorados pelo RMS.

A menos que exista indicação em contrário, os recursos com suporte se aplicam ao Azure RMS e ao AD RMS. Além disso, o suporte do AD RMS no iOS, no Android, no OS X e no Windows Phone 8.1 requer a [Extensão de dispositivo móvel do Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Informações sobre as colunas da tabela:

-   **PDF protegido**: os arquivos com extensão de nome de arquivo .ppdf e que são criados automaticamente quando você usa o aplicativo de compartilhamento do RMS para compartilhar arquivos do Office e arquivos PDF por email. O aplicativo de compartilhamento do RMS inclui um leitor para arquivos PDF protegidos. Antes de tudo, se você tiver criado arquivos PDF protegidos usando o Azure RMS ou o AD RMS, poderá continuar a ler esses arquivos nos dispositivos Windows, iOS e Android usando o Foxit Reader e o Nitro Pro.

-   **Email:** os clientes de email listados podem proteger a própria mensagem de email, o que protege arquivos anexados automaticamente. Neste cenário, o recurso de pré-visualização do cliente pode exibir o conteúdo protegido (mensagem e anexo) para os destinatários autorizados. No entanto, se uma mensagem de email por si só não estiver protegida, mas o anexo estiver protegido, o recurso de visualização do cliente não poderá exibir o anexo protegido para os destinatários autorizados.

-   **Outros tipos de arquivo**: arquivos de texto e imagem incluem arquivos com uma extensão de nome de arquivo como .txt, .xml, .jpg e jpeg. Esses arquivos alteram sua extensão de nome de arquivo depois de serem protegidos nativamente pelo RMS, tornando-se somente leitura. Os arquivos que não podem ser protegidos nativamente têm uma extensão do nome de arquivo .pfile após serem protegidos genericamente pelo RMS. Para saber mais, confira o [Guia do administrador do aplicativo de compartilhamento do Rights Management](../rms-client/sharing-app-admin-guide.md).


|**Sistema operacional do dispositivo**|Word, Excel, PowerPoint|PDF protegido|Email|Outros tipos de arquivos|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Aplicativos Office Mobile (somente Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client para Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Aplicativo RMS sharing|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](footnote-3)<br /><br />Windows Mail [[4]](footnote-4)|Aplicativo de compartilhamento RMS para Windows: texto, imagens, pfile<br /><br />Siemens JT2Go: arquivos JT (somente Windows 10)|
|**iOS**|Office para iPad e iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|Foxit Reader<br /><br />Aplicativo de compartilhamento de RMS [[1]](#footnote-1)<br /><br />TITUS Docs|Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para iPad e iPhone [[4]](#footnote-4)<br /><br />OWA para iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Aplicativo de compartilhamento de RMS [[1]](#footnote-1): Texto, imagens, pfile<br /><br />TITUS Docs: Pfile|
|**Android**|GigaTrust App para Android<br /><br />Office Online [[2]](#footnote-2)|GigaTrust App para Android<br /><br />Foxit Reader<br /><br />Aplicativo de compartilhamento de RMS [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App para Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para Android [[4]](#footnote-4)<br /><br />OWA para Android [[3]](#footnote-3) and [[7]](#footnote-7)<br /><br />Samsung Email (S3 e posterior) [[7]](#footnote-7)<br /><br />Classificação TITUS para dispositivos móveis|Aplicativo de compartilhamento de RMS [[1]](#footnote-1): Texto, imagens, pfile|
|**OS X**|Office 2011 (somente do AD RMS)<br /><br />Office 2016 para Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Aplicativo de compartilhamento de RMS [[1]](#footnote-1)|Outlook 2011 (somente do AD RMS)<br /><br />Outlook 2016 para Mac<br /><br />Outlook para Mac|Aplicativo de compartilhamento de RMS [[1]](#footnote-1): Texto, imagens, pfile|
|**Windows 10 Mobile**|Aplicativos do Office Mobile (somente Azure RMS)[[1]](#footnote-1)|Sem suporte|Citrix WorxMail [[6]](#footnote-6)<br /><br />Email do Outlook|Sem suporte|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Sem suporte|Outlook 2013 RT<br /><br />Aplicativo de email para o Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: arquivos JT|
|**Windows Phone 8.1**|Office Móvel (somente do AD RMS)|Aplicativo de compartilhamento de RMS [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Aplicativo de compartilhamento de RMS [[1]](#footnote-1): Texto, imagens, pfile|
|**Blackberry 10**|Sem suporte|Sem suporte|Email do Blackberry [[4]](#footnote-4)|Sem suporte|


###### Nota de rodapé 1
oferece suporte à exibição de conteúdo protegido.

###### Nota de rodapé 2 
oferece suporte à exibição de conteúdo protegido no SharePoint Online, OneDrive for Business e Outlook Web Access.

###### Nota de rodapé 3
se um destinatário tem uma caixa de correio no Exchange no local e recebe um email protegido, esse conteúdo pode ser aberto apenas em um cliente de email com formatação, como o Outlook.  Esse conteúdo não pode ser aberto no Outlook Web Access.

###### Nota de rodapé 4
usa o Exchange ActiveSync IRM, que deve ser habilitado pelo administrador do Exchange. Os usuários podem exibir, responder e responder a todos para mensagens de email protegidas, mas os usuários não podem proteger novas mensagens de email.

Se um destinatário tem uma caixa de correio no Exchange no local e recebe um email protegido de outra organização que usa Exchange, esse conteúdo pode ser aberto apenas em um cliente de email com formatação, como o Outlook.  Esse conteúdo não pode ser aberto em um dispositivo que usa o Exchange Active Sync IRM.

###### Nota de rodapé 5
oferece suporte à exibição e edição de documentos protegidos. Para saber mais, confira a seguinte postagem no blog do Office: [Azure Rights Management support comes to Office for iPad and iPhone (O suporte ao Azure Rights Management chega até o Office para iPad e iPhone)](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### Nota de rodapé 6
Para obter mais informações, consulte [Documentação de produto para WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

###### Nota de rodapé 7
Para saber mais, confira a seguinte postagem no blog do Office: [OWA for Android now available on select devices (OWA para Android já disponível em dispositivos selecionados)](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## Para saber mais sobre o suporte do Azure RMS para Office

Todas as edições do Office (com exceção do Office 2007) oferecem suporte ao consumo de conteúdo protegido.

Azure RMS com o Office Professional Plus 2010 ou o Office Professional 2010:

- Requer o aplicativo de compartilhamento do Rights Management para Windows

- Sem suporte no Windows 10


## Saiba mais informações sobre o aplicativo de compartilhamento do Rights Management

Para obter mais informações sobre o aplicativo de compartilhamento do Rights Management do Windows, consulte os seguintes recursos:

-   [Guia do administrador do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guia do usuário do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-user-guide.md)

Para obter mais informações sobre o aplicativo de compartilhamento do Rights Management para plataformas móveis, consulte os seguintes recursos:

-   Baixe o aplicativo relevante usando os links na [página do Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   Se você tiver o Microsoft Intune, poderá implantar e gerenciar o aplicativo usando um aplicativo gerenciado por política: 

    -   Para dispositivos iOS e Android registrados pelo Intune: [Configurar e implantar políticas de gerenciamento de aplicativo móvel no console do Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)

    -   Para dispositivos Android que não estão registrados pelo Intune: [Configurar e implantar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune).

-   [Perguntas frequentes para os aplicativos de compartilhamento do Microsoft Rights Management para Plataformas Móveis](https://technet.microsoft.com/dn451248)



## Saiba mais sobre outros aplicativos que dão suporte ao Azure RMS

Além dos aplicativos na tabela, qualquer aplicativo que ofereça suporte a APIs de RMS pode ser integrado ao Azure RMS, incluindo:

- Aplicativos de linha de negócios escritos internamente com o RMS SDK

- Aplicativos de fornecedores de software que são escritos usando o RMS SDK

Para saber mais sobre o SDK, veja [Microsoft Rights Management SDK](../develop/developers-guide.md).

## Aplicativos que não têm suporte do Azure RMS

Os aplicativos que atualmente não têm suporte do Azure RMS incluem os seguintes:

-   Microsoft Office for Mac 2011

-   Microsoft OneDrive for Business para SharePoint Server 2013

-   Visualizador XPS
 
Além disso, o aplicativo de compartilhamento do RMS tem as seguintes restrições:

-   Para computadores Windows: requer uma versão mínima do Windows 7 Service Pack 1



## Próximas etapas
Para verificar se há outros requisitos, veja [Requisitos do Azure Rights Management](requirements-azure-rms.md).

Para saber mais sobre como os aplicativos usados com mais frequência oferecem suporte ao Azure RMS, veja [Como os aplicativos dão suporte ao Azure Rights Management](../understand-explore/applications-support.md).

Para saber mais sobre como configurar os aplicativos usados com mais frequência para o Azure RMS, veja [Configuração de aplicativos para o Azure Rights Management](../deploy-use/configure-applications.md).

<!--HONumber=May16_HO2-->


