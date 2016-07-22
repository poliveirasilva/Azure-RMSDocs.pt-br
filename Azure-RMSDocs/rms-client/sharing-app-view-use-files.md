---
title: Ver e utilizar ficheiros que foram protegidos pelo Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: c243ad02bdbd5bd46ba1b2a4818839df8a7deb7b


---

# Ver e utilizar ficheiros que foram protegidos pelo Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Quando a [Aplicação de partilha Rights Management (RMS) está instalada no computador](install-sharing-app.md), basta fazer duplo clique num ficheiro protegido para o ver. O ficheiro pode ser um anexo numa mensagem de e-mail ou poderá vê-lo ao utilizar o Explorador de Ficheiros.

> [!NOTE]
> Antes de poder ver o ficheiro protegido, o RMS tem de confirmar que está autorizado a fazê-lo. Para tal, verifica o seu nome de utilizador e palavra-passe. Em alguns casos, estas informações podem estar em cache e não lhe são pedidas as suas credenciais. Noutros casos, ser-lhe-á pedido que forneça as credenciais.
>
> Se a sua organização não utilizar o Azure Rights Management (Azure RMS) nem o AD RMS, pode candidatar-se a uma conta gratuita que aceitará as suas credenciais para que possa abrir ficheiros que estão protegidos pelo RMS:
>
> -   Para se candidatar a esta conta, clique na ligação para aderir ao [RMS para indivíduos](http://go.microsoft.com/fwlink/?LinkId=309469)
>
>     Quando se inscrever, utilize o seu endereço de e-mail da empresa em vez de um endereço de e-mail pessoal. Caso se esteja a inscrever porque recebeu um anexo protegido, utilize o mesmo endereço de e-mail que foi utilizado para lhe enviar a mensagem de e-mail.
> -   Para mais informações, veja [RMS para indivíduos e Azure Rights Management](../understand-explore/rms-for-individuals.md)

## Para ver um ficheiro protegido
Ao utilizar o Explorador de Ficheiros ou a mensagem de e-mail que contém o anexo, faça duplo clique no ficheiro protegido e introduza as suas credenciais, se lhe for pedido.

Se vir duas versões do ficheiro, mas com extensões de nome de ficheiro diferentes, abra o ficheiro com a extensão de ficheiro .ppdf apenas se o outro ficheiro não abrir. Se também não conseguir abrir a versão .ppdf, instale primeiro a [Aplicação de partilha RMS](install-sharing-app.md), que sabe como abrir ficheiros com uma extensão de nome de ficheiro .ppdf.

> [!NOTE]
> Para obter mais informações, veja “[O que é o ficheiro .ppdf criado automaticamente?](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)”.

O modo como o ficheiro abre depende da forma como foi protegido, o que pode descobrir ao observar a extensão de nome de ficheiro. Em qualquer um dos casos, a abertura do ficheiro pode estar sujeita a auditoria e permanece auditada enquanto este estiver protegido. Além disso, se o ficheiro tiver sido enviado como um anexo de e-mail, o remetente poderá ser notificado por e-mail sempre que abrir o ficheiro.

- **O ficheiro tem uma extensão de nome de ficheiro *.pfile***

    O ficheiro foi protegido genericamente.

    Quando abre o ficheiro, é apresentada uma caixa de diálogo **ficheiro protegido** da aplicação de partilha que indica quem protegeu o ficheiro e que é esperado que respeite as permissões de coproprietário. Clique em **Abrir** para ler o ficheiro.

    ![Caixa de diálogo para um ficheiro .pfile partilhado por e-mail ao utilizar a aplicação de partilha RMS](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **O ficheiro tem uma extensão de nome de ficheiro *.ppdf* ou é um ficheiro de texto ou de imagem protegido (tal como *.ptxt* ou *.pjpg*

    O ficheiro foi protegido nativamente como uma cópia só de leitura.

    Para abrir o ficheiro, é utilizado o visualizador instalado juntamente com a aplicação de partilha RMS. Este ficheiro é só de leitura, mesmo que o guarde noutra localização ou mude o seu nome.

- **Outras extensões de nome de ficheiro**

    O ficheiro foi protegido nativamente.

    Para abrir o ficheiro, é utilizada a aplicação associada à extensão de nome de ficheiro original e é apresentada uma faixa de restrição na parte superior do ficheiro. A faixa pode apresentar as permissões que estão aplicadas ao ficheiro ou pode disponibilizar uma ligação para as mostrar. Por exemplo, poderá ver a seguinte mensagem em que tem de clicar em **A permissão encontra-se atualmente restrita** para ver as permissões reais que estão aplicadas ao ficheiro e as pessoas que podem aceder ao mesmo:

    ![Faixa de acesso restrito quando o ficheiro está protegido](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



Para obter uma lista completa das extensões de nome de ficheiro que o Rights Management suporta, veja a secção [Tipos de ficheiro suportados e extensões de nome de ficheiro](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) no [Guia do administrador da aplicação de partilha Rights Management](sharing-app-admin-guide.md). Se a sua extensão de nome de ficheiro não constar da lista, faça uma pesquisa na Web para ver se é uma extensão de nome de ficheiro suportada por outra aplicação.

> [!NOTE]
> Se, depois de confirmar que o ficheiro está protegido pelo Rights Management, o ficheiro não abrir, transfira e utilize a [Ferramenta RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Siga as instruções na ferramenta para verificar se existem problemas no seu computador que possam impedir que um documento protegido seja aberto.

## Para utilizar ficheiros que foram protegidos (por exemplo, editar e imprimir o ficheiro)
Se pretender efetuar outras ações além da leitura (por exemplo, editar, copiar e imprimir) depois de abrir o ficheiro protegido, siga as instruções de acordo com a extensão de nome de ficheiro:

- **O ficheiro tem uma extensão de nome de ficheiro *.pfile***

    Guarde o ficheiro aberto e atribua-lhe uma nova extensão de nome de ficheiro que esteja associada à aplicação que pretende utilizar.

    Por exemplo, se um ficheiro tiver sido protegido com o nome de ficheiro documento.vsdx.pfile, visualize o ficheiro e, no Explorador de Ficheiros, guarde-o como documento.vsdx.

    O novo ficheiro já não está protegido. Se pretender protegê-lo, tem de o fazer manualmente. Para obter instruções, veja [Proteger um ficheiro num dispositivo (proteger no local) ao utilizar a aplicação de partilha Rights Management](sharing-app-protect-in-place.md)

- **O ficheiro tem uma extensão de nome de ficheiro *.ppdf* ou é um ficheiro de texto ou de imagem protegido (tal como *.ptxt* ou *.pjpg*

    Só pode ver o ficheiro e, se o mover ou mudar o nome, a proteção permanece aplicada ao ficheiro.

- **Outras extensões de nome de ficheiro**

    O dispositivo tem de ter uma aplicação que suporte o Rights Management para utilizar estes ficheiros. Estas aplicações chamam-se aplicações otimizadas para o RMS. As aplicações do Office 2016, Office 2013 e Office 2010 (como o Word, Excel, PowerPoint e Outlook) são exemplos de aplicações que são otimizadas para o Rights Management. No entanto, as aplicações que não são da Microsoft, tais como as aplicações de outras empresas de software e as suas próprias aplicações de linha de negócio, também podem ser otimizadas para o Rights Management.

    As aplicações otimizadas para o Rights Management sabem como abrir ficheiros que foram protegidos por outras aplicações otimizadas para o Rights Management. Além disso, também mantêm a proteção que lhes é aplicada, mesmo que edite o ficheiro ou o guarde com outro nome de ficheiro ou noutra localização. Estas aplicações permitem-lhe utilizar o ficheiro de acordo com as permissões aplicadas atualmente ao mesmo, para que o possa utilizar se tiver permissões para o fazer. Por exemplo, poderá conseguir editar o ficheiro, mas não imprimi-lo.


## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, veja as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jun16_HO4-->


