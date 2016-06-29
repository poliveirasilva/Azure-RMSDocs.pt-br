---
# required metadata

title: Guia do utilizador da aplicação de partilha Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guia do utilizador da aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

A aplicação de partilha Microsoft Rights Management (RMS) para Windows ajuda a manter os documentos e imagens importantes protegidos das pessoas que não os deveriam ver, mesmo que os envie por e-mail ou guarde noutro dispositivo. Também pode utilizar esta aplicação para abrir e utilizar ficheiros que tenham sido protegidos por outras pessoas com a mesma tecnologia de Rights Management.

Tudo o que precisa é de um computador que execute, pelo menos, o Windows 7 com Service Pack 1. Em seguida, [transfira e instale](http://go.microsoft.com/fwlink/?LinkId=303970) esta aplicação gratuita da Microsoft.

Se tiver questões que não sejam abordadas neste guia, consulte [FAQ acerca da Aplicação de Partilha Microsoft Rights Management para Windows](http://go.microsoft.com/fwlink/?LinkId=303971). Esta página também inclui algumas informações de resolução de problemas, caso se depare com algum problema.

## Exemplos de utilização da aplicação de partilha RMS
Seguem-se apenas alguns exemplos de como pode utilizar a aplicação de partilha RMS para ajudar a proteger os seus ficheiros.

|Pretendo...|Como proceder|
|----------------|------------------|
|**… partilhar de forma segura informações financeiras com alguém em quem confio e que trabalha noutra organização**<br /><br />Trabalha com uma empresa parceira e pretende enviar-lhe por e-mail uma folha de cálculo do Excel que contém uma estimativa do volume de vendas. Pretende que essas pessoas possam ver os valores, mas não alterá-los.|Utilize o botão **Partilhar Protegido** no friso do Excel, escreva os endereços de e-mail das duas pessoas com quem trabalha na empresa parceira, selecione **Visualizador – Ver Apenas** e clique em **Enviar**.<br /><br />Quando os e-mails são recebidos na empresa parceira, apenas os destinatários no e-mail podem ver a folha de cálculo e não podem guardar, editar, imprimir ou reencaminhá-la.<br /><br />Passo a passo: [Proteger um ficheiro que partilha por e-mail ao utilizar a aplicação de partilha Rights Management](sharing-app-protect-by-email.md).|
|**… enviar em segurança um documento por e-mail para uma pessoa que utiliza um dispositivo iOS**<br /><br />Pretende enviar por e-mail um documento do Word altamente confidencial a uma colega que sabe que verifica regularmente o e-mail no dispositivo iOS.|Utilize o Explorador de Ficheiros, clique com o botão direito do rato no ficheiro e selecione **Partilhar Protegido** para enviar o ficheiro como um anexo à sua colega.<br /><br />A destinatária recebe o e-mail no dispositivo iOS. Uma vez que ela não tem o Office para iPad e iPhone, clica na ligação do e-mail que lhe indica como transferir a aplicação de partilha, instala a versão para dispositivos iOS e, em seguida, visualiza o documento¹.<br /><br />Passo a passo: [Proteger um ficheiro que partilha por e-mail ao utilizar a aplicação de partilha Rights Management](sharing-app-protect-by-email.md).|
|**… verificar quem abriu os meus documentos protegidos e quando o fez, bem como revogar o acesso, se necessário**<br /><br />Partilhou de forma segura um documento de design confidencial com potenciais fornecedores e agora pretende ver quem acedeu ao mesmo, quando o fez e a partir de onde. Mais tarde, quando um dos fornecedores ganhar o contrato, pretende revogar o acesso ao documento original para que as pessoas com quem o partilhou já não o possam ler.|Depois de partilhar um documento por e-mail, aceda ao [site de controlo de documentos](http://go.microsoft.com/fwlink/?LinkId=529562) para verificar quem acedeu a esse documento e quando o fez. Quando precisar de deixar de o partilhar, selecione a opção para revogar o acesso.<br /><br />Passo a passo: [Controlar e revogar os documentos quando utiliza a aplicação de partilha RMS](sharing-app-track-revoke.md).|
|**… ler um anexo que recebi numa mensagem de e-mail com um anexo de ficheiro partilhado de forma segura, mas que não consigo ler porque a minha empresa não utiliza o Rights Management**<br /><br />O remetente do e-mail é uma pessoa em quem confia porque fez negócios com ele anteriormente e suspeita que este está a enviar-lhe informações sobre uma potencial nova oportunidade de negócio.|Siga as instruções do e-mail e clique na ligação para se inscrever no Microsoft Rights Management. A Microsoft confirma que a sua organização não tem uma subscrição que inclui o Azure Rights Management, envia-lhe uma mensagem de e-mail para concluir o processo de inscrição gratuito e, em seguida, deverá iniciar sessão com a sua nova conta. Clique na segunda ligação do e-mail para instalar a aplicação de partilha Rights Management e, em seguida, pode abrir o anexo do e-mail para ler mais sobre a nova oportunidade de negócio.<br /><br />Passo a passo: [Ver e utilizar ficheiros que foram protegidos pelo Rights Management](sharing-app-view-use-files.md).|
|**… proteger ficheiros confidenciais da empresa no meu portátil, para que pessoas exteriores à minha empresa não possam aceder aos mesmos**<br /><br />Viaja muito e utiliza o portátil para aceder e atualizar ficheiros numa pasta que tem de estar protegida contra acesso não autorizado.|Tem a aplicação de partilha RMS instalada no seu portátil. Utilize o Explorador de Ficheiros para proteger os ficheiros através da utilização de um modelo, o que protege rapidamente os ficheiros. Se o portátil for roubado, pode ficar tranquilo, uma vez que ninguém fora da sua empresa pode aceder a esses documentos.<br /><br />Passo a passo: [Proteger um ficheiro num dispositivo &#40;proteger no local&#41; ao utilizar a aplicação de partilha Rights Management](sharing-app-protect-in-place.md).|
¹ Composição de PDF com tecnologia da Foxit. Copyright © 2003–2014 por Foxit Corporation.

## O que pretende fazer?
> [!NOTE]
> Para obter mais informações técnicas, tais como os tipos de ficheiro suportados e como instalar esta aplicação numa rede empresarial, consulte o [Guia do administrador da aplicação de partilha Rights Management](sharing-app-admin-guide.md).

-   [Transferir e instalar a aplicação de partilha](install-sharing-app.md)

-   [Proteger um ficheiro num dispositivo (proteger no local)](sharing-app-protect-in-place.md)

-   [Proteger um ficheiro que partilha por e-mail](sharing-app-protect-by-email.md)

-   [Controlar e revogar os documentos](sharing-app-track-revoke.md)

-   [Ver e utilizar ficheiros que foram protegidos](sharing-app-view-use-files.md)

-   [Remover a proteção de um ficheiro](sharing-app-remove-protection.md)

-   [Utilizar atalhos de teclado](sharing-app-keyboard-shortcuts.md)

-   [Especificar definições na caixa de diálogo](sharing-app-dialog-box.md)





<!--HONumber=Apr16_HO4-->


