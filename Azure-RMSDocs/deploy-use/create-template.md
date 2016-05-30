---
# required metadata

title: Como criar, configurar e publicar um modelo personalizado | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d6e9aa0c-1694-4a53-8898-4939f31cc13f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Criar, configurar e publicar um modelo personalizado

*Aplica-se a: Azure Rights Management, Office 365*


Você cria e gerencia modelos personalizados no portal clássico do Azure. Você pode fazê-lo diretamente do portal clássico do Azure ou entrar no centro de administração do Office 365 e escolher os **recursos avançados** para o Rights Management que o redireciona para o portal clássico do Azure.

Use os procedimentos a seguir para criar, configurar e publicar modelos personalizados para o Rights Management.

## Para criar um modelo personalizado

1.  Dependendo de você entrar no centro de administração do Office 365 ou no portal clássico do Azure, execute um dos itens a seguir:

    -   Do [Centro de administração do Office 365](https://portal.office.com/):

        1.  No painel esquerdo, clique em **configurações de serviço**.

        2.  Na página **configurações de serviços**, clique em **gerenciamento de direitos**.

        3.  Na seção **Proteger suas informações**, clique em **Gerenciar**.

        4.  Na seção **gerenciamento de direitos**, clique em **recursos avançados**.

            > [!NOTE]
            > Se você ainda não ativou o Rights Management, primeiro clique em **ativar** e confirme sua ação. Para obter mais informações, consulte [Ativando o Azure Rights Management](activate-service.md).
            > 
            > Se ainda não tiver clicado em **recursos avançados**, depois de ativar o Rights Management, siga as instruções na tela para obter uma assinatura gratuita do Azure, necessária para acessar o portal clássico do Azure.

            Clicar em **recursos avançados** carrega o portal clássico do Azure, no qual você pode gerenciar **RIGHTS MANAGEMENT** para o Azure Active Directory de sua organização.

    -   No [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

        2.  Na página **active directory**, clique em **RIGHTS MANAGEMENT**.

        3.  Selecione o diretório para gerenciar para o Rights Management.

        4.  Se você ainda não ativou o Rights Management, primeiro clique em **ATIVAR** e confirme sua ação.

            > [!NOTE]
            > Para obter mais informações, consulte [Ativando o Azure Rights Management](activate-service.md).

2.  Criar um novo modelo:

    -   No portal clássico do Azure, em **Introdução ao Rights Management**, página de início rápido, clique em **Criar um novo modelo de política de direitos**.

        Se você não vir imediatamente essa página depois de seguir as instruções do Office 365, use as instruções de navegação acima para o portal clássico do Azure.

3.  Na página **Adicionar um novo modelo de política de direitos** , escolha um idioma no qual digitará o nome do modelo e a descrição que os usuários verão (você pode adicionar mais idiomas posteriormente). Em seguida, digite um nome exclusivo e uma descrição, e clique no botão Concluir.

Na página de início rápido **Introdução ao Rights Management** , agora clique em **Gerenciar seus modelos de política de direitos**. Você verá seu modelo recém-criado adicionado à lista de modelos, com um status de **Arquivado**. Nesta fase, o modelo está criado mas não configurado, e não fica visível para os usuários.

## Para configurar e publicar um modelo personalizado

1.  Escolha seu modelo recém-criado na página **MODELOS** no portal clássico do Azure.

2.  Da página de início rápido **Seu modelo foi adicionado** , clique na **Introdução** da etapa 1, **Configurar direitos de usuários e grupos** , então clique em **INICIAR AGORA** ou **ADICIONAR**e selecione os usuários e grupos que terão direito de usar o conteúdo que é protegido pelo novo modelo.

    > [!NOTE]
    > Os usuários ou grupos que você selecionar devem ter um endereço de email. Em um ambiente de produção, esse será quase sempre o caso, mas em um ambiente de teste simples, talvez seja necessário adicionar endereços de email às contas de usuário ou grupos.

    Como uma prática recomendada, use grupos em vez de usuários para simplificar o gerenciamento dos modelos. Se você tiver o Active Directory local e estiver sincronizando ao Azure AD, você pode usar grupos habilitados para email que são grupos de segurança ou grupos de distribuição. No entanto, se você deseja conceder direitos a todos os usuários da organização, será mais eficiente copiar um dos modelos padrão, em vez de especificar vários grupos. Para obter mais informações, consulte [Como copiar um modelo](copy-template.md).

    > [!TIP]
    > Mais tarde você pode adicionar usuários de fora da sua organização ao modelo, usando o [Módulo do Windows PowerShell para Azure Rights Management](install-powershell.md) e usando um dos seguintes métodos:
    > 
    > -   **Usar um objeto de definição de direitos para atualizar um modelo**: especifique os endereços de email externos e seus direitos em um objeto de definição de direitos, que você usará para atualizar seu modelo. É possível especificar o objeto de definição de direitos usando o cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para criar uma variável e, em seguida, fornecer essa variável para o parâmetro -RightsDefinition com o cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) para modificar um modelo existente. No entanto, se você está adicionando esses usuários a um modelo existente, também precisará definir objetos de definição de direitos para os grupos existentes nos modelos e não apenas os usuários externos e novos.
    > -   **Exporte, edite e importe o modelo atualizado**: use o cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar o modelo para um arquivo que você pode editar para adicionar os endereços de email externos desses usuários e seus direitos aos grupos e direitos existentes. Então, use o cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para importar esta mudança de volta para o Azure RMS.

3.  Clique no botão Avançar e, em seguida, atribua um dos direitos listados aos usuários e grupos selecionados.

    Use a descrição exibida para obter mais informações sobre cada direito (e direitos personalizados). Informações mais detalhadas também estão disponíveis em [Configurando os direitos de uso do Azure Rights Management](configure-usage-rights.md). No entanto, os aplicativos que oferecem suporte ao RMS podem variar no modo como implementam esses direitos. Consulte sua documentação e faça seus próprios testes com os aplicativos que os usuários usam para verificar o comportamento antes de implantar o modelo para os usuários. Para tornar esse modelo visível somente para os administradores para este teste, torne este modelo um modelo departamental (etapa 6).

4.  Se você selecionou **Personalizar**, clique no botão Avançar e selecione os direitos personalizados.

    Embora você possa usar qualquer combinação dos direitos individuais disponíveis, em certos aplicativos, alguns direitos podem ter dependências de outros direitos individuais. Quando este for o caso, os direitos dependentes serão selecionados automaticamente.

    > [!TIP]
    > Considere adicionar o direito de **Copiar e Extrair Conteúdo** e conceda isso aos administradores selecionados ou pessoal de outras funções que tenham responsabilidades de recuperação de informações. A concessão desse direito permite remover a proteção, se necessário, de arquivos e emails que serão protegidos usando esse modelo. Essa capacidade de remover a proteção no nível do modelo proporciona um controle mais refinado do que o uso do recurso de superusuário.

5.  Clique no botão Concluir.

6.  Se desejar que o modelo fique visível para apenas um subconjunto de usuários quando eles veem uma lista de modelos em aplicativos: Clique em **ESCOPO** para configurar isto como um modelo departamental e clique em **INICIAR AGORA**. Caso contrário, vá para a etapa 9.

    Mais informações sobre modelos departamentais: Por padrão, todos os usuários do seu diretório do Azure veem todos os modelos publicados e podem selecioná-los de aplicativos quando desejarem proteger conteúdo. Se você desejar que somente usuários específicos vejam alguns dos modelos publicados, crie um escopo dos modelos para esses usuários. Assim, apenas esses usuários poderão selecionar esses modelos. Outros usuários que você não especificar não verão os modelos e, portanto, não poderão selecioná-los. Essa técnica pode tornar a escolha do modelo correto mais fácil para os usuários, especialmente quando você cria modelos que são projetados para ser usados por grupos ou departamentos específicos. Em seguida, os usuários veem somente os modelos criados para eles.

    Por exemplo, você criou um modelo para o departamento de Recursos Humanos que aplica a permissão Somente leitura aos membros do departamento Financeiro. Para que somente os membros do departamento de Recursos Humanos possam aplicar esse modelo ao usarem o aplicativo de compartilhamento do Rights Management, faça o escopo o modelo para o grupo habilitado para email denominado RecursosHumanos. Assim, somente os membros desse grupo poderão ver e aplicar esse modelo.

7.  Na página **VISIBILIDADE DO MODELO**, selecione os usuários e grupos que poderão ver e selecionar o modelo dos aplicativos aprimorados pelo RMS. Como antes, como uma prática recomendada, use grupos em vez de usuários, e os grupos ou usuários selecionados devem ter um endereço de email.

8.  Clique no botão Avançar e decida se é necessário configurar a compatibilidade de aplicativos para o modelo departamental. Se você quiser, clique em **COMPATIBILIDADE DO APLICATIVO**, marque a caixa de seleção e clique em **Concluir**.

    Por que você talvez precise configurar a compatibilidade de aplicativos? Nem todos os aplicativos podem oferecer suporte a modelos departamentais. Para fazer isso, o aplicativo deve primeiro ser autenticado com o serviço RMS antes de baixar os modelos. Se o processo de autenticação não ocorrer, por padrão, nenhum dos modelos departamentais são baixados. Você pode substituir esse comportamento especificando que todos os modelos departamentais devem baixar, configurando a compatibilidade do aplicativo e marcando a caixa de seleção **Mostrar este modelo a todos os usuários quando os aplicativos não derem suporte à identidade do usuário** .

    Por exemplo, se não configurar a compatibilidade de aplicativos para o modelo departamental em nosso exemplo de Recursos Humanos, somente os usuários do departamento de Recursos Humanos veem o modelo departamental quando usam o aplicativo de compartilhamento RMS, mas nenhum usuário vê o modelo departamental ao usar o Outlook Web Access (OWA) do Exchange Server 2013, pois o Exchange OWA e o Exchange ActiveSync atualmente não oferecem suporte a modelos departamentais. Se substituir esse comportamento padrão configurando a compatibilidade de aplicativos, somente os usuários do departamento de Recursos Humanos veem o modelo departamental quando usarem o aplicativo de compartilhamento RMS, mas todos os usuários veem o modelo departamental quando usam o Outlook Web Access (OWA). Se os usuários usarem o OWA ou o Exchange ActiveSync do Exchange Online, todos os usuários verão os modelos departamentais ou nenhum usuário os verá, com base no status de modelo (arquivamento ou publicado) no Exchange Online.

    O Office 2016 dá suporte nativo a modelos departamentais. O mesmo ocorre com o Office 2013 da versão 15.0.4727.1000 em diante, lançada em junho de 2015 como parte do ([KB 3054853](https://support.microsoft.com/kb/3054853))).

    > [!NOTE]
    > Se você tiver aplicativos que ainda não dão suporte nativo a modelos departamentais, você poderá usar um script de download do modelo RMS personalizado ou outras ferramentas para implantar esses modelos na pasta local do cliente RMS. Em seguida, esses aplicativos exibem corretamente os modelos departamentais somente para os usuários e grupos que você selecionou para o escopo de modelo:
    > 
    > -   Para o Office 2010, a pasta do cliente é **%localappdata%\Microsoft\DRM\Templates**.
    > -   Em um computador cliente que baixou todos os modelos, você pode copiar e colar os arquivos de modelo em outros computadores.
    > 
    > Você pode [baixar o script do modelo RMS personalizado no site do Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Se vir um erro quando clicar neste link, você provavelmente ainda não se inscreveu no Microsoft Connect.   Para se inscrever:
    > 
    > 1.  Vá para o [site do Microsoft Connect](http://www.connect.microsoft.com) e entre com sua Conta da Microsoft.
    > 2.  Clique em **Diretório** e selecione a categoria **Exibir produtos do Connect que atualmente não aceitam comentários**.
    > 3.  Procure por **Rights Management Services** e, para o programa **Recursos do Enterprise do Microsoft RMS**, clique em **Ingressar**.

9. Clique em **CONFIGURAR** e adicione outros idiomas que os usuários usam, juntamente com o nome e descrição desse modelo nesse idioma. Quando você tem usuários em vários idiomas, é importante adicionar cada idioma usado e fornecer um nome e uma descrição nesse idioma. Assim, os usuários verão o nome e a descrição do modelo no mesmo idioma do seu sistema operacional cliente, o que garante que eles entendam a política aplicada a um documento ou uma mensagem de email. Se não houver correspondência com o seu sistema operacional cliente, o nome e a descrição que eles veem voltarão para o idioma e a descrição definidos quando o modelo foi criado.

    Em seguida, verifique se quer alterar as seguintes configurações:

    |Setting|Mais informações|
    |-----------|--------------------|
    |**expiração de conteúdo**|Defina uma data ou um número de dias para este modelo quando os arquivos que são protegidos pelo modelo não abrirem. Você pode especificar uma data ou um número de dias a partir do momento em que a proteção for aplicada ao arquivo.<br /><br />Quando você especifica uma data, ela entra em vigor à meia-noite, em seu fuso horário atual.|
    |**acesso offline**|Use essa configuração para equilibrar todos os requisitos de segurança que existirem em relação à exigência de que os usuários possam abrir arquivos protegidos quando não tiverem conexão com a Internet.<br /><br />Se for especificado que o conteúdo não está disponível sem uma conexão com a Internet ou que está disponível apenas por um determinado número de dias, quando esse limite for atingido, os usuários deverão ser autenticados novamente e seu acesso será registrado. Quando isso acontecer, se as credenciais não estiverem armazenadas em cache, os usuários serão solicitados a entrar antes que possam abrir o arquivo.<br /><br />Além da reautenticação, a política e os membros do grupo de usuário serão reavaliados. Isso significa que os usuários podem experimentar diferentes resultados de acesso para o mesmo arquivo, caso algo tenha mudado na política ou na associação do grupo desde o último acesso ao arquivo.|

10. Quando estiver certo de que o modelo está configurado adequadamente para os usuários, clique em **PUBLICAR** para tornar o modelo visível aos usuários, e então clique em **SALVAR**.

11. Clique no botão Voltar no portal clássico para retornar à página **MODELOS**, na qual seu modelo agora tem status atualizado como **Publicado**.

Para fazer qualquer alteração no seu modelo, selecione-o e, em seguida, use as etapas de início rápido novamente. Ou, selecione uma das seguintes opções:

-   Para adicionar mais usuários e grupos e definir os direitos para esses usuários e grupos: Clique em **DIREITOS**, e então clique em **ADICIONAR**.

-   Para remover usuários ou grupos que você selecionou anteriormente: clique em **DIREITOS**, selecione o usuário ou grupo na lista e, em seguida, clique em **EXCLUIR**.

-   Para alterar quais usuários podem ver os modelos para selecioná-los em aplicativos: clique em **ESCOPO**, e então clique em **ADICIONAR** ou **EXCLUIR**, ou **COMPATIBILIDADE DO APLICATIVO**.

-   Para tornar o modelo invisível para todos os usuários: clique em **CONFIGURAR**, clique em **ARQUIVAR**, e então clique em **SALVAR**.

-   Para fazer outras alterações de configuração: clique em **CONFIGURAR**, faça as alterações, e então clique em **SALVAR**.

> [!WARNING]
> Quando você fizer alterações em um modelo salvo anteriormente, os clientes não verão essas alterações nos modelos até que eles sejam atualizados em seus computadores. Para obter mais informações, consulte a seção [Atualizando modelos para usuários](refresh-templates.md).

## Consulte também
[Configurar modelos personalizados do Azure Rights Management](configure-custom-templates.md)

<!--HONumber=Apr16_HO4-->


