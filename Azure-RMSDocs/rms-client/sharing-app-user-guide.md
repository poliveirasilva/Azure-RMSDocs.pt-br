---
title: "Guia do usuário do aplicativo compartilhamento Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 46e5d3c9ea001d2fa157187a8b78c2dc3e6516f3


---

# Guia do usuário do aplicativo de compartilhamento Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

O aplicativo de compartilhamento Microsoft Rights Management (RMS) do Windows lhe ajuda a proteger imagens e documentos importantes contra pessoas que não devem vê-los, mesmo se você os enviar por email ou salvá-los em outro dispositivo. Use também esse aplicativo para abrir e usar arquivos que outras pessoas tenham protegido usando a mesma tecnologia do Rights Management.

Tudo de que você precisa é um computador que executa pelo menos Windows 7 com Service Pack 1. Em seguida, [baixe e instale o](http://go.microsoft.com/fwlink/?LinkId=303970) este aplicativo gratuito da Microsoft.

Se você tiver dúvidas não foram respondidas por este guia, consulte [Perguntas frequentes do aplicativo de compartilhamento Microsoft Rights Management para Windows](http://go.microsoft.com/fwlink/?LinkId=303971). Essa página também contém algumas informações de solução de problemas, caso você tenha problemas.

## Exemplos de uso do aplicativo RMS sharing
Estes são apenas alguns exemplos de como você pode usar o aplicativo RMSsharing para ajudar a proteger seus arquivos.

|Eu quero...|Como fazer isso|
|----------------|------------------|
|**… compartilhar com segurança as informações financeiras com alguém de confiança que trabalhe em outra organização**<br /><br />Você trabalhar com uma empresa parceira e deseja enviar-lhes por email uma planilha do Excel que contém os dados de projeção de vendas. Você quer que eles possam ver os dados, mas não alterá-los.|Use o botão **Compartilhamento protegido** na faixa de opções no Excel, digite os endereços de email das duas pessoas que trabalham com a empresa parceira, selecione **Visualizador – somente exibição**, e clique em **Enviar**.<br /><br />Quando o email chega na empresa do parceiro, apenas os destinatários de email podem ver a planilha e não podem salvá-la, editá-la, imprimi-la ou encaminhá-la.<br /><br />Passo a passo: [Proteger um arquivo que você compartilha por email usando o aplicativo de compartilhamento Rights Management](sharing-app-protect-by-email.md).|
|**… enviar com segurança um documento por email para alguém que usa um dispositivo iOS**<br /><br />Você quer enviar por email um documento do Word altamente confidencial para uma colega de trabalho que você sabe que verifica os emails regularmente em um dispositivo iOS.|Usando o Explorador de Arquivos, clique com o botão direito do mouse no arquivo e selecione **Compartilhamento Protegido**. envie o arquivo como um anexo para sua colega.<br /><br />O destinatário recebe um email em seu dispositivo iOS. Já que ela não tem o Office para iPad e iPhone, ela clica no link no email que a instrui sobre como baixar o aplicativo de compartilhamento, instala a versão para dispositivos iOS e exibe o documento¹.<br /><br />Passo a passo: [Proteger um arquivo que você compartilha por email usando o aplicativo de compartilhamento Rights Management](sharing-app-protect-by-email.md).|
|**… verificar quem abriu meus documentos protegidos e quando revogar o acesso se necessário**<br /><br />Você compartilhou com segurança um documento de um projeto confidencial com fornecedores potenciais, e agora quer ver quem acessou, quando e de onde. Depois, quando um dos fornecedores receber o negócio, é recomendável revogar o acesso ao documento original para que as pessoas com quem você compartilhou não possam mais acessá-lo.|Depois de compartilhar um documento por email, acesse o [site de rastreamento de documentos](http://go.microsoft.com/fwlink/?LinkId=529562) para verificar quem acessou esse documentos e quando. Quando precisar parar de compartilhá-lo, selecione a opção de revogar acesso.<br /><br />Passo a passo: [Rastrear e revogar seus documentos ao usar o aplicativo RMS sharing](sharing-app-track-revoke.md).|
|**… ler um anexo que recebi em uma mensagem de email com um anexo de arquivo compartilhado com segurança, mas não consigo lê-lo porque minha empresa não usa o Rights Management**<br /><br />O remetente do email é alguém de sua confiança, pois vocês já fez negócios juntos antes, e você suspeita de que ele pode enviar informações sobre uma nova oportunidade de negócios potenciais.|Siga as instruções no email e clique no link para inscrever-se no Microsoft Rights Management. A Microsoft confirma que sua organização não tem uma assinatura que inclui o Azure Rights Management, envia um email a você para concluir o processo de inscrição gratuita e você faz logon com sua nova conta. Clique no segundo link no email para instalar o aplicativo de compartilhamento Rights Management e abra o anexo de email para ler sobre as novas oportunidades de negócios.<br /><br />Passo a passo: [Exibir e usar arquivos que foram protegidos pelo Rights Management](sharing-app-view-use-files.md).|
|**… proteger arquivos confidenciais de empresa no meu laptop para que eles não possam ser acessados por pessoas fora da minha empresa**<br /><br />Você viaja muito e usa seu laptop para acessar e atualizar arquivos em uma pasta que deve ser protegida contra acesso não autorizado.|Você tem o aplicativo RMS sharing instalado no seu laptop. Use o Explorador de Arquivos para proteger os arquivos usando um modelo, o que protege rapidamente os arquivos. Se seu laptop for roubado, você terá a tranquiliddade de que ninguém fora da sua empresa pode acessar esses documentos.<br /><br />Passo a passo: [Proteger um arquivo em um dispositivo &#40;proteger in-loco&#41; usando o aplicativo Rights Management sharing](sharing-app-protect-in-place.md).|
¹ Renderização de PDF por Foxit. Copyright © 2003–2014 by Foxit Corporation.

## O que você deseja fazer?
> [!NOTE]
> Para obter informações técnicas, como tipos de arquivo com suporte e como instalar esse aplicativo em uma rede corporativa, consulte o [guia de administrador do aplicativo de compartilhamento Rights Management](sharing-app-admin-guide.md).

-   [Baixar e instalar o aplicativo de compartilhamento](install-sharing-app.md)

-   [Proteger um arquivo em um dispositivo (proteger in-loco)](sharing-app-protect-in-place.md)

-   [Proteger um arquivo que você compartilha por email](sharing-app-protect-by-email.md)

-   [Rastrear e revogar seus documentos](sharing-app-track-revoke.md)

-   [Exibir e usar os arquivos que foram protegidos](sharing-app-view-use-files.md)

-   [Remover a proteção de um arquivo](sharing-app-remove-protection.md)

-   [Usar atalhos de teclado](sharing-app-keyboard-shortcuts.md)

-   [Especificar as configurações na caixa de diálogo](sharing-app-dialog-box.md)






<!--HONumber=Jun16_HO4-->


