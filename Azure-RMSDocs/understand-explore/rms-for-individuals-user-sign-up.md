---
title: "Como os usuários se inscrevem no RMS para pessoas físicas | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 19252180802c69d6e5d6bf22c71ff3bcba96fb36


---

# Como os usuários se inscrevem no RMS para pessoas físicas

*Aplica-se a: Azure Rights Management*

Solicite o registro para esta conta gratuita visitando a [página do Microsoft Rights Management](https://portal.aadrm.com/) e forneça seu endereço de email do trabalho ou escola. 

A maneira mais comum para ser direcionado para a página de inscrição é receber uma mensagem de email com um anexo protegido que contenha instruções de como se inscrever. Você receberá um email em resposta da Microsoft e, em seguida, poderá concluir o processo de inscrição digitando os detalhes para criar sua conta. Quando você receber um email de confirmação da Microsoft, esta mensagem final enviará o usuário para uma página na qual é possível baixar o aplicativo de compartilhamento para diferentes dispositivos e um link para o guia do usuário.

## Para se inscrever no RMS para pessoas físicas

1.  Usando um computador Windows ou Mac, vá para a [página do Microsoft Rights Management](https://portal.aadrm.com).

2.  Digite o endereço de email que você usa para sua organização, como **janetm@contoso.com** ou **p.dover@fabrikam.com**.

    > [!IMPORTANT]
    > Não há suporte para contas de email pessoal, por isso não insira uma conta da Microsoft (antes conhecida como conta da Microsoft Live ID) ou outra conta pessoal que você use em casa do seu provedor de Internet.

3.  Clique em **Introdução**.

    A Microsoft usa seu endereço de email para verificar se sua organização já tem uma [assinatura paga que inclua o Azure RMS](../get-started/requirements-subscriptions.md). Se esse for o caso, você não precisará do RMS para pessoas físicas, por isso, você será conectado imediatamente e a assinatura de autoatendimento para o RMS para pessoas físicas será cancelada. Se uma assinatura paga do Azure RMS não for encontrada, você continuará para a próxima etapa.

4.  Aguarde uma mensagem de confirmação por email que será enviada para o endereço fornecido. Esta mensagem será da Microsoft (DoNotReply@microsoft.com) e tem como assunto **Microsoft RMS**.

5.  Ao receber o email, clique no link das instruções para concluir o processo de inscrição.

6.  O link leva você uma nova página do **Microsoft Rights Management** para fornecer detalhes da sua conta. Digite seu nome, seu sobrenome, introduza e confirme uma senha de sua escolha, selecione seu país/região (ou o país/região mais próximo, caso seu país/região não esteja na lista suspensa) e, em seguida, clique em **Criar**.

7.  Espere por outra mensagem de email da Microsoft agora confirmando que a sua conta está pronta para ser usada.

8.  Quando você receber o email, clique no link para entrar e ler as instruções para baixar e instalar o aplicativo de compartilhamento ou clique no link Ajuda para ler o guia do usuário do aplicativo de compartilhamento.

Agora que a sua conta foi criada, você pode começar a proteger arquivos e ler arquivos que outras pessoas protegeram. Ao ser solicitado a entrar para proteger ou ler arquivos protegidos, digite o endereço de email e a senha usados para criar a conta no RMS para indivíduos.

## Visão geral técnica do processo de inscrição
O RMS para pessoas físicas usa um processo de inscrição de autoatendimento que também é usado por outros serviços que usam tecnologia baseada em nuvem da Microsoft para autenticar usuários.

Isso é o que acontece em segundo plano quando um usuário se inscreve para o RMS para indivíduos e sua organização não tiver uma assinatura do Office 365 ou assinatura do Azure e, portanto, nenhum diretório no Azure para autenticar os usuários:

1.  Quando o primeiro usuário de uma organização solicita uma assinatura do RMS para pessoas físicas, o nome de domínio fornecido em seu endereço de email é verificado para ver se ele já está associado a um locatário do Azure. Se não houver nenhum locatário existente, um novo locatário e o diretório do Azure são criados automaticamente para a organização, que contém uma conta para este primeiro usuário. Ao contrário de uma assinatura paga do Azure, essa primeira conta não é um administrador global, mas um usuário padrão. A nova conta usa o endereço de email e senha que o usuário forneceu.

    > [!NOTE]
    > Alguns nomes de domínio não podem ser usados para criar o diretório e, portanto, não podem ser usados para o RMS para indivíduos. A lista de nomes de domínios bloqueados pode ser visualizada neste arquivo do JavaScript Object Notation: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Se for encontrado um locatário existente, será verificado se ele já possui uma assinatura do Azure RMS. Quando nenhuma assinatura é encontrada, a assinatura gratuita do RMS para pessoas físicas pode ser adicionada.

2.  A organização recebe a assinatura do RMS para pessoas físicas. Agora, esse usuário poderá ser autenticado pelo Azure e poderá proteger e ler arquivos protegidos por outras pessoas usando o Azure Rights Management. Para proteger e ler arquivos protegidos, o usuário deve ter um aplicativo habilitado para RMS, como o [aplicativo de compartilhamento Rights Management](../rms-client/sharing-app-windows.md) gratuito.

3.  Quando o segundo usuário da mesma organização solicita uma assinatura do RMS para indivíduos, uma nova conta de usuário é adicionada ao diretório do Azure criado anteriormente, usando a assinatura do RMS para indivíduos da organização. Este segundo usuário pode fazer tudo o que o primeiro usuário podia fazer (proteger arquivos e ler arquivos protegidos), mas esses dois usuários agora também podem colaborar com segurança e mais facilmente, porque eles podem aplicar rapidamente modelos padrão a arquivos que restringem o acesso a contas no diretório do Azure da organização.

4.  Os usuários subsequentes da mesma organização seguem o mesmo padrão, adicionando contas de usuário (quando novos usuários se inscreverem) ao diretório Azure da organização. Quanto mais contas forem adicionadas ao diretório, mais os usuários podem colaborar de forma segura com os colegas e parceiros, e fica mais fácil evitar que pessoas não autorizadas leiam seus arquivos quando nem deveriam acessá-los.

Durante todo este processo, não há custos para a organização e nenhum trabalho é exigido do departamento de TI. No entanto, o departamento de TI pode optar por uma das seguintes opções:

-   **Gerenciar as contas e o processo de inscrição**: os administradores de TI podem assumir a propriedade do diretório e contas criados automaticamente no Azure. Eles podem gerenciar as contas através da implementação de soluções de integração de diretório, como a sincronização de senhas e logon único. Ou eles podem impedir que os usuários criem contas ou se inscrevam no RMS para pessoas físicas.

    Para obter mais informações, consulte [Como os administradores podem controlar as contas criadas para o RMS para pessoas físicas](rms-for-individuals-take-control.md).

-   **Gerenciar o Rights Management**: os administradores de TI podem converter a assinatura do RMS para indivíduos da organização para uma assinatura paga que inclui o Azure Rights Management. Ao fazer isso, o diretório do Azure e as contas existentes serão preservados para proporcionar uma transição suave para os usuários existentes que estavam usando o RMS para indivíduos. Todos os arquivos protegidos anteriormente ainda serão protegidos com as mesmas políticas e as pessoas a quem concederam permissões para usar os arquivos ainda poderão usar os arquivos da mesma forma.

    Quando você faz isso, sua organização se beneficia da capacidade de integrar o Rights Management em seus fluxos de trabalho, serviços e armazenamento de dados. Além disso, agora você pode gerenciar o Rights Management, porque você tem controle sobre a chave do locatário da organização para o Azure Rights Management. Agora você pode fazer o seguinte:

    -   Configure o Exchange e o SharePoint para dar suporte ao Azure Rights Management, ainda que eles estejam em execução local. O Exchange e o SharePoint têm suporte nativo para os serviços online e são suportados por um conector para os servidores locais. Para obter mais informações, consulte o seguinte:

        -   As seções do Exchange Online e o SharePoint Online do [Office 365: configuração para clientes e serviços online](../deploy-use/configure-office365.md)

        -   [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md)

    -   Execute o e-discovery em dados de propriedade da empresa para que, se necessário, você possa descriptografar arquivos que foram protegidos com o Rights Management. Para mais informações, consulte [Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou a recuperação de dados](../deploy-use/configure-super-users.md).

    -   Registre todas as atividades no Rights Management como é feito na sua organização. Isso é muito eficiente, porque não só é possível monitorar quais arquivos estão sendo protegidos e quem os está acessando com sucesso, mas você também pode identificar comportamentos potencialmente suspeitos de pessoas não autorizadas que estão tentando acessar os arquivos protegidos. Para obter mais informações, consulte [Registrando em log e analisando o uso do Azure Rights Management](../deploy-use/log-analyze-usage.md).

    -   Forneça aos usuários a capacidade de rastrear e revogar seus documentos protegidos, se esses recursos forem compatíveis com a sua [assinatura do Azure RMS](https://technet.microsoft.com/dn858608). Para obter mais informações, consulte [Rastrear e revogar seus arquivos](../rms-client/sharing-app-track-revoke.md) no [guia de usuário do aplicativo RMS sharing](../rms-client/sharing-app-user-guide.md).

    -   Implemente a solução BYOK (Bring Your Own Key ou Traga Sua Própria Chave) para que sua chave de locatário para o Azure Rights Management seja gerada no local, de acordo com suas políticas de TI, e transferida com segurança para a Microsoft usando um Hardware Security Module (HSM). Para mais informações, consulte o [Planejamento e implementação de sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).


## Próximas etapas
Consulte [Como os administradores podem controlar as contas criadas para o RMS para pessoas físicas](rms-for-individuals-take-control.md).





<!--HONumber=Jun16_HO4-->


