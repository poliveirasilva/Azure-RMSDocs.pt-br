---
# required metadata

title: Como os utilizadores se inscrevem no RMS para indivíduos | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Como os utilizadores se inscrevem no RMS para indivíduos

*Aplica-se a: Azure Rights Management*

Para se inscrever nesta conta gratuita, os utilizadores efetuam o pedido ao visitar a [página Microsoft Rights Management](https://portal.aadrm.com/) e fornecem o seu endereço de e-mail profissional ou escolar. 

A forma mais habitual através da qual os utilizadores serão direcionados para esta página de inscrição é se receberem uma mensagem de e-mail com um anexo protegido, que contém instruções para a inscrição. Recebem um e-mail em resposta da Microsoft e, em seguida, podem concluir o processo de inscrição, introduzindo os detalhes para criar a conta. Quando recebem uma confirmação de e-mail da Microsoft, esta última mensagem de e-mail envia-os para uma página onde podem transferir a aplicação de partilha para diferentes dispositivos e uma ligação para o guia do utilizador.

## Para se inscrever no RMS para indivíduos

1.  Num computador Windows ou Mac, aceda à [página Microsoft Rights Management](https://portal.aadrm.com).

2.  Escreva o endereço de e-mail que utiliza para a sua organização, tal como **juliam@contoso.com** ou **p.barbosa@fabrikam.com**.

    > [!IMPORTANT]
    > As contas de e-mail pessoais não são suportadas, como tal, não introduza uma conta Microsoft (anteriormente denominada uma conta Microsoft Live ID) ou outra conta pessoal que poderá utilizar em casa através do seu fornecedor de Internet.

3.  Clique em **Introdução**.

    A Microsoft utiliza o seu endereço de e-mail para verificar se a sua organização já tem uma [subscrição paga que inclui o Azure RMS](../get-started/requirements-subscriptions.md). Se for esse o caso, não precisa do RMS para indivíduos, pelo que irá iniciar sessão imediatamente e a inscrição self-service para o RMS para indivíduos é cancelada. Se não for encontrada uma subscrição paga para o Azure RMS, irá continuar para o passo seguinte.

4.  Aguarde que uma mensagem de e-mail de confirmação seja enviada para o endereço que especificou. Esta mensagem será enviada pela Microsoft (DoNotReply@microsoft.com) com o assunto **Microsoft RMS**.

5.  Quando receber o e-mail, clique na ligação nas instruções para concluir o processo de inscrição.

6.  A ligação reencaminha-o para uma nova página **Microsoft Rights Management** para que forneça os detalhes da sua conta. Escreva o seu nome próprio e apelido, introduza e confirme uma palavra-passe à sua escolha, selecione o seu país (ou o país mais próximo do seu se o seu país não estiver listado) na lista pendente e, em seguida, clique em **Criar**.

7.  Aguarde por outra mensagem de e-mail da Microsoft que confirme que a sua conta já está pronta a ser utilizada.

8.  Quando receber o e-mail, clique na ligação para iniciar sessão e leia as instruções para transferir e instalar a aplicação de partilha ou clique na ligação de Ajuda para ler o guia do utilizador da aplicação de partilha.

Agora, a sua conta está criada, está pronto para começar a proteger ficheiros e a ler ficheiros que outros utilizadores protegeram. Quando lhe for pedido que inicie sessão para proteger ou ler ficheiros protegidos, introduza o seu endereço de e-mail e palavra-passe que utilizou para criar a conta do RMS para indivíduos.

## Descrição geral técnica do processo de inscrição
O RMS para indivíduos utiliza um processo de inscrição self-service que também é utilizado por outros serviços que utilizam a tecnologia baseada na nuvem da Microsoft para autenticar os utilizadores.

Isto é o que acontece em segundo plano quando um utilizador se inscreve no RMS para indivíduos e a respetiva organização não tem uma subscrição do Office 365 ou do Azure e, por conseguinte, nenhum diretório no Azure para autenticar os utilizadores:

1.  Quando o primeiro utilizador de uma organização solicita uma subscrição do RMS para indivíduos, o nome de domínio fornecido no respetivo endereço de e-mail é verificado para ver se já está associado a um inquilino do Azure. Se não houver um inquilino existente, é criado automaticamente um novo inquilino e um diretório do Azure para a organização, que contém uma conta para este primeiro utilizador. Ao invés de uma subscrição paga do Azure, esta primeira conta não é um administrador global, mas um utilizador padrão. A nova conta utiliza o endereço de e-mail e a palavra-passe que o utilizador forneceu.

    > [!NOTE]
    > Alguns nomes de domínio não podem ser utilizados para criar o diretório e, por conseguinte, não podem ser utilizados para o RMS para indivíduos. A lista de nomes de domínio bloqueados pode ser visualizada neste ficheiro JavaScript Object Notation: [http://portal.aadrm.com/content/blocked_domains.json](http://portal.aadrm.com/content/blocked_domains.json)

    Se for encontrado um inquilino existente, este é verificado para ver se já tem uma subscrição do Azure RMS. Quando não é encontrada qualquer subscrição, é possível adicionar a subscrição do RMS para indivíduos gratuita.

2.  É concedida à organização a subscrição do RMS para indivíduos. Agora, este utilizador pode ser autenticado pelo Azure e pode, em seguida, proteger ficheiros e ler ficheiros que outras pessoas protegeram utilizando o Azure Rights Management. Para proteger e ler ficheiros protegidos, o utilizador tem de ter uma aplicação otimizada por RMS, tal como a [aplicação de partilha Rights Management](../rms-client/sharing-app-windows.md) gratuita.

3.  Quando o segundo utilizador da mesma organização solicita uma subscrição do RMS para indivíduos, é adicionada uma nova conta de utilizador ao diretório do Azure criado anteriormente, utilizando a subscrição do RMS para indivíduos da organização. Este segundo utilizador pode fazer tudo o que o primeiro utilizador podia fazer (proteger ficheiros e ler ficheiros protegidos), mas, além disso, estes dois utilizadores podem agora colaborar mais facilmente em segurança porque podem aplicar rapidamente modelos predefinidos a ficheiros que restringem o acesso a contas no diretório do Azure da sua organização.

4.  Os utilizadores subsequentes da mesma organização seguem o mesmo padrão, adicionando contas de utilizadores (quando novos utilizadores se inscrevem) ao diretório do Azure da sua organização. Quanto mais contas forem adicionadas ao diretório, mais utilizadores podem colaborar com colegas e parceiros de forma mais segura e impedir mais facilmente que as pessoas não autorizadas leiam os seus ficheiros quando não devem ter acesso aos mesmos.

Ao longo deste processo, não é cobrado qualquer valor à organização e não é necessário qualquer trabalho por parte do departamento de TI. No entanto, o departamento de TI pode optar por efetuar um dos seguintes procedimentos:

-   **Gerir as contas e o processo de inscrição**: os administradores de TI podem tornar-se proprietários das contas e diretórios criados automaticamente no Azure. Em seguida, podem gerir as contas através da implementação de soluções de integração de diretórios como o início de sessão único e a sincronização de palavras-passe. Em alternativa, podem impedir os utilizadores de criarem contas ou de se inscreverem no RMS para indivíduos.

    Para obter mais informações, consulte [Como os administradores podem controlar as contas criadas para o RMS para indivíduos](rms-for-individuals-take-control.md).

-   **Gerir o Rights Management**: os administradores de TI podem converter a subscrição do RMS para indivíduos da organização numa subscrição paga que inclui o Azure Rights Management. Ao fazê-lo, as contas e o diretório do Azure existentes são preservadas para uma transição sem problemas para utilizadores existentes que estavam a utilizar o RMS para indivíduos. Todos os ficheiros que os utilizadores protegeram anteriormente continuarão a estar protegidos com as mesmas políticas e as pessoas às quais foram concedidas permissões para utilizar os ficheiros continuarão a poder utilizar os ficheiros da mesma forma.

    Ao realizar este procedimento, a sua organização é beneficiada por poder integrar o Rights Management nos seus fluxos de trabalho, serviços e arquivos de dados. Além disso, já pode gerir o Rights Management porque tem controlo sobre a chave de inquilino da sua organização para o Azure Rights Management. Agora, pode realizar o seguinte:

    -   Configurar o Exchange e o SharePoint para suportar o Azure Rights Management, mesmo que estas estejam em execução no local. O Exchange e o SharePoint são nativamente suportados para os serviços online e são suportados por um conetor para os servidores no local. Para obter mais informações, consulte o seguinte:

        -   As secções do Exchange Online e do SharePoint Online de [Office 365: configuração para os clientes e os serviços online](../deploy-use/configure-office365.md)

        -   [Implementar o conetor Azure Rights Management](../deploy-use/deploy-rms-connector.md)

    -   Efetue a deteção de dados eletrónicos nos dados pertencentes à empresa para poder, se necessário, desencriptar ficheiros que foram protegidos através do Rights Management. Para mais informações, consulte [Configurar superutilizadores para o Azure Rights Management e serviços de deteção ou recuperação de dados](../deploy-use/configure-super-users.md).

    -   Registe toda a atividade do Rights Management, conforme utilizado na sua organização. Isto é extremamente útil porque não só pode monitorizar os ficheiros que estão a ser protegidos e quem está a aceder a esses ficheiros protegidos com êxito, como também pode identificar comportamentos potencialmente suspeitos de pessoas não autorizadas que estão a tentar aceder a ficheiros protegidos. Para obter mais informações, consulte [Registo e análise da utilização do Azure Rights Management](../deploy-use/log-analyze-usage.md).

    -   Forneça aos utilizadores a capacidade de controlar e revogar os seus documentos protegidos, se estas funcionalidades forem suportadas pela sua [Subscrição do Azure RMS](https://technet.microsoft.com/dn858608). Para obter mais informações, consulte [Controlar e revogar os ficheiros](../rms-client/sharing-app-track-revoke.md) no [Guia do utilizador da aplicação de partilha RMS](../rms-client/sharing-app-user-guide.md).

    -   Implemente uma solução “traga a sua própria chave” (BYOK) para que a chave de inquilino do Azure Rights Management seja gerada no local, de acordo com as políticas de TI, e seja transferida em segurança para a Microsoft através da utilização de um Módulo de Hardware de Segurança (HSM). Para mais informações, consulte [Planear e implementar a chave de inquilino do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).


## Passos seguintes
Consulte [Como os administradores podem controlar as contas criadas para o RMS para indivíduos](rms-for-individuals-take-control.md).




<!--HONumber=Apr16_HO4-->


