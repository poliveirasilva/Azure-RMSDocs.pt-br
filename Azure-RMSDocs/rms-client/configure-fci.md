---
# required metadata

title: Proteção RMS com Infraestrutura de Classificação de Ficheiros (FCI) do Windows Server | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
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

# Proteção RMS com Infraestrutura de Classificação de Ficheiros (FCI) do Windows Server

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Utilize este artigo para obter instruções e um script para utilizar o cliente de Rights Management (RMS) com a ferramenta RMS Protection para configurar o Gestor de Recursos do Servidor de Ficheiros e a infraestrutura de classificação de ficheiros (FCI).

Esta solução permite-lhe proteger automaticamente todos os ficheiros numa pasta num servidor de ficheiros com o Windows Server ou proteger automaticamente ficheiros que cumpram critérios específicos. Por exemplo, ficheiros que tenham sido classificados como contendo informações confidenciais. Esta solução utiliza o Azure Rights Management (Azure RMS) para proteger os ficheiros, pelo que esta tecnologia tem de estar implementada na sua organização.

> [!NOTE] Embora o Azure RMS inclua um [conector](../deploy-use/deploy-rms-connector.md) que suporta a infraestrutura de classificação de ficheiros, essa solução só suporta a proteção nativa — por exemplo, ficheiros do Office.
> 
> Para suportar todos os tipos de ficheiro com a infraestrutura de classificação de ficheiros, tem de utilizar o módulo **Proteção RMS** do Windows PowerShell, conforme documentado neste artigo. Os cmdlets da Proteção RMS, como a aplicação de partilha RMS, suportam a proteção genérica, bem como a proteção nativa, o que significa que todos os ficheiros podem ser protegidos. Para mais informações sobre estes níveis de proteção diferentes, consulte a secção [Níveis de proteção – nativa e genérica](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) no [Rights Management sharing application administrator guide (Guia do administrador da aplicação de partilha Rights Management – em inglês)](sharing-app-admin-guide.md).

As instruções que se seguem aplicam-se ao Windows Server 2012 R2 ou Windows Server 2012. Se utilizar outras versões suportadas do Windows, poderá ter de adaptar alguns dos passos devido às diferenças entre a versão do seu sistema operativo e a descrita neste artigo.

## Pré-requisitos para a proteção Azure RMS com a FCI do Windows Server
Pré-requisitos para estas instruções:

