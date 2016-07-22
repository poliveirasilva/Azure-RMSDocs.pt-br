---
title: "Opções da caixa de diálogo para a aplicação de partilha Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c611fa8a846612fed238e59e5077be67f6f9531a
ms.openlocfilehash: 771a80843ca5ab01cd06bd4e76c827469b0e9f00


---

# Opções da caixa de diálogo para a aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Utilize estas informações para ajudar a especificar as opções na caixa de diálogo **adicionar proteção** da aplicação de partilha RMS ou na caixa de diálogo **partilhar protegido**. Irá ver esta caixa de diálogo quando [proteger um ficheiro para partilhar](sharing-app-protect-by-email.md) ou [proteger um ficheiro no local](sharing-app-protect-in-place.md) e escolher permissões personalizadas.

> [!IMPORTANT]
> Se as opções apresentadas forem diferentes das documentadas aqui, provavelmente não tem a versão mais recente da aplicação de partilha instalada. Pode transferir a versão mais recente a partir da página do [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970).
> 
> Como pode saber se tem a versão mais recente? Procure a **aplicação de partilha Microsoft Rights Management** na lista de Programas e Funcionalidades e verifique o número da versão correspondente. Para ver e utilizar as opções da tabela, a versão deve ser, pelo menos, **1.0.1770.0**. Pode verificar o número da versão mais recente na página de transferência.

Além das opções que pode escolher, poderá também estar a perguntar-se:

