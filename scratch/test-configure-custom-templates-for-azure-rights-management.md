---
title: TESTAR a configuração de modelos personalizados do Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# ANTES DE: configurar modelos personalizados do Azure Rights Management
Depois da ativação do Azure Rights Management (Azure RMS), os usuários podem usar automaticamente dois modelos padrão que facilitam a aplicação de políticas a arquivos confidenciais que restringem o acesso a usuários autorizados em sua organização. Esses dois modelos têm as seguintes restrições de política de direitos:

-   Visualização de somente leitura para o conteúdo protegido

    -   Nome de exibição: **&lt;nome da organização&gt; - somente exibição confidencial**

    -   Permissão específica: Exibir Conteúdo

-   As permissões de leitura ou modificação do conteúdo protegido

    -   Nome de exibição: **&lt;nome da organização&gt; - confidencial**

    -   Permissões específicas: Exibir Conteúdo, Salvar Arquivo, Editar Conteúdo, Exibir Direitos Atribuídos, Permitir Macros, Encaminhar, Responder e Responder a Todos

Além disso, o [aplicativo RMS sharing](http://technet.microsoft.com/library/dn339006.aspx) permite que os usuários definam seus próprios conjuntos de permissões. E, para o cliente Outlook e Outlook Web Access, os usuários podem selecionar a opção **Não Encaminhar** para mensagens de email.

Para muitas organizações, os modelos padrão podem ser suficientes. Porém, se você quiser criar seus próprios modelos personalizados de política de direitos, isso é possível. Os motivos para criar um modelo personalizado incluem o seguinte:

-   Você quer um modelo para conceder direitos a um subconjunto de usuários na organização, ao invés de todos os usuários.

-   Você deseja que apenas um subconjunto de usuários possa ver e selecionar um modelo (modelo departamental) de aplicativos, e não que todos os usuários da organização possam ver e selecionar o modelo.

-   Você quer definir um direito personalizado para um modelo, como Exibir e Editar, mas não Copiar e Imprimir.

-   Você quer configurar opções adicionais em um modelo que incluem uma data de validade e se o conteúdo pode ser acessado sem uma conexão com a Internet.

Para que os usuários possam selecionar um modelo personalizado que contenha definições como essas, é necessário primeiro criar um modelo personalizado, configurá-lo e depois publicá-lo.

Use as seções a seguir para ajudar a configurar e usar modelos personalizados:

-   [Como criar, configurar e publicar um modelo personalizado](configure-custom-templates.md#BKMK_HowToConfigureCustomTemplates)

-   [Como copiar um modelo](configure-custom-templates.md#BKMK_HowToCopyTemplates)

-   [Como remover (arquivar) modelos](configure-custom-templates.md#BKMK_HowToArchiveTemplates)

-   [Atualizando modelos para usuários](configure-custom-templates.md#BKMK_RefreshingTemplates)

-   [Referência do Windows PowerShell](configure-custom-templates.md#BKMK_PowerShellTemplates)

## Como criar, configurar e publicar um modelo personalizado
Você cria e gerencia modelos personalizados no portal clássico do Azure. Você pode fazê-lo diretamente do portal clássico do Azure ou entrar no centro de administração do Office 365 e escolher os **recursos avançados** para o Rights Management que o redireciona para o portal clássico do Azure.

Use os procedimentos a seguir para criar, configurar e publicar modelos personalizados para o Rights Management.

#### Para criar um modelo personalizado

1.  Dependendo de você entrar no centro de administração do Office 365 ou no portal clássico do Azure, execute um dos itens a seguir:

    -   Do [Centro de administração do Office 365](https://portal.office.com/):

        1.  No painel esquerdo, clique em **configurações de serviços**.

        2.  Na página **configurações de serviços** , clique em **gerenciamento de direitos**.

        3.  Na seção **Proteger suas informações** , clique em **Gerenciar**.

        4.  Na seção **gerenciamento de direitos** , clique em **recursos avançados**.

            > [!NOTE]
            > Se você ainda não ativou o Rights Management, primeiro clique em **ativar** e confirme sua ação. Para obter mais informações, consulte [Ativando o Azure Rights Management](activate-service.md).
            > 
            > Se ainda não tiver clicado em **recursos avançados**, depois de ativar o Rights Management, siga as instruções na tela para obter uma assinatura gratuita do Azure, necessária para acessar o portal clássico do Azure.

            Clicar em **recursos avançados** carrega o portal clássico do Azure, no qual você pode gerenciar **RIGHTS MANAGEMENT** para o Azure Active Directory de sua organização.

    -   No [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081):

        1.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

        2.  Na página **active directory** , clique em **RIGHTS MANAGEMENT**.

        3.  Selecione o diretório para gerenciar para o Rights Management.

        4.  Se você ainda não ativou o Rights Management, primeiro clique em **ATIVAR** e confirme sua ação.

            > [!NOTE]
            > Para obter mais informações, consulte [Ativando o Azure Rights Management](activate-service.md).

2.  Criar um novo modelo:

    -   No portal clássico do Azure, na página de início rápido **Introdução ao Rights Management**, clique em **Criar um novo modelo de política de direitos**.

        Se você não vir imediatamente essa página depois de seguir as instruções do Office 365, use as instruções de navegação acima para o portal clássico do Azure.

3.  Na página **Adicionar um novo modelo de política de direitos** , escolha um idioma no qual digitará o nome do modelo e a descrição que os usuários verão (você pode adicionar mais idiomas posteriormente). Em seguida, digite um nome exclusivo e uma descrição, e clique no botão Concluir.

Na página de início rápido **Introdução ao Rights Management** , agora clique em **Gerenciar seus modelos de política de direitos**. Você verá seu modelo recém-criado adicionado à lista de modelos, com um status de **Arquivado**. Nesta fase, o modelo está criado mas não configurado, e não fica visível para os usuários.

#### Para configurar e publicar um modelo personalizado

1.  Escolha seu modelo recém-criado na página **MODELOS** no portal clássico do Azure.

2.  Da página de início rápido **Seu modelo foi adicionado** , clique na **Introdução** da etapa 1, **Configurar direitos de usuários e grupos** , então clique em **INICIAR AGORA** ou **ADICIONAR**e selecione os usuários e grupos que terão direito de usar o conteúdo que é protegido pelo novo modelo.

    > [!NOTE]
    > Os usuários ou grupos que você selecionar devem ter um endereço de email. Em um ambiente de produção, esse será quase sempre o caso, mas em um ambiente de teste simples, talvez seja necessário adicionar endereços de email às contas de usuário ou grupos.

    Como uma prática recomendada, use grupos em vez de usuários para simplificar o gerenciamento dos modelos. Se você tiver o Active Directory local e estiver sincronizando ao Azure AD, você pode usar grupos habilitados para email que são grupos de segurança ou grupos de distribuição. No entanto, se você deseja conceder direitos a todos os usuários da organização, será mais eficiente copiar um dos modelos padrão, em vez de especificar vários grupos. Para obter mais informações, consulte a seção [Como copiar um modelo](configure-custom-templates.md#BKMK_HowToCopyTemplates) neste tópico.

    > [!TIP]
    > Mais tarde você pode adicionar usuários de fora da sua organização ao modelo, usando o [Módulo do Windows PowerShell para Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx) e usando um dos seguintes métodos:
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

8.  Clique no botão Avançar e decida se é necessário configurar a compatibilidade de aplicativos para o modelo departamental. Se você quiser, clique em **COMPATIBILIDADE DE APLICATIVOS**, marque a caixa de seleção e clique em **Concluir**.

    Por que você talvez precise configurar a compatibilidade de aplicativos? Nem todos os aplicativos podem oferecer suporte a modelos departamentais. Para fazer isso, o aplicativo deve primeiro ser autenticado com o serviço RMS antes de baixar os modelos. Se o processo de autenticação não ocorrer, por padrão, nenhum dos modelos departamentais são baixados. Você pode substituir esse comportamento especificando que todos os modelos departamentais devem baixar, configurando a compatibilidade do aplicativo e marcando a caixa de seleção **Mostrar este modelo a todos os usuários quando os aplicativos não derem suporte à identidade do usuário** .

    Por exemplo, se não configurar a compatibilidade de aplicativos para o modelo departamental em nosso exemplo de Recursos Humanos, somente os usuários do departamento de Recursos Humanos veem o modelo departamental quando usam o aplicativo de compartilhamento RMS, mas nenhum usuário vê o modelo departamental ao usar o Outlook Web Access (OWA) do Exchange Server 2013, pois o Exchange OWA e o Exchange ActiveSync atualmente não oferecem suporte a modelos departamentais. Se substituir esse comportamento padrão configurando a compatibilidade de aplicativos, somente os usuários do departamento de Recursos Humanos veem o modelo departamental quando usarem o aplicativo de compartilhamento RMS, mas todos os usuários veem o modelo departamental quando usam o Outlook Web Access (OWA). Se os usuários usarem o OWA ou o Exchange ActiveSync do Exchange Online, todos os usuários verão os modelos departamentais ou nenhum usuário os verá, com base no status de modelo (arquivamento ou publicado) no Exchange Online.

    O Office 2016 oferece suporte nativo a modelos departamentais, assim como o Office 2013 com as atualizações mais recentes do Office ([KB 3054853](https://support.microsoft.com/kb/3054853)).

    > [!NOTE]
    > Se tiver aplicativos que ainda não dão suporte nativo a modelos departamentais, você poderá usar um script de download do modelo RMS personalizado ou outras ferramentas para implantar esses modelos na pasta local do cliente RMS. Em seguida, esses aplicativos exibem corretamente os modelos departamentais somente para os usuários e grupos que você selecionou para o escopo de modelo:
    > 
    > -   Para o Office 2010, a pasta do cliente é **%localappdata%\Microsoft\DRM\Templates**.
    > -   Em um computador cliente que baixou todos os modelos, você pode copiar e colar os arquivos de modelo em outros computadores.
    > 
    > Você pode [baixar o script do modelo RMS personalizado no site do Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Se vir um erro quando clicar neste link, você provavelmente ainda não se inscreveu no Microsoft Connect.   Para se inscrever:
    > 
    > 1.  Vá para o [site do Microsoft Connect](http://www.connect.microsoft.com) e entre com sua Conta da Microsoft.
    > 2.  Clique em **Diretório** e selecione a categoria **Exibir produtos do Connect que atualmente não aceitam comentários**.
    > 3.  Procure por **Rights Management Services** e, para o programa **Microsoft RMS Enterprise Features**, clique em **Ingressar**.

9. Clique em **CONFIGURAR** e adicione outros idiomas que os usuários usam, juntamente com o nome e descrição desse modelo nesse idioma. Quando você tem usuários em vários idiomas, é importante acrescentar cada idioma usado e fornecer um nome e uma descrição nesse idioma. Assim, os usuários verão o nome e a descrição do modelo no mesmo idioma do seu sistema operacional cliente, o que garante que eles entendam a política aplicada a um documento ou uma mensagem de email. Se não houver correspondência com o seu sistema operacional cliente, o nome e a descrição que eles veem voltarão para o idioma e a descrição definidos quando o modelo foi criado.

    Em seguida, verifique se quer alterar as seguintes configurações:

    |Setting|Mais informações|
    |-----------|--------------------|
    |**expiração de conteúdo**|Defina uma data ou um número de dias para este modelo quando os arquivos que são protegidos pelo modelo não abrirem. Você pode especificar uma data ou um número de dias a partir do momento em que a proteção for aplicada ao arquivo.<br /><br />Quando você especifica uma data, ela entra em vigor à meia-noite, em seu fuso horário atual.|
    |**acesso offline**|Use essa configuração para equilibrar todos os requisitos de segurança que existirem em relação à exigência de que os usuários possam abrir arquivos protegidos quando não tiverem conexão com a Internet.<br /><br />Se for especificado que o conteúdo não está disponível sem uma conexão com a Internet ou que está disponível apenas por um determinado número de dias, quando esse limite for atingido, os usuários deverão ser autenticados novamente e seu acesso será registrado. Quando isso acontecer, se as credenciais não estiverem armazenadas em cache, os usuários serão solicitados a entrar antes que possam abrir o arquivo.<br /><br />Além da reautenticação, a política e os membros do grupo de usuário serão reavaliados. Isso significa que os usuários podem experimentar diferentes resultados de acesso para o mesmo arquivo, caso algo tenha mudado na política ou na associação do grupo desde o último acesso ao arquivo.|

10. Quando estiver certo de que o modelo está configurado adequadamente para os usuários, clique em **PUBLICAR** para tornar o modelo visível para os usuários, e então clique em **SALVAR**.

11. Clique no botão Voltar no portal clássico para retornar para a página **MODELOS**, na qual seu modelo agora tem status atualizado de **Publicado**.

Para fazer qualquer alteração no seu modelo, selecione-o e, em seguida, use as etapas de início rápido novamente. Ou, selecione uma das seguintes opções:

-   Para adicionar mais usuários e grupos e definir os direitos para esses usuários e grupos: Clique em **DIREITOS**, e então clique em **ADICIONAR**.

-   Para remover usuários ou grupos que você selecionou anteriormente: Clique em **DIREITOS**, selecione o usuário ou grupo na lista e, em seguida, clique em **EXCLUIR**.

-   Para alterar quais usuários podem ver os modelos para selecioná-los em aplicativos: Clique em **ESCOPO**, e então clique em **ADICIONAR** ou **EXCLUIR**, ou **COMPATIBILIDADE DE APLICATIVOS**.

-   Para tornar o modelo invisível para todos os usuários: Clique em **CONFIGURAR**, clique em **ARQUIVAR**, e então clique em **SALVAR**.

-   Para fazer outras alterações de configuração: Clique em **CONFIGURAR**, faça as alterações, e então clique em **SALVAR**.

> [!WARNING]
> Quando você fizer alterações em um modelo salvo anteriormente, os clientes não verão essas alterações nos modelos até que eles sejam atualizados em seus computadores. Para obter mais informações, consulte a seção [Atualizando modelos para usuários](configure-custom-templates.md#BKMK_RefreshingTemplates) neste tópico.

## Como copiar um modelo
Se for necessário criar um novo modelo que tenha configurações bem parecidas às de um modelo existente, selecione o modelo original na página **MODELOS** , clique em **COPIAR**, especifique um nome exclusivo e faça as alterações necessárias.

> [!IMPORTANT]
> Ao copiar um modelo, o status **Publicado** ou **Arquivado** também é copiado. Então, se você copiar um modelo publicado, seu status será publicado a menos que você o altere.

Você pode copiar modelos personalizados e modelos padrão. Como uma prática recomendada, copie um dos modelos padrão em vez de criar um novo modelo personalizado se quiser o modelo de concessão de direitos a todos os usuários em sua organização. Este método significa que você não tem que criar ou selecionar vários grupos para especificar todos os usuários. Neste cenário no entanto, certifique-se de especificar um novo nome e uma descrição para o modelo copiado para outros idiomas.

## Como remover (arquivar) modelos
Os modelos padrão não podem ser excluídos, mas podem ser arquivados para que os usuários não os vejam.

Da mesma forma, se você publicou um modelo personalizado e não quer mais que os usuários o vejam, é possível editar o modelo e escolher **ARQUIVAR** e **SALVAR** na página **CONFIGURAR** . Ou ainda, você pode selecionar a partir da página **MODELOS** e selecionar **ARQUIVAR**.

Como não é possível editar os modelos padrão, para arquivar esses modelos é necessário usar a opção **ARQUIVAR** da página **MODELOS** . Não é possível arquivar a opção **Não encaminhar** do Outlook.

#### Para remover um modelo padrão

-   Na página **modelos** , selecione o modelo padrão e clique em **ARQUIVAR**.

O status é alterado de **Publicado** para **Arquivado**. Se você mudar de ideia, selecione o modelo e clique em **PUBLICAR**.

## Atualizando modelos para usuários
Ao usar o Azure RMS, os modelos são baixados automaticamente para os computadores clientes para que os usuários possam selecioná-los em seus aplicativos. No entanto, talvez seja necessário tomar medidas adicionais se forem feitas alterações nos modelos:

|Aplicativo ou serviço|Como os modelos são atualizados após as alterações|
|--------------------------|---------------------------------------------|
|Exchange Online|Configuração manual necessária para atualizar os modelos.<br /><br />Para as etapas de configuração, expanda a seção a seguir, [Exchange Online somente: como configurar o Exchange para baixar modelos personalizados alterados](configure-custom-templates.md#BKMK_ExchangeOnlineTemplatesUpdate).|
|Office 365|Atualizado automaticamente, não são necessários outros procedimentos.|
|Office 2016 e Office 2013<br /><br />Aplicativo de compartilhamento RMS para Windows|Atualizado automaticamente, por agendamento:<br /><br />Para essas versões posteriores do Office: o intervalo de atualização padrão é a cada 7 dias.<br /><br />Para o aplicativo RMS sharing para Windows: da versão 1.0.1784.0 em diante, o intervalo de atualização padrão é a cada 1 dia. As versões anteriores têm um intervalo de atualização padrão de a cada 7 dias.<br /><br />Para forçar uma atualização antes desse agendamento, expanda a seção a seguir, [Aplicativo RMS sharing para Windows, Office 2013 e Office 2016: como forçar uma atualização de um modelo personalizado alterado](#BKMK_Office2013ForceUpdate).|
|Office 2010|Atualizado quando os usuários fazem logon.<br /><br />Para forçar uma atualização, peça ou force os usuários a fazerem logoff e logon novamente. Alternativamente, consulte a seção a seguir: [Somente Office 2010: Como forçar uma atualização para um modelo personalizado alterado](#BKMK_Office2010ForceUpdate).|
Para dispositivos móveis que usam o aplicativo RMS sharing, os modelos são baixados (e atualizados, se necessário) automaticamente sem configuração adicional necessária.

### Somente Exchange Online: como configurar o Exchange para baixar modelos personalizados alterados
Se você já configurou o IRM (Gerenciamento de Direitos de Informação) para o Exchange Online, os modelos personalizados não serão baixados para os usuários até que as alterações a seguir sejam feitas usando o Windows PowerShell no Exchange Online.

> [!NOTE]
> Para obter mais informações sobre como usar o Windows PowerShell no Exchange Online, consulte [Usar o PowerShell com o Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Esse procedimento deve ser feito cada vez que um modelo for alterado.

##### Para atualizar modelos para o Exchange Online

1.  Usando o Windows PowerShell no Exchange Online, conecte-se ao serviço:

    1.  Forneça seu nome de usuário e senha do Office 365:

        ```
        $Cred = Get-Credential
        ```

    2.  Conecte-se ao serviço Exchange Online executando os seguintes dois comandos:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Use o cmdlet [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) para importar novamente o TPD (domínio de publicação confiável) do Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Por exemplo, se seu nome TPD for **RMS Online - 1** (um nome comum para muitas organizações), digite: **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Para verificar seu nome TPD, você pode usar o cmdlet [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx).

3.  Para confirmar se os modelos foram importados com sucesso, espere alguns minutos e, em seguida, execute o cmdlet [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) e defina o Tipo como Todos. Por exemplo:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > É útil manter uma cópia da saída para que você possa facilmente copiar os nomes de modelo ou GUIDs se você arquivar um modelo mais tarde.

4.  Para cada modelo importado que você deseja disponibilizar no Outlook Web App, você deve usar o cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) e definir o Tipo a ser distribuído:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Visto que o Outlook Web Access armazena a interface do usuário por 24 horas, os usuários não poderão ver o novo modelo por até um dia.

Além disso, se você arquivar um modelo (personalizado ou padrão) e usar o Exchange Online com o Office 365, os usuários continuarão vendo os modelos arquivados se usarem o aplicativo Web Outlook ou dispositivos móveis que utilizam o protocolo ActiveSync Exchange.

Para que os usuários não vejam esses modelos, conecte-se ao serviço usando o Windows PowerShell no Exchange Online, em seguida, use o cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) executando o seguinte comando:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### Office 2016, Office 2013 e aplicativo RMS sharing para Windows: como forçar uma atualização de um modelo personalizado alterado
Editando o registro nos computadores que executam o Office 2016, o Office 2013 ou o aplicativo Rights Management (RMS) sharing para Windows, você pode alterar o agendamento automático para que os modelos alterados sejam atualizados em computadores com mais frequência do que seus valores padrão. Você também pode forçar uma atualização imediata excluindo os dados existentes em um valor de registro.

> [!WARNING]
> Se o Editor de Registro for usado de forma incorreta, podem ocorrer problemas graves que podem exigir a reinstalação do sistema operacional. A Microsoft não garante que seja possível solucionar problemas resultantes do uso incorreto do Editor de Registro. Use o Editor de Registro por sua conta e risco.

##### Para alterar o agendamento automático

1.  Ao utilizar um editor de registro, crie e defina um dos seguintes valores de registro:

    -   Para definir uma frequência de atualização em dias (mínimo de 1 dia):  Crie um novo valor de registro denominado **TemplateUpdateFrequency** e defina um valor inteiro para os dados que especifica a frequência em dias para baixar todas as alterações para um modelo baixado. Use a tabela a seguir para localizar o caminho do registro para criar esse novo valor de registro.

        |Registrar caminho|Tipo|Valor|
        |-----------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   Para definir uma frequência de atualização em segundos (mínimo de 1 segundo):  Crie um novo valor de registro denominado **TemplateUpdateFrequencyInSeconds** e definir um valor inteiro para os dados que especifica a frequência em segundos para baixar todas as alterações para um modelo baixado. Use a tabela a seguir para localizar o caminho do registro para criar esse novo valor de registro.

        |Registrar caminho|Tipo|Valor|
        |-----------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    Certifique-se de criar e definir um desses valores de registro, não ambos. Se ambos estiverem presentes, **TemplateUpdateFrequency** será ignorado.

2.  Se você quiser forçar uma atualização imediata dos modelos, vá para o próximo procedimento. Caso contrário, reinicie seus aplicativos do Office e instâncias do Explorador de arquivos agora.

##### Para forçar uma atualização imediata

1.  Usando um editor de registro, exclua os dados do valor **LastUpdatedTime** . Por exemplo, os dados poderão exibir **2015-04-20T15:52**; exclua 2015-04-20T15:52 para que nenhum dado seja exibido. Use a tabela a seguir para localizar o caminho do registro de forma a excluir esses dados de valor de registro.

    |Registrar caminho|Tipo|Valor|
    |-----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\&lt;MicrosoftRMS_FQDN&gt;\Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > No caminho do Registro, *<MicrosoftRMS_FQDN>* refere-se ao FQDN do serviço Microsoft RMS. Se você quiser verificar este valor:
    > 
    > 1.  Execute o cmdlet [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS. Se você ainda não instalou o módulo do Windows PowerShell para o Azure RMS, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).
    > 2.  A partir da saída, identifique o valor **LicensingIntranetDistributionPointUrl**
    > 
    >     Por exemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  No valor, remova **https://** e **/_wmcs/licensing** dessa cadeia de caracteres. O valor restante é o FQDN do serviço Microsoft RMS. Em nosso exemplo, o FQDN do serviço Microsoft RMS seria o seguinte valor:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Exclua a seguinte pasta e todos os arquivos que ela contém: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie seus aplicativos do Office e instâncias do Explorador de arquivos.

### Somente Office 2010: como forçar uma atualização de um modelo personalizado alterado
Ao editar o registro nos computadores que executam o Office 2010, você pode definir um valor para que os modelos alterados sejam atualizados em computadores sem esperar que os usuários façam logoff e logon novamente. Você também pode forçar uma atualização imediata excluindo os dados existentes em um valor de registro.

> [!WARNING]
> Se o Editor de Registro for usado de forma incorreta, podem ocorrer problemas graves que podem exigir a reinstalação do sistema operacional. A Microsoft não garante que seja possível solucionar problemas resultantes do uso incorreto do Editor de Registro. Use o Editor de Registro por sua conta e risco.

##### Para alterar a frequência de atualização

1.  Usando um editor de registro, crie um novo valor de registro denominado **UpdateFrequency** e defina um valor inteiro para os dados que especifica a frequência em dias para baixar todas as alterações para um modelo baixado. Use a tabela a seguir para localizar o caminho do registro para criar esse novo valor de registro.

    |Registrar caminho|Tipo|Valor|
    |-----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  Se você quiser forçar uma atualização imediata dos modelos, vá para o próximo procedimento. Caso contrário, reinicie os aplicativos do Office agora.

##### Para forçar uma atualização imediata

1.  Usando um editor de registro, exclua os dados do valor **LastUpdatedTime** . Por exemplo, os dados poderão exibir **2015-04-20T15:52**; exclua 2015-04-20T15:52 para que nenhum dado seja exibido. Use a tabela a seguir para localizar o caminho do registro de forma a excluir esses dados de valor de registro.

    |Registrar caminho|Tipo|Valor|
    |-----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  Exclua a seguinte pasta e todos os arquivos que ela contém: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie seus aplicativos do Office.

## Referência do Windows PowerShell
Tudo que você pode fazer no portal clássico do Azure para criar e gerenciar modelos, você pode fazer na linha de comando, usando o Windows PowerShell. Além disso, você pode exportar e importar modelos, de modo que você possa copiar os modelos entre locatários ou realizar edições em massa de propriedades complexas em modelos, como nomes e descrições.

Você pode também usar a exportação e importação para fazer backup e restaurar seus modelos personalizados, como melhor prática, fazer backup regularmente de seus modelos personalizados, para que, se você fizer uma alteração não pretendida, poderá revertê-la facilmente para uma versão anterior.

> [!IMPORTANT]
> Para usar o Windows PowerShell para criar e gerenciar modelos de política de direitos do Azure RMS, você deve ter pelo menos a versão 2.0.0.0 do [módulo Windows PowerShell para Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Se você instalou este módulo do Windows PowerShell anteriormente, execute o seguinte comando em uma janela do PowerShell para verificar o número de versão: `(Get-Module aadrm -ListAvailable).Version`

Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

Os cmdlets que oferecem suporte à criação e gerenciamento de modelos são:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Expout-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Impout-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## Próximas etapas
Depois de configurar modelos personalizados para o Azure Rights Management, use o [Roteiro de implantação do Azure Rights Management](deployment-roadmap.md) para verificar se existem outras etapas de configuração que você pode fazer antes de implementar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para os usuários e administradores. Se não houver outras etapas de configuração que você precise executar, consulte [Usando o Azure Rights Management](using-azure-rights-management.md) para obter diretrizes operacionais para dar suporte a uma implantação bem-sucedida para sua organização.

## Consulte também
[Configurando o Azure Rights Management](configuring-azure-rights-management.md)

<!--HONumber=Apr16_HO3-->