-   Nos servidores de ficheiros em que executará o Gestor de Recursos de Ficheiros com a infraestrutura de classificação de ficheiros:

    -   Instalou o Gestor de Recursos do Servidor de Ficheiros como um dos serviços de função para a função Serviços de Ficheiros.

    -   Identificou uma pasta local que contém ficheiros que pretende proteger com a Rights Management. Por exemplo, C:\FileShare.

    -   Instalou a ferramenta RMS Protection, incluindo os pré-requisitos da ferramenta (por exemplo, o cliente RMS) e do Azure RMS (por exemplo, a conta do principal de serviço). Para mais informações, consulte [Cmdlets da Proteção RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Se quiser alterar o nível predefinido da proteção RMS (nativo ou genérico) para extensões de nome de ficheiro específicas e tiver editado o registo, conforme descrito na página [File API configuration (Configuração da API de Ficheiros – em inglês)](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx).

    -   Tem uma ligação à Internet, com as definições de computador configuradas, se tal for necessário para um servidor proxy. Por exemplo: `netsh winhttp import proxy source=ie`

-   Configurou os pré-requisitos adicionais para a sua implementação do Azure Rights Management, conforme descrito em [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). Especificamente, tem os seguintes valores para ligar ao Azure RMS através de um principal de serviço:

    -   BposTenantId

    -   AppPrincipalId

    -   Symmetric key

-   Sincronizou as suas contas de utilizador do Active Directory no local com o Azure Active Directory ou o Office 365, incluindo os respetivos endereços de e-mail. Isto é necessário para todos os utilizadores que possam precisar de aceder a ficheiros depois de estarem protegidos pela FCI e o Azure RMS. Se não efetuar este passo (por exemplo, num ambiente de teste), os utilizadores poderão ficar bloqueados de aceder a estes ficheiros. Se precisar de mais informações sobre esta configuração de conta, consulte [Preparing for Azure Rights Management (Preparar para o Azure Rights Management – em inglês)](../plan-design/prepare.md).

-   Identificou o modelo de Rights Management a utilizar, o que irá proteger os ficheiros. Certifique-se de que sabe o ID deste modelo. Para esse efeito, utilize o cmdlet [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx).

## Instruções para configurar a FCI do Gestor de Recursos do Servidor de Ficheiros FCI para a proteção Azure RMS
Siga estas instruções para proteger automaticamente todos os ficheiros numa pasta, através de um script do Windows PowerShell como uma tarefa personalizada. Efetue estes procedimentos pela seguinte ordem:

1.  Guardar o script do Windows PowerShell

2.  Criar uma propriedade de classificação para a Rights Management (RMS)

3.  Criar uma regra de classificação (Classificar para RMS)

4.  Configurar a agenda de classificação

5.  Criar uma tarefa de gestão de ficheiros personalizada (Proteger ficheiros com o RMS)

6.  Testar a configuração ao executar manualmente a regra e a tarefa

No final destas instruções, todos os ficheiros na sua pasta selecionada serão classificados com a propriedade personalizada do RMS e estes ficheiros estarão assim protegidos pela Rights Management. Para uma configuração mais complexa que protege seletivamente alguns ficheiros e não outros, pode criar ou utilizar uma propriedade e regra de classificação diferente, com uma tarefa de gestão de ficheiros que protege apenas esses ficheiros.

### Guardar o script do Windows PowerShell

1.  Copie os conteúdos do [script do Windows PowerShell](fci-script.md) para a proteção Azure RMS através do Gestor de Recursos do Servidor de Ficheiros. Cole os conteúdos do script e atribua o nome **RMS-Protect-FCI.ps1** ao ficheiro no seu computador.

2.  Reveja o script e efetue as seguintes alterações:

    -   Procure a seguinte cadeia e substitua-a pelo seu AppPrincipalId, que utiliza com o cmdlet [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) para estabelecer ligação ao Azure RMS:

        ```
        <enter your AppPrincipalId here>
        ```
        Por exemplo, o script poderá ter o seguinte aspeto:

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Procure a seguinte cadeia e substitua-a pela sua chave simétrica, que utiliza com o cmdlet [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) para estabelecer ligação ao Azure RMS:

        ```
        <enter your key here>
        ```
        Por exemplo, o script poderá ter o seguinte aspeto:

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Procure a seguinte cadeia e substitua-a pelo seu BposTenantId (ID de inquilino), que utiliza com o cmdlet [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) para estabelecer ligação ao Azure RMS:

        ```
        <enter your BposTenantId here>
        ```
        Por exemplo, o script poderá ter o seguinte aspeto:

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Se o seu servidor utiliza o Windows Server 2012, poderá ter de carregar manualmente o módulo RMSProtection no início do script. Adicione o seguinte comando (ou equivalente, se a pasta "Programas" estiver numa unidade que não seja a unidade C:):

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Assine o script. Se não assinar o script (mais seguro), tem de configurar o Windows PowerShell nos servidores que o executam. Por exemplo, execute uma sessão do Windows PowerShell com a opção **Executar como Administrador** e escreva: **Set-ExecutionPolicy RemoteSigned**. No entanto, esta configuração permite executar todos os scripts não assinados quando estes estão armazenados neste servidor (menos seguro).

    Para mais informações sobre como assinar os scripts do Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) na biblioteca de documentação do PowerShell.

4.  Guarde o ficheiro localmente em cada um dos servidores de ficheiros que irão executar o Gestor de Recursos de Ficheiros com a infraestrutura de classificação de ficheiros. Por exemplo, guarde o ficheiro em **C:\RMS-Protection**. Proteja este ficheiro com permissões NTFS para que os utilizadores não autorizados não o possam modificar.

Agora está pronto para iniciar a configuração do Gestor de Recursos do Servidor de Ficheiros.

### Criar uma propriedade de classificação para a Rights Management (RMS)

-   No Gestor de Recursos do Servidor de Ficheiros, em Gestão de Classificação, crie uma nova propriedade local:

    -   **Nome**: escreva **RMS**

    -   **Descrição**:   escreva **Proteção da Rights Management**

    -   **Tipo de Propriedade**: selecione **Sim/Não**

    -   **Valor**: selecione **Sim**

Agora podemos criar uma regra de classificação que utiliza esta propriedade.

### Criar uma regra de classificação (Classificar para RMS)