-   [O que é o ficheiro .ppdf criado automaticamente?](#what-s-the-ppdf-file-that-s-automatically-created-)

-   [Qual é a diferença entre proteção genérica e proteção incorporada (nativa)?](#what-s-the-difference-between-generic-protection-and-built-in-native-protection-)

|Opção|Descrição|
|----------|---------------|
|**UTILIZADORES**|Se ainda não tiver especificado um endereço de e-mail no Outlook, escreva os endereços de e-mail das pessoas que pretende que consigam abrir o ficheiro.<br /><br />Tenha em atenção que a aplicação de partilha RMS não suporta todos os endereços de e-mail.<br /><br />Se a sua organização utilizar a versão no local do Rights Management (AD RMS), os endereços de e-mail que pode especificar estão limitados às pessoas da sua organização. Quando isto se aplicar e tentar especificar endereços de e-mail externos, verá uma mensagem a indicar que a configuração da empresa permite a partilha de conteúdo protegido apenas dentro da empresa. <br /><br /> Se a sua organização utilizar o Azure RMS, os endereços de e-mail que especificar podem ser de pessoas da sua organização ou de pessoas noutra organização.<br /><br />Por exemplo: **juliam@contoso.com; p.barbosa@fabrikam.com**<br /><br />Atualmente, a aplicação de partilha RMS não suporta endereços de e-mail pessoais.|
|**Proteção genérica**|Se esta opção estiver selecionada, significa que o ficheiro que selecionou não pode ser protegido nativamente. Para obter mais informações, consulte: [Qual é a diferença entre proteção genérica e proteção incorporada (nativa)?](#what-s-the-difference-between-generic-protection-and-built-in-native-protection-) nesta página.|
|**Visualizador – Ver Apenas**<br /><br />**Revisor – Ver e Editar**<br /><br />**Coautor – Ver, Editar, Copiar e Imprimir**<br /><br />**Coproprietário – Todas as Permissões**<br /><br />Nota: todas estas opções têm um ícone redondo antes do nome, que representa um globo do mundo. Este ícone é utilizado porque, normalmente, seleciona uma destas opções quando envia o anexo para alguém numa organização diferente.|Selecione uma destas opções se pretender definir os direitos para o seu documento protegido. Clique em cada uma das opções para ver uma descrição.<br /><br />Quando escolhe uma destas opções, apenas as pessoas que especifica em **UTILIZADORES** têm os direitos especificados por si para abrir e utilizar o documento. Por exemplo, se reencaminharem o documento para outra pessoa, este não abre.|
|Modelos de política que o administrador configura.<br /><br />Por exemplo, se o nome da sua empresa for Contoso, Lda.: **Contoso, Lda. – Apenas Visualização Confidencial**<br /><br />Nota: todas estas opções têm um ícone quadrado antes do nome, que representa um edifício de escritórios. Este ícone é utilizado porque, normalmente, seleciona uma destas opções quando envia o anexo para alguém na sua organização.|Quando partilha um documento com pessoas que trabalham na sua organização, são apresentados os modelos de política disponíveis que o seu administrador configura. Escolha um deles quando o documento não deve ser partilhado fora da sua organização.<br /><br />Ao escolher uma destas opções, o administrador define os direitos para o documento e quem o pode abrir.|
|**Expirar estes documentos em**|Selecione esta opção apenas para ficheiros sensíveis ao tempo que os utilizadores que selecionou não devem poder abrir após uma data especificada por si. Ainda poderá abrir o ficheiro original, mas, após a meia-noite (o seu fuso horário atual), no dia em que especificou, as outras pessoas não poderão abrir o ficheiro.<br /><br />Esta opção não está disponível se selecionar um modelo de política que o seu administrador configura.|
|**Enviar-me um e-mail quando alguém tentar abrir estes documentos**|Nota: esta opção está atualmente em pré-visualização.<br /><br />Selecione esta opção se pretender receber notificações por e-mail sempre que alguém tentar abrir o documento que está a proteger. A mensagem de e-mail indicará quem o tentou abrir, quando o fez e se teve êxito.<br /><br />Esta opção está disponível apenas se a sua organização utilizar o Azure RMS. Se a sua organização utilizar a versão no local do Rights Management (AD RMS), não verá esta opção.|
|**Permitir a revogação instantânea do acesso a estes documentos**|Escolha esta opção se precisar de revogar o acesso aos documentos mais tarde através do site de controlo de documentos e se a revogação tiver de ter efeito imediatamente. No entanto, se definir esta opção, enquanto o documento não for revogado, os utilizadores precisarão sempre de uma ligação à Internet para ler o documento, cada vez que acederem ao mesmo. Poderão existir alguns cenários em que os utilizadores não conseguem ligar o dispositivo à Internet, pelo que não poderão ler o documento conforme pretendido.<br /><br />Se não escolher esta opção, pode revogar os documentos mais tarde, ao utilizar o site de controlo de documentos. No entanto, uma vez que os utilizadores não precisam sempre de uma ligação à Internet para ler o documento, não sabem de imediato que o documento foi revogado e podem continuar a lê-lo até efetuarem novamente a autenticação com o Azure RMS. Por predefinição, o número máximo de dias durante os quais alguém pode continuar a ler um documento protegido que revogou é 30 dias, mas um administrador pode alterar este valor para ser inferior ou superior a 30 dias.<br /><br />Esta opção está disponível apenas se a sua organização utilizar o Azure RMS. Se a sua organização utilizar a versão no local do Rights Management (AD RMS), não verá esta opção.|

## Qual é a diferença entre proteção genérica e proteção incorporada (nativa)?

-   Quando **protege um ficheiro genericamente**, as pessoas não autorizadas não podem abrir esse ficheiro. Porém, depois de as pessoas autorizadas abrirem o ficheiro, podem reencaminhá-lo desprotegido para outras pessoas ou guardá-lo numa localização à qual têm acesso outros utilizadores. No entanto, veem uma mensagem que indica as permissões que têm para o ficheiro e é-lhes pedido que as respeitem, mas esta proteção não pode ser imposta. Além disso, quando protege genericamente um ficheiro, não pode restringir as permissões além da autorização. Por exemplo, não pode restringir o conteúdo para ver apenas ou não imprimir.

    > [!NOTE]
    > Um ficheiro protegido genericamente tem sem+re a extensão de nome de ficheiro **.pfile**.

-   Em comparação, quando utiliza a **proteção incorporada (nativa)** do Rights Management com aplicações que suportam este tipo de proteção (por exemplo, ficheiros do Office), a proteção é aplicada ao ficheiro mesmo se este for enviado para outra pessoa ou guardado noutra localização. Além disso, ao proteger estes ficheiros, pode utilizar permissões restritivas como só de leitura, ou a permissão para editar, mas não para imprimir ou copiar. Por exemplo, pode selecionar **Visualizador – Ver Apenas**, para que não seja possível editar, imprimir ou copiar o conteúdo.

Para obter informações técnicas adicionais, consulte a secção [Níveis de proteção – nativa e genérica](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) no [Guia do administrador da aplicação de partilha Rights Management](sharing-app-admin-guide.md).

## O que é o ficheiro .ppdf criado automaticamente?

-   Quando partilha um ficheiro protegido por e-mail (partilhar protegido), a aplicação de partilha RMS cria automaticamente uma versão **.ppdf** do ficheiro para Word, Excel, PowerPoint ou PDF. Esta é uma versão protegida só de leitura do ficheiro que apenas as pessoas autorizadas podem abrir e assegura que os destinatários podem sempre ler o anexo, mesmo se estiverem a utilizar um dispositivo móvel que não tem uma aplicação que suporta nativamente o Rights Management. Desde que estas pessoas tenham a aplicação de partilha RMS instalada, poderão ler o anexo.

    Neste cenário, ao contrário de um ficheiro protegido genericamente, é imposta a restrição de utilização. O destinatário não conseguirá guardar esta versão do ficheiro e, se reencaminhar o anexo para outra pessoa, as restrições originais permanecem no documento. Apenas as pessoas com autorização para o documento protegido poderão abri-lo.

    > [!NOTE]
    > Um ficheiro .ppdf é criado automaticamente quando utiliza a opção partilhar protegido (partilhar por e-mail), mas não é criado quando utiliza a opção proteger no local.

## Exemplos e outras instruções
Para obter exemplos de como pode utilizar a aplicação de partilha Rights Management e instruções sobre como proceder, veja as secções seguintes do guia do utilizador da aplicação de partilha Rights Management:

-   [Exemplos de utilização da aplicação de partilha RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que pretende fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte Também
[Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md)




<!--HONumber=Jun16_HO4-->


