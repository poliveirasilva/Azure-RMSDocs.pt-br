---
# required metadata

title: Proteção por RMS com a FCI (Infraestrutura de Classificação de Arquivos) do Windows Server | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteção por RMS com a FCI (Infraestrutura de Classificação de Arquivos) do Windows Server

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Use este artigo para obter as instruções e um script para usar o cliente do Rights Management (RMS) com a ferramenta de Proteção por RMS para configurar o Gerenciador de Recursos de Servidor de Arquivos e a Infraestrutura de Classificação de Arquivos (FCI).

Esta solução permite proteger automaticamente todos os arquivos em uma pasta em um servidor de arquivos executando o Windows Server ou protege automaticamente os arquivos que atendem a critérios específicos. Por exemplo, os arquivos que foram classificados como contendo informações confidenciais ou sensíveis. Esta solução usa o Azure RMS (Azure Rights Management) para proteger os arquivos, portanto, você deve ter essa tecnologia implantada em sua organização.

> [!NOTE]
> Apesar de o Azure RMS incluir um [conector](../deploy-use/deploy-rms-connector.md) que dá suporte à infraestrutura de classificação de arquivos, essa solução dá suporte apenas à proteção nativa, por exemplo, arquivos do Office.
> 
> Para dar suporte a todos os tipos de arquivo com a infraestrutura de classificação de arquivos, você deve usar o módulo de **Proteção por RMS** do Windows PowerShell, conforme documentado neste artigo. Os cmdlets de Proteção por RMS, como o aplicativo de RMS sharing, dão suporte tanto à proteção genérica como à proteção nativa, o que significa que todos os arquivos podem ser protegidos. Para obter mais informações sobre os diferentes níveis de proteção, consulte a seção [Níveis de proteção - nativa e genérica](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) no tópico [Guia do administrador do aplicativo de compartilhamento Rights Management](sharing-app-admin-guide.md).

As instruções a seguir são para o Windows Server 2012 R2 ou o Windows Server 2012. Se você executar outras versões com suporte do Windows, talvez seja necessário adaptar algumas das etapas para as diferenças entre a versão do seu sistema operacional e o documentado neste artigo.

## Pré-requisitos da proteção por Azure RMS com FCI do Windows Server
Pré-requisitos para estas instruções:

-   Em cada servidor de arquivos onde você executa o Gerenciador de Recursos de Arquivo com a infraestrutura de classificação de arquivos:

    -   Você instalou o Gerenciador de Recursos do Servidor de Arquivos como um dos serviços de função para a função Serviços de Arquivo.

    -   Você identificou uma pasta local que contém os arquivos a serem protegidos com o Rights Management. Por exemplo, C:\FileShare.

    -   Você instalou a ferramenta de Proteção por RMS, incluindo os pré-requisitos da ferramenta (como o cliente RMS) e para o Azure RMS (como a conta de entidade de serviço). Para obter mais informações, consulte [Cmdlets de proteção do RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Se você quiser alterar o nível padrão de proteção por RMS (nativa ou genérica) para extensões de nome de arquivo específico, você editou o Registro conforme descrito na página [Configuração da API de arquivo](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx).

    -   Você tem uma conexão com a Internet, com configurações de computador configurado se necessário para um servidor proxy. Por exemplo: `netsh winhttp import proxy source=ie`

-   Você configurou os pré-requisitos adicionais para sua implantação do Azure Rights Management, conforme descrito em [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). Especificamente, você tem os seguintes valores para se conectar ao Azure RMS usando uma entidade de serviço:

    -   BposTenantId

    -   AppPrincipalId

    -   Chave simétrica

-   Você sincronizou suas contas de usuário do Active Directory local com o Active Directory do Azure ou o Office 365, incluindo seu endereço de email. Isso é necessário para todos os usuários que talvez precisem acessar arquivos depois que eles foram protegidos pelo FCI e pelo Azure RMS. Se você não executar essa etapa (por exemplo, em um ambiente de teste), os usuários poderão ser impedidos de acessar esses arquivos. Se precisar de mais informações sobre essa configuração de conta, consulte [Preparando o Azure Rights Management](../plan-design/prepare.md).

-   Identificar o modelo do Rights Management para uso, o qual protegerá os arquivos. Certifique-se de que você saiba a ID desse modelo usando o [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) cmdlet.

## Instruções para configurar o Gerenciador de Recursos do Servidor de Arquivos FCI para proteção do Azure RMS
Siga estas instruções para proteger automaticamente todos os arquivos em uma pasta, usando um script do Windows PowerShell como uma tarefa personalizada. Siga estes procedimentos nesta ordem:

1.  Salvar o script do Windows PowerShell

2.  Criar uma propriedade de classificação para o Rights Management (RMS)

3.  Criar uma regra de classificação (Classificar para RMS)

4.  Configurar o agendamento da classificação

5.  Criar uma tarefa de gerenciamento de arquivos personalizada (Proteger arquivos com o RMS)

6.  Testar a configuração executando manualmente a regra e a tarefa

No final destas instruções, todos os arquivos na pasta selecionada serão classificados com a propriedade personalizada do RMS e esses arquivos, em seguida, estarão protegidos pelo Rights Management. Para uma configuração mais complexa que seletivamente protege alguns arquivos e outros não, você pode criar ou usar uma propriedade de classificação e uma regra diferente, com uma tarefa de gerenciamento de arquivos que protege apenas aqueles arquivos.

### Salvar o script do Windows PowerShell

1.  Copie o conteúdo do [script do Windows PowerShell](fci-script.md) para proteção do Azure RMS usando o Gerenciador de Recursos de Servidor de Arquivos. Cole o conteúdo do script e nomeie o arquivo **RMS-Protect-FCI.ps1** no seu próprio computador.

2.  Examine o script e faça as seguintes alterações:

    -   Pesquisar a seguinte cadeia de caracteres e substituí-la com seu próprio AppPrincipalId que você usa com o [conjunto RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet para se conectar ao Azure RMS:

        ```
        <enter your AppPrincipalId here>
        ```
        Por exemplo, o script pode parecer com isso:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Pesquisar a seguinte cadeia de caracteres e substituí-la com a sua própria chave simétrica que você usa com o [conjunto RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet para se conectar ao Azure RMS:

        ```
        <enter your key here>
        ```
        Por exemplo, o script pode parecer com isso:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Pesquisar a seguinte cadeia de caracteres e substituí-la com seu próprio BposTenantId (Id do Locatário) que você usa com o [conjunto RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) cmdlet para se conectar ao Azure RMS:

        ```
        <enter your BposTenantId here>
        ```
        Por exemplo, o script pode parecer com isso:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Se o servidor estiver executando o Windows Server 2012, você talvez precise carregar manualmente o módulo RMSProtection no início do script. Adicione o seguinte comando (ou equivalente, se a pasta "Arquivos de programas" estiver em uma unidade diferente da unidade C:

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Assinar o script. Se você não assinar o script (mais seguro), você deve configurar o Windows PowerShell nos servidores que o executam. Por exemplo, inicie uma sessão do Windows PowerShell com a opção **Executar como Administrador** e, em seguida, digite: **Set-ExecutionPolicy Unrestricted**. No entanto, essa configuração permite que todos os scripts não assinados sejam executados (menos seguro).

    Para mais informações sobre a assinatura de scripts do Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) na biblioteca de documentação do PowerShell.

4.  Salve o arquivo localmente em cada servidor que executará o Gerenciador de Recursos de Arquivo com a infraestrutura de classificação de arquivos. Por exemplo, salve o arquivo em **C:\RMS-Protection**. Proteja esse arquivo usando as permissões NTFS para que usuários não autorizados não possam modificá-lo.

Agora você está pronto para começar a configurar o Gerenciador de Recursos do Servidor de Arquivos.

### Criar uma propriedade de classificação para o Rights Management (RMS)

-   No Gerenciador de Recursos do Servidor de Arquivos, Gerenciamento de Classificação, crie uma nova propriedade local:

    -   **Nome**: Tipo **RMS**

    -   **Descrição**:   Tipo **proteção por Rights Management**

    -   **Tipo de propriedade**: selecione **Sim/Não**

    -   **Valor**: Selecione **Sim**

Agora podemos criar uma regra de classificação que usa essa propriedade.

### Criar uma regra de classificação (Classificar para RMS)

-   Crie uma nova regra de classificação:

    -   Na guia **Geral** :

        -   **Nome**: Tipo **Classificar para RMS**

        -   **Habilitado**: Mantenha o padrão, que é essa caixa de seleção estar selecionada.

        -   **Descrição**: tipo **Classificar todos os arquivos em &lt;nome da pasta&gt; para o Rights Management**.

            Substitua *&lt;nome da pasta&gt;* pelo nome da pasta escolhida. Por exemplo, **classifique todos os arquivos na pasta C:\FileShare para Rights Management**

        -   **Escopo**: Adicione a sua pasta escolhida. Por exemplo, **C:\FileShare**.

            Não marque as caixas de seleção.

    -   Na guia **classificação** :

    -   **Método de classificação**: Selecione **Classificador de Pasta**

    -   **Property** : Selecione **RMS**

    -   Valor da **propriedade**: Selecione **Sim**.

Embora você possa executar as regras de classificação manualmente, para operações contínuas, você desejará que esta regra seja executada em uma agenda para que os novos arquivos serão classificados com a propriedade do RMS.

### Configurar o agendamento da classificação

-   Na guia **Classificação Automática** :

    -   **Habilitar agendamento fixo**: Selecione essa caixa de seleção.

    -   Configure o agendamento para todas as regras de classificação a serem executadas, que inclui a nossa nova regra para classificar arquivos com a propriedade do RMS.

    -   **Permite classificação contínua para novos arquivos**: Selecione essa caixa de seleção para que os novos arquivos serão classificados.

    -   Opcional: Faça outras alterações desejadas, como configurar opções para relatórios e notificações.

Agora você concluiu a configuração de classificação, você estará pronto para configurar uma tarefa de gerenciamento para aplicar a proteção de RMS para os arquivos.

### Criar uma tarefa de gerenciamento de arquivos personalizada (Proteger arquivos com o RMS)

-   Em **Tarefas de Gerenciamento de Arquivos**, crie uma nova tarefa de gerenciamento de arquivo:

    -   Na guia **Geral** :

        -   **Nome da tarefa**: Tipo **Proteger arquivos com o RMS**

        -   Manter a caixa de seleção **Habilitar** selecionada.

        -   **Descrição**: tipo **Proteger arquivos em &lt;nome da pasta&gt; com Rights Management e um modelo usando um script do Windows PowerShell.**

            Substitua *&lt;nome da pasta&gt;* pelo nome da pasta escolhida. Por exemplo, **proteger arquivos em C:\FileShare com Rights Management e um modelo usando um script do Windows PowerShell**

        -   **Escopo**: Selecione a sua pasta escolhida. Por exemplo, **C:\FileShare**.

            Não marque as caixas de seleção.

    -   Na guia **Ação** :

        -   **Tipo**: Selecionar **Personalizado**

        -   **Executável**: Especifique o seguinte:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Se o Windows não estiver na unidade C:, modifique esse caminho ou navegue até o arquivo.

        -   **Argumento**: especifique o seguinte, fornecendo seus próprios valores para &lt;caminho&gt; e &lt;ID do modelo&gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Por exemplo, se você copiou o script para C:\RMS-Protection e a ID do modelo identificado dos pré-requisitos é e6ee2481-26b9-45e5-b34a-f744eacd53b0, especifique o seguinte:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            Neste comando, as variáveis **[Caminho do Arquivo de Origem]** e **[Email do Proprietário do Arquivo de Origem]** são ambas específicas da FCI. Sendo assim, digite-as exatamente como aparecem no comando acima. O primeiro é usado por FCI para especificar o arquivo identificado automaticamente na pasta e o segundo é para FCI recuperar automaticamente o endereço de e-mail do Proprietário do arquivo identificado. Esse comando é repetido para cada arquivo na pasta, que, em nosso exemplo, é cada arquivo na pasta C:\FileShare que além disso, tem o RMS como uma propriedade de classificação do arquivo.

            > [!NOTE]
            > O parâmetro e valor **-OwnerMail [email do proprietário do arquivo de origem]** garantem que o proprietário original do arquivo receba o status de proprietário de Rights Management do arquivo depois que este estiver protegido. Isso garante que o dono do arquivo original terá todos os direitos de Rights Management de seus próprios arquivos. Quando arquivos são criados por um usuário de domínio, o endereço de email é recuperado automaticamente do Active Directory usando o nome de conta de usuário na propriedade do proprietário do arquivo. Para fazer isso, o servidor de arquivo deverá estar no mesmo domínio ou domínio confiável que o usuário.
            > 
            > Sempre que possível, atribua os proprietários originais para documentos protegidos, para garantir que esses usuários continuem a ter controle total sobre os arquivos que criaram. No entanto, se você usar a variável [Email do Proprietário do Arquivo de Origem], como acima, e um arquivo não tiver um usuário de domínio definido como o proprietário (por exemplo, uma conta local foi usada para criar o arquivo, assim o proprietário exibe SYSTEM), o script falhará.
            > 
            > Para arquivos que não possuem um usuário de domínio como proprietário, você pode copiar e salvar esses arquivos por conta própria como usuário de domínio, para que você se torne o proprietário para apenas esses arquivos. Ou, se tiver permissões, você poderá alterar o proprietário manualmente.  Ou, como alternativa, você poderá fornecer um endereço de email específico (como o seu próprio ou um endereço de grupo para o departamento de TI) em vez da variável [Email do Proprietário do Arquivo de Origem], o que significa que todos os arquivos que você proteger usando esse email usarão esse endereço de email para definir o novo proprietário.

    -   **Execute o comando como**: Selecione **Sistema Local**

    -   Na guia **Condição** :

        -   **Property**: Selecione **RMS**

        -   **Operador**: Selecione **Igual**

        -   **Valor**: Selecione **Sim**

    -   Na guia **Agenda** .

        -   **Executar em**: Configure a agenda desejada.

            Permitir bastante tempo para concluir o script. Embora essa solução proteja todos os arquivos na pasta, o script é executado uma vez para cada arquivo, cada vez. Embora isso demore mais do que proteger todos os arquivos ao mesmo tempo, o que é suportado pela ferramenta de proteção RMS, essa configuração de arquivo por arquivo para FCI é mais eficiente. Por exemplo, os arquivos protegidos podem ter proprietários diferentes (manter o proprietário original) quando você usar a variável [Email do Proprietário do Arquivo de Origem], e esta ação de arquivo por arquivo será necessária se você alterar posteriormente a configuração para proteger seletivamente arquivos em vez de todos os arquivos em uma pasta.

        -   **Executar continuamente nos novos arquivos**: Selecione essa caixa de seleção.

### Testar a configuração executando manualmente a regra e a tarefa

1.  Executar a regra de classificação:

    1.  Clique em **Regras de Classificação** &gt; **Executar Classificação com Todas as Regras Agora**

    2.  Clique em **Aguardar a conclusão da classificação**, e, em seguida, clique em **OK**.

2.  Aguarde até que a caixa de diálogo **Executando Classificação** feche e, em seguida, veja os resultados no relatório exibido automaticamente. Você deve ver **1** para o campo **Propriedades** e o número de arquivos na pasta. Confirme usando o Explorador de Arquivos e verificando as propriedades de arquivos na pasta escolhida. Na guia **Classificação**, você deve ver **RMS** como um nome de propriedade e **Sim** como seu **Valor**.

3.  Execute a tarefa de gerenciamento de arquivos:

    1.  Clique em **Tarefas de Gerenciamento de Arquivos** &gt; **Proteger arquivos com o RMS** &gt; **Executar Tarefa de Gerenciamento de Arquivos Agora**

    2.  Clique em **Aguardar a conclusão da tarefa**, e, em seguida, clique em **OK**.

4.  Aguarde até que a caixa de diálogo **Executando Tarefa de Gerenciamento de Arquivo** feche e, em seguida, veja os resultados no relatório exibido automaticamente. Você deve ver o número de arquivos que estão na pasta escolhida no campo **Arquivos** . Confirme que os arquivos na pasta escolhida estão agora protegidos pelo RMS. Por exemplo, se sua pasta escolhida for C:\FileShare, digite o seguinte em uma sessão do Windows PowerShell e assegure que nenhum arquivo tem o status **Desprotegido**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Algumas dicas de Solução de problemas:
    > 
    > -   Se você vir **0** no relatório, em vez do número de arquivos na pasta, isso indica que o script não foi executado. Primeiro, verifique o script propriamente dito, carregndo-o no ISE do Windows PowerShell para validar o conteúdo do script e tente executá-lo para ver se algum erro é exibido. Sem argumentos especificados, o script tentará se conectar e autenticar para o Azure RMS.
    > 
    >     -   Se o script reporta que ele não pôde se conectar ao Azure RMS, verifique os valores exibidos na conta de entidade de serviço, que você especificou no script.  Para obter mais informações sobre como criar essa conta de entidade de serviço, consulte o segundo pré-requisito no [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)
    >     -   Se o script reportar que ele pode se conectar ao Azure RMS, em seguida, verifique que ele pode encontrar o modelo especificado, executando [Get-RMSTemplate](https://msdn.microsoft.com/library/mt433197.aspx) diretamente do Windows PowerShell no servidor. Você deverá ver o modelo especificado retornar nos resultados.
    > -   Se o script por si só é executado no Windows PowerShell ISE sem erros, tente executá-lo da seguinte maneira de uma sessão do PowerShell, especificando um nome de arquivo para proteger e sem o parâmetro - OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Se o script for executado com êxito nesta sessão do Windows PowerShell, verifique as entradas para **Executivo** e **Argumento** na ação de tarefas de gerenciamento de arquivo.  Se você tiver especificado **-OwnerEmail [email do proprietário do arquivo de origem]**, tente remover esse parâmetro.
    > 
    >         Se a tarefa de gerenciamento de arquivo funcionar com êxito sem o **-OwnerEmail [Email do proprietário do arquivo de origem]**, verifique se os arquivos desprotegidos têm um usuário de domínio listado como o proprietário do arquivo, em vez de **SYSTEM**.  Para fazer isso, use a guia **Segurança** para as propriedades do arquivo e clique em **Avançado**. O valor de **Proprietário** é exibido imediatamente após o **Nome** do arquivo. Além disso, verifique se o servidor de arquivos está no mesmo domínio ou em um domínio confiável para pesquisar o endereço de email do usuário dos Serviços de Domínio do Active Directory.
    > -   Se você vir o número correto de arquivos no relatório, mas os arquivos não estão protegidos, tente proteger os arquivos manualmente usando o cmdlet [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) , para ver se algum erro é exibido.

Quando tiver confirmado que essas tarefas foram executadas com êxito, você poderá fechar o Gerenciador de recursos de arquivo. Os novos arquivos serão automaticamente protegidos e todos os arquivos serão protegidos novamente quando a agenda for executada. Proteger os arquivos novamente garante que quaisquer alterações no modelo serão aplicadas nos arquivos.


## Modificando as instruções para proteger os arquivos de forma seletiva
Quando você tiver as instruções anteriores trabalhando, é então muito fácil modificá-los para uma configuração mais sofisticada. Por exemplo, proteger os arquivos usando o mesmo script, mas apenas para arquivos que contêm Informações de Identificação Pessoal e, talvez, selecione um modelo que tenha direitos mais restritivos.

Para fazer isso, use uma das propriedades internas de classificação (por exemplo, **Informações de Identificação Pessoal**) ou crie uma nova propriedade de sua própria autoria. Em seguida, crie uma nova regra que usa essa propriedade. Por exemplo, você pode selecionar o **Classificador de Conteúdo**, escolher a propriedade **Informações de Identificação Pessoal** com um valor de **Alto**, e configurar o padrão de cadeia de caracteres ou expressão que identifica o arquivo a ser configurado para essa propriedade (como a cadeia de caracteres “**Data de nascimento**”)").

Agora tudo o que você precisa fazer é criar uma nova tarefa de gerenciamento de arquivo que usa o mesmo script mas talvez com um modelo diferente e configure a condição para a propriedade de classificação que você configurou. Por exemplo, em vez da condição que configuramos anteriormente (propriedade **RMS**, **Igual**, **Sim**), selecione a propriedade **Informações de Identificação Pessoal** com o valor **Operador** definido como **Igual** e **Valor** **Alto**.



<!--HONumber=Apr16_HO4-->