-   Crie uma nova regra de classificação:

    -   No separador **Geral**:

        -   **Nome**: escreva **Classificar para RMS**

        -   **Ativado**: mantenha esta caixa de verificação selecionada, que é a predefinição.

        -   **Descrição**: escreva **Classificar todos os ficheiros na pasta &lt;nome da pasta&gt; para a Rights Management**.

            Substitua *&lt;nome da pasta&gt;* pelo nome da pasta que escolheu. Por exemplo, **Classificar todos os ficheiros na pasta C:\FileShare para a Rights Management**

        -   **Âmbito**: adicione a pasta escolhida. Por exemplo, **C:\FileShare**.

            Não selecione as caixas de verificação.

    -   Clique no separador **Classificação**:

    -   **Método de classificação**: selecione **Classificador de Pastas**

    -   Nome da **Propriedade**: selecione **RMS**

    -   Valor da **Propriedade**: selecione **Sim**

Pode executar as regras de classificação manualmente, mas para operações em curso é aconselhável agendar a execução desta regra, para que os novos ficheiros sejam classificados com a propriedade do RMS.

### Configurar a agenda de classificação

-   No separador **Classificação Automática**:

    -   **Ativar agenda fixa**: selecione esta caixa de verificação.

    -   Configure a agenda para todas as regras de classificação a executar, o que inclui a nossa nova regra para classificar ficheiros com a propriedade do RMS.

    -   **Permitir classificação contínua para novos ficheiros**: selecione esta caixa de verificação para classificar os novos ficheiros.

    -   Opcional: faça todas as alterações que quiser, como configurar as opções de relatórios e notificações.

Agora que concluiu a configuração de classificação, está pronto para configurar uma tarefa de gestão para aplicar a proteção RMS aos ficheiros.

### Criar uma tarefa de gestão de ficheiros personalizada (Proteger ficheiros com o RMS)

