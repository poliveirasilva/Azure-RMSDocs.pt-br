---
title: "Ajudando os usuários a proteger os arquivos usando o Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b6dcd8bb1091e9c484e02042adbf993381581a9d
ms.openlocfilehash: d48616cb638522e6cda61e7ae96db9480fc14099


---

# Ajudando os usuários a proteger os arquivos usando o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Após ter implantado e configurado o Azure Rights Managenent (RMS) para sua organização, forneça ajuda e orientação para os usuários, administradores e seu suporte técnico:

-   **Informação do usuário final:**

    Informe os usuários sobre como proteger documentos e e-mails que contenham informações confidenciais. Sempre que possível, forneça essas informações para seus fluxos de trabalho existentes para que eles possam incorporar as etapas adicionais em um processo já familiar em vez de introduzir processos completamente novos. Permita-lhes saber os benefícios (e os riscos) que são específicos do seu negócio, assim como fornecer orientação para quando eles devem proteger arquivos e e-mails. Se você configurou os [modelos personalizados](configure-custom-templates.md), forneça instruções sobre qual selecionar se o nome e a descrição do modelo não forem suficientes para eles escolherem o modelo correto.

    > [!TIP]
    > Vídeos de exemplo para os usuários finais:
    >
    > -   [Experiência do usuário do Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Rastreio e revogação de documentos no Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informações do administrador:**

    Alguns aplicativos aplicam a proteção de informações automaticamente, usando as políticas e configurações que os administradores configuram. Para estes aplicativos, talvez seja necessário fornecer instruções para outros administradores que gerenciem estes aplicativos e serviços. Para obter mais informações, consulte [Como os aplicativos dão suporte ao Azure Rights Management](../understand-explore/applications-support.md) e [Configurando aplicativos do Azure Rights Management](configure-applications.md).

-   **Informações de suporte técnico:**

    Uma das ferramentas mais úteis para o suporte técnico é o [Analisador RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Operadores de suporte técnico podem executá-lo com a opção de administrador do Azure RMS e podem solicitar aos usuários para executá-lo com a opção de usuário do Azure RMS. Essa ferramenta pode não apenas ajudar a identificar problemas, mas também corrigir os problemas que encontrar e se o problema não for resolvido, cria registos de rastreamento.

    Se houver solicitações legítimas para direitos totais de acesso a documentos protegidos, por exemplo, uma solicitação do departamento jurídico ou gerente depois que um funcionário sai da organização, verifique se o suporte técnico tem processos para solicitação usando o [recurso de superusuário](configure-super-users.md) do Azure RMS.

    Além disso, estes são alguns dos problemas típicos que os usuários podem relatar:

    -   **Ajuda de logon:**

        Os usuários poderão ser solicitados a fornecerem suas credenciais quando o Azure RMS precise autenticar um usuário e não possa usar as credenciais armazenadas em cache. Essa será a conta e senha comercial ou escolar do usuário que está associada ao seu locatário do Office 365 ou seu locatário do Active Directory do Azure. Não será uma conta da Microsoft (anteriormente a ID do Microsoft Live) ou sua conta de e-mail pessoal, porque essas atualmente não têm suporte no Azure RMS. Forneça aos usuários e ao seu suporte técnico instruções sobre que conta usar quando os usuários são solicitados a fornecer suas credenciais ao usarem esses aplicativos.

    -   **Problemas de proteção ou consumo de conteúdo:**

        Certifique-se de que os usuários tenham as instruções apropriadas para os aplicativos que eles usam e que estão usando aplicativos e dispositivos que são suportados pelo Azure RMS. Para mais informações sobre os dispositivos e aplicativos com suporte, consulte [Requisitos do Azure Rights Management](../get-started/requirements-azure-rms.md).

        Se os usuários vêem um erro ao tentar proteger ou consumir conteúdo, peça-lhes para executar o [Analisador RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437) como um usuário do Azure RMS.

        Se os usuários relatarem que podem abrir o conteúdo protegido, mas não têm os direitos necessários, peça-lhes para executar o [Analisador RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437) como um usuário do Azure RMS e baixar e verem os modelos. Isso confirmará que baixaram com êxito os modelos e quais são os direitos que os modelos fornecem. O problema pode ser que o usuário não esteja no grupo correto que está configurado para o modelo, ou que o modelo precisa ser reconfigurado para o usuário.

Use as seguintes seções para obter informações específicas ao aplicativo para ajudar os usuários a proteger documentos e e-mails confidenciais.

## Usar a proteção de informações com o aplicativo de compartilhamento Rights Management
O aplicativo de compartilhamento Rights Management (RMS) é necessário para que os usuários protejam e consumam conteúdo protegido se eles usam o Office 2010, mas também é recomendado para todos os computadores e dispositivos móveis que suportem o Azure RMS.

Além de tornar mais fácil para os usuários a proteção de documentos importantes, o aplicativo de compartilhamento do RMS permite aos usuários controlar os documentos que eles tenham protegido e, se necessário, revogar o acesso a eles.

Para obter instruções para usar esse aplicativo para computadores com Windows, consulte o [guia de usuário do aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-user-guide.md).

Para dispositivos móveis, consulte [Perguntas Frequentes para o aplicativo de compartilhamento Microsoft Rights Management para plataformas móveis](http://technet.microsoft.com/dn451248).

> [!TIP]
> Para ver um cenário de exemplo de alto nível com capturas de tela, consulte [Users safely share attachments with mobile users](../understand-explore/what-admins-users-see.md#users-safely-share-attachments-with-mobile-users) (Os usuários compartilham com segurança anexos com usuários móveis).

## Usando a proteção de informações com o Office 365, Office 2016 ou Office 2013
Se você estiver usando o Azure RMS e não tiver instalado o aplicativo de compartilhamento Rights Management, os usuários não verão o botão **Compartilhamento protegido** na faixa de opções ou **Proteção no local** no Explorador de Arquivo que lhes facilita proteger os arquivos. Para esses usuários, eles devem seguir instruções semelhantes a estas.

> [!TIP]
> Para encontrar ajuda específica do aplicativo e instruções para usar a proteção de informações com estes aplicativos, pesquise **IRM** e o nome e versão do aplicativo.

#### Para proteger um documento no Word 2013

1.  No Microsoft Word, crie um novo documento.

2.  No menu **Arquivo** , clique em **Informações**, clique em **Proteger Documento**, clique em **Restringir Acesso**, e então escolha um modelo para rapidamente aplicar os direitos de uso apropriados, ou selecione **Restringir o Acesso** e selecione os direitos de uso você mesmo.

    > [!NOTE]
    > Se esta for a primeira vez que você usou o Rights Management, você contatará o serviço do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e suas credenciais serão solicitadas para configurar o cliente do Office IRM.

3.  Salve o documento.

Quando outros abrime o documento, primeiro são autenticados. Se eles não são autorizados a abrir o documento, o documento não abre. Se eles são autorizados a abrir o documento, ele abre com os direitos de uso restritos que foram especificados para aquele usuário. Por exemplo, um direito de uso de Somente leitura não permite ao usuário editar ou salvar o documento, mesmo que primeiro seja copiado de outro local. Os direitos de uso são exibidos na parte superior do documento usando uma faixa de restrição. A faixa pode exibir as permissões que são aplicadas ao documento, ou pode fornecer um link para mostrá-las.

#### Para proteger uma mensagem de e-mail usando o Outlook 2013 e o Exchange Online

1.  No Outlook, crie uma nova mensagem de e-mail direcionada a um recipiente dentro da sua organização.

2.  Na guia **OPÇÕES** clique em **Permissões**, e então selecione uma opção. Por exemplo: **Não Encaminhar**, **&lt;Nome da Empresa&gt; - Confidencial** ou **&lt;Nome da Empresa&gt; - Somente Exibição Confidencial**.

3.  Envie a mensagem.

Da mesma forma a ver um documento protegido, quando os destinatários recebem a mensagem de e-mail, eles são autenticados primeiro. Se eles são autorizados a ver a mensagem de e-mail, ele abre com os direitos de uso restritos que foram especificados para aquele usuário. Por exemplo, se você selecionou **Não encaminhar**, o botão Encaminhar não estará disponível na faixa de opções.

#### Para proteger uma mensagem de e-mail usando o Outlook Web App

1.  No Outlook Web App, crie uma nova mensagem de e-mail direcionada a um recipiente dentro da sua organização.

2.  Clique em  **…**, clique em **definir permissões**e então selecione uma opção. **Não Encaminhar**, **Não Responder a Todos**, **&lt;Nome da Empresa&gt; - Confidencial** ou **&lt;Nome da Empresa&gt; Somente Exibição Confidencial**.

3.  Envie a mensagem.

Da mesma forma a ver um documento protegido, quando os destinatários recebem a mensagem de e-mail, eles são autenticados primeiro. Se eles são autorizados a ver a mensagem de e-mail, ele abre com os direitos de uso restritos que foram especificados para aquele usuário. Por exemplo, se você selecionou **Não Responder a Todos**, a opção **RESPONDER A TODOS** não estará disponível na janela da mensagem.





<!--HONumber=Jun16_HO4-->


