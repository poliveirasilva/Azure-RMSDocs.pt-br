---
# required metadata

title: Requisitos do Azure RM&#58; aplicações | Azure RMS
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


# Requisitos do Azure RMS: aplicações

*Aplica-se a: Azure Rights Management, Office 365*


Utilize a seguinte tabela para identificar as aplicações que suportam nativamente o Azure RMS, o que significa que o RMS está totalmente integrado nestas aplicações ao utilizar as APIs de RMS para suportar restrições de utilização. Estas aplicações também são conhecidas como otimizadas por RMS.

Salvo indicação em contrário, as capacidades suportadas aplicam-se ao Azure RMS e ao AD RMS. Além disso, o suporte do AD RMS em iOS, Android, OS X e Windows Phone 8.1 necessita da [Extensão de Dispositivos Móveis dos Serviços de Gestão de Direitos do Active Directory](https://technet.microsoft.com/library/dn673574.aspx).

Informações acerca das colunas da tabela:

-   **PDF protegido**: ficheiros que têm uma extensão de nome de ficheiro .ppdf e que são criados automaticamente quando utiliza a aplicação de partilha RMS para partilhar ficheiros do Office e ficheiros PDF por e-mail. A aplicação de partilha RMS inclui um leitor para ficheiros PDF protegidos. Se anteriormente tiver criado ficheiros PDF que protegeu ao utilizar o Azure RMS ou o AD RMS, pode continuar a ler estes ficheiros em dispositivos com Windows, iOS e Android através do Foxit Reader e do Nitro Pro.

-   **E-mail:** os clientes de e-mail listados podem proteger a própria mensagem de e-mail, que protegerá automaticamente quaisquer ficheiros anexados. Neste cenário, a funcionalidade de pré-visualização do cliente pode apresentar o conteúdo protegido (mensagem e anexos) aos destinatários autorizados. No entanto, se uma mensagem de e-mail em si não estiver protegida mas o anexo estiver protegido, a funcionalidade de pré-visualização do cliente não conseguirá apresentar o anexo protegido aos destinatários autorizados.

-   **Outros tipos de ficheiro**: os ficheiros de texto e imagem incluem ficheiros que tenham uma extensão de nome de ficheiro .txt, .xml, .jpg e .jpeg. Estes ficheiros alteram a respetiva extensão de nome de ficheiro depois de serem nativamente protegidos pelo RMS e passam a ser só de leitura. Os ficheiros que não podem ser protegidos nativamente têm uma extensão de nome de ficheiro .pfile depois de serem protegidos genericamente pelo RMS. Para obter mais informações, consulte o [Guia do administrador da aplicação de partilha Rights Management](../rms-client/sharing-app-admin-guide.md).


|**Sistema operativo do dispositivo**|Word, Excel, PowerPoint|PDF protegido|E-mail|Outros tipos de ficheiro|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Aplicações do Office Mobile (apenas para Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Aplicação de partilha RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](footnote-3)<br /><br />Windows Mail [[4]](footnote-4)|Aplicação de partilha RMS para Windows: texto, imagens, pfile<br /><br />Siemens JT2Go: ficheiros JT (apenas para Windows 10)|
|**iOS**|Office para iPad e iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|Foxit Reader<br /><br />Aplicação de partilha RMS [[1]](#footnote-1)<br /><br />TITUS Docs|Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para iPad e iPhone [[4]](#footnote-4)<br /><br />OWA para iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Aplicação de partilha RMS [[1]](#footnote-1): texto, imagens, pfile<br /><br />TITUS Docs: Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)|GigaTrust App for Android<br /><br />Foxit Reader<br /><br />Aplicação de partilha RMS [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook para Android [[4]](#footnote-4)<br /><br />OWA para Android [[3]](#footnote-3) e [[7]](#footnote-7)<br /><br />Samsung Email (S3 e posterior) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Aplicação de partilha RMS [[1]](#footnote-1): texto, imagens, pfile|
|**OS X**|Office 2011 (apenas para AD RMS)<br /><br />Office 2016 para Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Aplicação de partilha RMS [[1]](#footnote-1)|Outlook 2011 (apenas para AD RMS)<br /><br />Outlook 2016 para Mac<br /><br />Outlook para Mac|Aplicação de partilha RMS [[1]](#footnote-1): texto, imagens, pfile|
|**Windows 10 Mobile**|Aplicações do Office Mobile (apenas para Azure RMS)[[1]](#footnote-1)|Não suportado|Citrix WorxMail [[6]](#footnote-6)<br /><br />Correio do Outlook|Não suportado|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Não suportado|Outlook 2013 RT<br /><br />Aplicação Correio para Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: ficheiros JT|
|**Windows Phone 8.1**|Office Mobile (apenas para AD RMS)|Aplicação de partilha RMS [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Aplicação de partilha RMS [[1]](#footnote-1): texto, imagens, pfile|
|**Blackberry 10**|Não suportado|Não suportado|E-mail Blackberry [[4]](#footnote-4)|Não suportado|


###### Nota de rodapé 1
Suporta a visualização de conteúdo protegido.

###### Nota de rodapé 2 
Suporta a visualização de conteúdo protegido no SharePoint Online, no OneDrive para Empresas e no Outlook Web Access.

###### Nota de rodapé 3
Se um destinatário tiver uma caixa de correio do Exchange no local e receber uma mensagem de e-mail protegida, este conteúdo pode ser aberto apenas num cliente de e-mail avançado, como o Outlook.  Não é possível abrir este conteúdo no Outlook Web Access.

###### Nota de rodapé 4
Utiliza a IRM do Exchange ActiveSync, que tem de ser ativada pelo administrador do Exchange. Os utilizadores podem ver, responder e responder a todos em mensagens de e-mail protegidas, mas não podem proteger novas mensagens de e-mail.

Se um destinatário tiver uma caixa de correio do Exchange no local e receber um e-mail protegido de outra organização que esteja a utilizar o Exchange, este conteúdo pode ser aberto apenas num cliente de e-mail avançado, como o Outlook.  Não é possível abrir este conteúdo num dispositivo que utiliza a IRM do Exchange Active Sync.

###### Nota de rodapé 5
Suporta a visualização e a edição de documentos protegidos. Para obter mais informações, consulte a seguinte publicação no blogue do Office: [Suporte do Azure Rights Management chega ao Office para iPad e iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### Nota de rodapé 6
Para obter mais informações, consulte a [documentação do produto Citrix para WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

###### Nota de rodapé 7
Para obter mais informações, consulte a seguinte publicação no blogue do Office: [OWA para Android, agora disponível em determinados dispositivos](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## Mais informações sobre o suporte do Azure RMS para o Office

Todas as edições do Office (à exceção do Office 2007) suportam o consumo de conteúdo protegido.

O Azure RMS com Office Professional Plus 2010 ou Office Professional 2010:

- Necessita da aplicação de partilha Rights Management para Windows

- Não suportado no Windows 10


## Mais informações sobre a aplicação de partilha Rights Management

Para obter mais informações acerca da aplicação de partilha Rights Management para Windows, consulte os seguintes recursos:

-   [Guia do administrador da aplicação de partilha Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guia do utilizador da aplicação de partilha Rights Management](../rms-client/sharing-app-user-guide.md)

Para obter mais informações acerca da aplicação de partilha Rights Management para plataformas móveis, consulte os seguintes recursos:

-   Transferir a aplicação relevante utilizando as ligações na [página Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   Se tiver o Microsoft Intune, pode implementar e gerir a aplicação através de uma aplicação gerida por política: 

    -   Para os dispositivos iOS e Android que estão inscritos pelo Intune: [Configurar e implementar políticas de gestão de aplicações móveis na consola do Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)

    -   Para os dispositivos Android que não estão inscritos pelo Intune: [Criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)

-   [FAQ acerca da Aplicação de Partilha Microsoft Rights Management para Plataformas Móveis](https://technet.microsoft.com/dn451248)



## Mais informações sobre outras aplicações que suportem o Azure RMS

Para além das aplicações na tabela, qualquer aplicação que suporte essas APIs do RMS pode ser integrada com o Azure RMS, que inclui:

- Aplicações de linha de negócio que são escritas internamente através do SDK RMS

- Aplicações de fornecedores de software que são escritas através do SDK RMS.

Para mais informações acerca do SDK, consulte o [SDK Microsoft Rights Management](../develop/developers-guide.md).

## Aplicações que não são suportadas pelo Azure RMS

As aplicações seguintes não são atualmente suportadas pelo Azure RMS incluem o seguinte:

-   Microsoft Office para Mac 2011

-   Microsoft OneDrive para Empresas para o SharePoint Server 2013

-   Visualizador XPS
 
Além disso, a aplicação de partilha RMS tem as seguintes restrições:

-   Para computadores com o Windows: necessita de uma versão mínima do Windows 7 Service Pack 1



## Passos seguintes
Para verificar outros requisitos, consulte [Requisitos do Azure Rights Management](requirements-azure-rms.md).

Para obter mais informações sobre como as aplicações utilizadas com mais frequência suportam o Azure RMS, consulte [Como é que as aplicações suportam o Azure Rights Management](../understand-explore/applications-support.md).

Para obter informações sobre como configurar as aplicações utilizadas com mais frequência para o Azure RMS, consulte [Configurar aplicações para o Azure Rights Management](../deploy-use/configure-applications.md).

<!--HONumber=May16_HO2-->


