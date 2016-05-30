---
# required metadata

title: Opções de caixa de diálogo para o aplicativo de compartilhamento Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Opções da caixa de diálogo do aplicativo de compartilhamento do Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Use essas informações para ajudá-lo a especificar as opções na caixa de diálogo **Adicionar proteção** ou na caixa de diálogo **Compartilhamento protegido** do aplicativo RMS sharing. Você verá essa caixa de diálogo ao [proteger um arquivo para compartilhamento](sharing-app-protect-by-email.md) ou ao [proteger um arquivo no local](sharing-app-protect-in-place.md) e deverá escolher permissões personalizadas.

> [!IMPORTANT]
> Se as opções exibidas forem diferentes das documentadas aqui, você provavelmente não terá a versão mais recente do aplicativo de compartilhamento instalada. Você pode baixar a versão mais recente na página do [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) .
> 
> Como saber se você tem a versão mais recente? Procure **aplicativo de compartilhamento Microsoft Rights Management** listado em Programas e Recursos e verifique o número de versão correspondente. Para ver e usar as opções na tabela, a versão deve ser pelo menos **1.0.1770.0**. Você pode verificar o número da versão mais recente na página de download.

Além das opções que você pode escolher, você deve também estar se perguntando:

-   [O que é o arquivo .ppdf, criado automaticamente?](#what-s-the-ppdf-file-that-s-automatically-created-)

-   [Qual é a diferença entre proteção genérica e proteção interna (nativa)?](#what-s-the-difference-between-generic-protection-and-built-in-native-protection-)

|Opção|Descrição|
|----------|---------------|
|**USUÁRIOS**|Se você ainda não tiver especificado um endereço de email do Outlook, digite os endereços de email das pessoas que você deseja ser capaz de abrir o arquivo.<br /><br />Observe que o aplicativo RMS sharing não dá suporte a todos os endereços de email.<br /><br />Se sua organização usa a versão local do Rights Management (AD RMS), os endereços de email que você pode especificar são restritos a pessoas da sua organização. Quando isso se aplicar e você tentar especificar endereços de email externos, você verá uma mensagem que diz que a configuração da sua empresa permite o compartilhamento de conteúdo protegido apenas dentro da empresa. <br /><br /> Se sua organização usa o Azure RMS, esses endereços de email especificados por você poderão ser para pessoas da sua ou de outra organização.<br /><br />Por exemplo: **janetm@contoso.com; p.dover@fabrikam.com**<br /><br />Endereços de email pessoais não têm suporte atualmente pelo aplicativo RMS sharing.|
|**Proteção genérica**|Se essa opção for selecionada, isso significa que o arquivo selecionado não pode ser protegido nativamente. Para obter mais informações, consulte. [Qual é a diferença entre proteção genérica e proteção interna (nativa)?](#what-s-the-difference-between-generic-protection-and-built-in-native-protection-) nesta página.|
|**Visualizador – Somente exibição**<br /><br />**Revisor – Exibir e editar**<br /><br />**Coautor – Exibir, editar, copiar e imprimir**<br /><br />**Coproprietário – Todas as permissões**<br /><br />Observação: todas essas opções têm um ícone redondo antes do nome que representa um globo. Esse ícone é usado porque, normalmente, você seleciona uma dessas opções ao enviar o anexo para alguém em uma organização diferente.|Selecione uma das seguintes opções para definir os direitos para o documento protegido. Clique em cada opção para exibir uma descrição.<br /><br />Quando você escolhe uma dessas opções, somente as pessoas que você especificar em **USUÁRIOS** possuem os direitos que você especificou para abrir e usar o documento. Por exemplo, se eles encaminharem para outra pessoa, o documento não abrirá.|
|Modelos de política que o administrador configura.<br /><br />Por exemplo, se o nome da sua organização é “Contoso, Ltd”, você deverá encontrar **Contoso, Ltd - Somente Exibição Confidencial**<br /><br />Observação: todas essas opções têm um ícone quadrado antes do nome que representa um edifício de escritórios. Esse ícone é usado porque, normalmente, você seleciona uma dessas opções ao enviar o anexo para alguém na sua organização.|Quando você compartilha um documento com pessoas que trabalham para sua organização, você verá os modelos de política disponíveis que o administrador configurar. Escolha uma destas opções se o documento não puder ser compartilhado fora da sua organização.<br /><br />Quando você escolhe uma dessas opções, o administrador define os direitos para o documento e quem pode abri-lo.|
|**Expirar esses documentos em**|Selecione esta opção apenas para arquivos com detecção de hora que os usuários que você selecionou não devem conseguir abrir depois de uma data especificada. Você ainda poderá abrir o arquivo original, mas após a meia-noite (seu fuso horário atual), no dia em que você especificar, mas outras pessoas não poderão abrir o arquivo.<br /><br />Essa opção não estará disponível se você selecionar um modelo de política que o administrador configurar.|
|**Envie um email para mim quando alguém tentar abrir esses documentos**|Observação: essa opção está atualmente em preview.<br /><br />Selecione esta opção se você deseja receber notificações por email sempre que alguém tentar abrir o documento que você está protegendo. A mensagem de email dirá quem tentou abri-lo, quando e se foi bem-sucedido.<br /><br />Essa opção está disponível apenas se a sua organização usar o Azure RMS. Se sua organização usa a versão local do Rights Management (AD RMS), você não verá essa opção.|
|**Permitir que eu revogue instantaneamente o acesso a esses documentos**|Escolha esta opção se você precisar revogar o acesso aos documentos posteriormente usando o site de rastreamento de documentos e se a revogação precisar entrar em vigor imediatamente. No entanto, a configuração desta opção significa que, enquanto o documento não for revogado, os usuários sempre precisarão de uma conexão à Internet para ler o documento todas as vezes que o acessarem. Pode haver alguns cenários em que os usuários não conseguem conectar seu dispositivo à Internet e, por isso, não poderão ler o seu documento conforme pretendido.<br /><br />Se você não escolher essa opção, você ainda pode revogar os documentos mais tarde usando o site de rastreamento de documentos. No entanto, devido ao fato de os usuários não precisarem sempre de uma conexão à Internet para ler o documento, eles não saberão imediatamente que o documento foi revogado e poderão continuar a ler até que eles se autentiquem novamente no Azure RMS. Por padrão, o número máximo de dias em que alguém pode continuar a ler um documento protegido que foi revogado é de 30 dias, mas um administrador pode alterar este número para um período maior ou menor que 30 dias.<br /><br />Essa opção está disponível apenas se a sua organização usar o Azure RMS. Se sua organização usa a versão local do Rights Management (AD RMS), você não verá essa opção.|

## Qual é a diferença entre proteção genérica e proteção interna (nativa)?

-   Se você **proteger um arquivo genericamente**, pessoas não autorizadas não poderão abrir o arquivo. Mas depois de pessoas autorizadas abrirem o arquivo, elas podem, em seguida, encaminhá-lo desprotegido para outras pessoas ou salvá-lo em um local que outras pessoas possam acessar. No entanto, elas verão uma mensagem informando quais as permissões que possuem para o arquivo e é solicitado que as aceitem, mas esta proteção não pode ser imposta. Além disso, quando você protege genericamente um arquivo, é possível restringir as permissões mais do que a autorização. Por exemplo, não é possível restringir o conteúdo para somente exibição ou não imprimir.

    > [!NOTE]
    > Um arquivo protegido genericamente sempre tem uma extensão de nome de arquivo **.pfile**.

-   Em comparação, quando você usa a **proteção interna (nativa)** do Rights Management com aplicativos que dão suporte a isso (por exemplo, arquivos do Office), a proteção se aplica ao arquivo mesmo que o arquivo seja enviado para outra pessoa ou salvo em outro local. E, ao proteger esses arquivos, você pode usar permissões restritivas, como somente leitura, ou a permissão para editar, mas não imprimir ou copiar. Por exemplo, você poderá selecionar **Visualizador – somente exibição**de modo que o conteúdo não possa ser editado, impresso ou copiado.

Para obter informações técnicas adicionais, consulte a seção [Níveis de proteção – nativa e genérica](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) no [Guia de administrador do aplicativo de compartilhamento Rights Management](sharing-app-admin-guide.md).

## O que é o arquivo .ppdf, criado automaticamente?

-   Quando você compartilha um arquivo protegido por email (compartilhamento protegido), o aplicativo RMS sharing cria automaticamente uma versão **.ppdf** do arquivo para Word, Excel, PowerPoint ou PDF. Esta é uma versão protegida de somente leitura do arquivo que somente pessoas autorizadas podem abrir e garante que os destinatários possam sempre ler o anexo, mesmo se estiverem usando um dispositivo móvel que não tenha um aplicativo nativamente compatível com o Rights Management. Desde que essas pessoas tenham o aplicativo RMS sharing instalado, elas poderão ler o anexo.

    Neste cenário, ao contrário de um arquivo protegido genericamente, a restrição de uso é imposta. O destinatário não poderá salvar esta versão do arquivo e, se encaminharem o anexo para outra pessoa, as restrições originais permanecerão com o documento. Somente as pessoas que foram autorizadas para o documento protegido poderão abri-lo.

    > [!NOTE]
    > Um arquivo .ppdf é criado automaticamente ao compartilhá-lo protegido (compartilhamento por email), mas não é criado ao proteger no local.

## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)



<!--HONumber=May16_HO2-->