-   Em **Tarefas de Gestão de Ficheiros**, crie uma nova tarefa de gestão de ficheiros:

    -   No separador **Geral**:

        -   **Nome da tarefa**: escreva **Proteger ficheiros com RMS**

        -   Mantenha a caixa de verificação **Ativar** selecionada.

        -   **Descrição**: escreva **Proteger ficheiros em &lt;nome da pasta&gt; com a Rights Management e um modelo ao utilizar um script do Windows PowerShell.**

            Substitua *&lt;nome da pasta&gt;* pelo nome da pasta que escolheu. Por exemplo, **Proteger ficheiros em C:\FileShare com a Rights Management e um modelo ao utilizar um script do Windows PowerShell**

        -   **Âmbito**: selecione a pasta à sua escolha. Por exemplo, **C:\FileShare**.

            Não selecione as caixas de verificação.

    -   No separador **Ação**:

        -   **Tipo**: selecione **Personalizado**

        -   **Executável**: Especifique o seguinte:

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Se o Windows não estiver na sua unidade C:, modifique este caminho ou navegue até este ficheiro.

        -   **Argumento**: Especifique o seguinte, fornecendo os seus próprios valores para &lt;path&gt; e &lt;template ID&gt;:

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Por exemplo, se tiver copiado o script para C:\RMS-Protection e o ID de modelo que identificou a partir dos pré-requisitos for e6ee2481-26b9-45e5-b34a-f744eacd53b0, especifique o seguinte:

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            Neste comando, **[Source File Path]** e **[Source File Owner Email]** são ambas variáveis específicas da FCI, por isso escreva-as exatamente tal como aparecem no comando acima. A primeira é utilizada pela FCI para especificar automaticamente o ficheiro identificado na pasta e a segunda serve para que a FCI obtenha automaticamente o endereço de e-mail do Proprietário mencionado do ficheiro identificado. Este comando é repetido para cada ficheiro na pasta, o que, no nosso exemplo, significa cada ficheiro que se encontre na pasta C:\FileShare e tenha o RMS como uma propriedade de classificação de ficheiros.

            > [!NOTE]
            > O valor e o parâmetro **-OwnerMail [Source File Owner Email] (E-mail do Proprietário do Ficheiro de Origem)** garantem que os direitos de proprietário de Rights Management do ficheiro são concedidos ao proprietário original do ficheiro após este ser protegido. Isto garante que o proprietário do ficheiro original tem todos os direitos de Rights Management dos seus ficheiros. Quando os ficheiros são criados por um utilizador de domínio, o endereço de e-mail é obtido automaticamente a partir do Active Directory através do nome de conta de utilizador na propriedade Proprietário do ficheiro. Para fazer isto, o servidor de ficheiros tem de se encontrar no mesmo domínio ou domínio fidedigno que o utilizador.
            > 
            > Sempre que possível, atribua os proprietários originais aos documentos protegidos, para garantir que estes utilizadores continuam a ter controlo total sobre os ficheiros que criaram. No entanto, se utilizar a variável [Source File Owner Email] (E-mail do Proprietário do Ficheiro de Origem) conforme apresentado acima e um ficheiro não tiver um utilizador de domínio definido como o proprietário (por exemplo, se tiver sido utilizada uma conta local para criar o ficheiro e, por isso, o nome de proprietário apresentado for SYSTEM), o script irá falhar.
            > 
            > Para ficheiros que não dispõem de um utilizador de domínio como proprietário, pode copiar e guardá-los como um utilizador de domínio, de modo a ser o proprietário apenas destes ficheiros. Em alternativa, se tiver as permissões, pode alterar manualmente o proprietário.  Outra alternativa é fornecer um endereço de e-mail específico (tal como o seu próprio endereço ou um endereço de grupo do departamento de TI) em vez da variável [Source File Owner Email] (E-mail do Proprietário do Ficheiro de Origem), o que significa que todos os ficheiros que proteger com este script irão utilizar este endereço de e-mail para definir o novo proprietário.

    -   **Executar o comando como**: selecione **Sistema Local**

    -   No separador **Condição**:

        -   **Propriedade**: selecione **RMS**

        -   Em **Operador**, selecione **Igual**

        -   **Valor**: selecione **Sim**

    -   No separador **Agenda**:

        -   **Executar em**: configure o horário da sua preferência.

            Reserve bastante tempo para que o script seja concluído. Embora esta solução proteja todos os ficheiros na pasta, o script é executado uma vez para cada ficheiro, de cada vez. Apesar de este processo ser mais demorado do que proteger todos os ficheiros ao mesmo tempo, o que é suportado pela ferramenta RMS Protection, esta configuração ficheiro-a-ficheiro para a FCI é mais eficiente. Por exemplo, os ficheiros protegidos podem ter diferentes proprietários (manter o proprietário original) quando utiliza a variável [Source File Owner Email] (E-mail do Proprietário do Ficheiro de Origem) e esta ação ficheiro-a-ficheiro será necessária se posteriormente alterar a configuração para proteger ficheiros de forma seletiva, em vez de todos os ficheiros numa pasta.

        -   **Executar continuamente em ficheiros novos**: selecione esta caixa de verificação.

### Testar a configuração ao executar manualmente a regra e a tarefa

1.  Executar a regra de classificação:

    1.  Clique em **Regras de Classificação** &gt; **Executar Classificação Com Todas as Regras Agora**

    2.  Clique em **Aguardar conclusão da classificação** e, em seguida, clique em **OK**.

2.  Aguarde que a caixa de diálogo **A Executar Classificação** seja fechada e, em seguida, veja os resultados no relatório que é automaticamente apresentado. Deverá ver **1** no campo **Propriedades** e o número de ficheiros existentes na sua pasta. Utilize o Explorador de Ficheiros para confirmar e verificar as propriedades dos ficheiros na pasta escolhida. No separador **Classificação**, deverá ver **RMS** como um nome de propriedade e **Sim** para o respetivo **Valor**.

3.  Execute a tarefa de gestão de ficheiros:

    1.  Clique em **Tarefas de Gestão de Ficheiros** &gt; **Proteger os ficheiros com RMS** &gt; **Executar Ficheiro de Gestão de Tarefas Agora**

    2.  Clique em **Aguardar a conclusão da tarefa** e, em seguida, clique em **OK**.

4.  Aguarde que a caixa de diálogo **A Executar Tarefa de Gestão de Ficheiros** seja fechada e, em seguida, veja os resultados no relatório que é automaticamente apresentado. Deverá ver o número de ficheiros que estão na pasta selecionada no campo **Ficheiros**. Certifique-se de que os ficheiros na pasta escolhida estão agora protegidos pelo RMS. Por exemplo, se a pasta que escolheu for C:\FileShare, escreva o seguinte numa sessão do Windows PowerShell e confirme que não existem ficheiros com um estado **Desprotegido**:

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP] Algumas dicas para a resolução de problemas:
    > 
    > -   Se vir **0** no relatório, em vez do número de ficheiros na sua pasta, isto indica que o script não foi executado. Em primeiro lugar, verifique o próprio script ao carregá-lo no ISE do Windows PowerShell para validar os conteúdos do script e tente executá-lo para ver se são apresentados erros. Sem especificar argumentos, o script irá tentar estabelecer ligação e autenticar para o Azure RMS.
    > 
    >     -   Se o script anunciar que não foi possível ligar ao Azure RMS, verifique os valores que este apresenta para a conta do principal do serviço que especificou no script.  Para mais informações sobre como criar esta conta do principal de serviço, consulte o segundo pré-requisito em [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)
    >     -   Se o script anunciar que pode ligar ao Azure RMS, em seguida verifique se pode encontrar o modelo especificado ao executar [Get-RMSTemplate](https://msdn.microsoft.com/library/mt433197.aspx) diretamente a partir do Windows PowerShell no servidor. Deverá ver o modelo que especificou devolvido nos resultados.
    > -   Se o script for automaticamente executado no ISE do Windows PowerShell sem erros, tente executá-lo da seguinte maneira a partir de uma sessão do PowerShell, especificando um nome de ficheiro a proteger e sem o parâmetro -OwnerEmail:
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Se o script for executado com êxito nesta sessão do Windows PowerShell, verifique as suas entradas para **Executivo** e **Argumento** na ação de tarefa de gestão de ficheiros.  Se tiver especificado **-OwnerEmail [Source File Owner Email] (E-mail de Proprietário do Ficheiro de Origem)**, experimente remover este parâmetro.
    > 
    >         Se a tarefa de gestão de ficheiros funcionar com êxito sem **-OwnerEmail [Source File Owner Email] (E-mail de Proprietário do Ficheiro de Origem)**, verifique se os ficheiros não protegidos têm um utilizador de domínio listado como o proprietário do ficheiro, em vez de **SYSTEM**.  Para o fazer, utilize o separador **Segurança** nas propriedades do ficheiro e, em seguida, clique em **Avançadas**. O valor **Proprietário** é apresentado imediatamente a seguir ao **Nome** do ficheiro. Além disso, certifique-se de que o servidor de ficheiros está no mesmo domínio ou num domínio fidedigno para procurar o endereço de e-mail do utilizador a partir dos Serviços de Domínio do Active Directory.
    > -   Se vir o número correto de ficheiros no relatório, mas os ficheiros não estiverem protegidos, experimente proteger os ficheiros manualmente com o cmdlet [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx), para ver se são apresentados erros.

Após confirmar que estas tarefas foram executadas com êxito, pode fechar o Gestor de Recursos de Ficheiros. Os novos ficheiros serão protegidos automaticamente e todos os ficheiros serão protegidos novamente quando os agendamentos forem executados. Voltar a proteger os ficheiros garante que todas as alterações ao modelo são aplicadas aos ficheiros.


## Modificar as instruções para proteger ficheiros de forma seletiva
Quando tiver implementado as instruções anteriores, será muito fácil modificá-las para uma configuração mais complexa. Por exemplo, pode proteger ficheiros com o mesmo script, mas apenas para ficheiros que contenham informações pessoais, e talvez selecionar um modelo que possua direitos mais restritivos.

Para tal, utilize uma das propriedades de classificação incorporadas (por exemplo, **Informações Pessoais**) ou crie uma nova propriedade. Em seguida, crie uma nova regra que utilize esta propriedade. Por exemplo, poderá selecionar o **Classificador de Conteúdos**, selecionar a propriedade **Informações Pessoais** com o valor **Elevado** e configurar o padrão de expressão ou cadeia que identifica o ficheiro a ser configurado para esta propriedade (tais como a cadeia "**Data de Nascimento**").

Agora, tudo o que precisa de fazer é criar uma nova tarefa de gestão de ficheiros que utilize o mesmo script, mas talvez com um modelo diferente, e configurar a condição da propriedade de classificação que acabou de configurar. Por exemplo, em vez da condição que configurámos anteriormente (propriedade **RMS**, **Igual**, **Sim**), selecione a propriedade **Informações Pessoais** com o valor **Operador** definido como **Igual** e o **Valor** **Elevado**.



<!--HONumber=Jun16_HO2-->


