---
title: "Configuração de servidores para o conector do Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0b07ecc88b1d2d344f0984d4a805cc033996cc4d
ms.openlocfilehash: 79171b5931b69ca18d2a2cbe321d5d5887903da2


---

# Configuração de servidores para o conector do Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*


Use as informações a seguir para ajudá-lo a configurar os servidores locais que usarão o conector do Azure RMS (Azure Rights Management). Esses procedimentos abrangem a etapa 5 da [Implantação do conector do Azure Rights Management](deploy-rms-connector.md).

Antes de começar, certifique-se de que você instalou e configurou o conector RMS e verificou os [pré-requisitos](deploy-rms-connector.md#prerequisites-for-the-rms-connector) que são aplicáveis para os servidores que usam o conector.


## Configurando servidores para usar o conector RMS
Após ter instalado e configurado o conector RMS, você está pronto para configurar seus servidores locais que usam o Rights Management e se conectam ao Azure RMS usando o conector. Isso significa configurando os servidores a seguir:

-   **Para o Exchange 2016 e Exchange 2013**: servidores de acesso para cliente e servidores de caixa de correio

-   **Para o Exchange 2010**: servidores de acesso para clientes e servidores de transporte de hub

-   **Para o SharePoint**: servidores Web de front-end do SharePoint, incluindo aqueles hospedados no servidor de Administração Central

-   **Para a Infraestrutura de Classificação de Arquivos**: computadores com Windows Server com o Gerenciador de Recursos de Arquivos instalado

Esta configuração requer configurações de registro. Para fazer isso, você tem duas opções: automaticamente, usando a ferramenta de configuração do servidor para o conector Microsoft RMS, ou manualmente, editando o Registro.

---

**Automaticamente, usando a ferramenta de configuração do servidor para o conector Microsoft RMS:**

- Vantagens:

    - Sem edição direta do registro. Esse método é automatizado para você usando um script.

    - Não é necessário executar um cmdlet do Windows PowerShell para obter sua URL do Microsoft RMS.

    - Os pré-requisitos são verificados automaticamente (mas não corrigidos automaticamente) se você executá-los localmente.

Desvantagens:

- Ao executar a ferramenta, é necessário fazer uma conexão a um servidor que já esteja em execução no conector RMS.

---

**Manualmente, editando o Registro:**

- Vantagens:

    - Não é necessária uma conectividade a um servidor que execute o conector RMS.

- Desvantagens:

    - Mais despesas administrativas que são propensas a erros.

    - É necessário obter a URL do Microsoft RMS, o que exige que um comando do Windows PowerShell seja executado.

    - É necessário fazer sempre todas as verificações de pré-requisitos.


---

> [!IMPORTANT]
> Em ambos os casos, você deve manualmente instalar todos os pré-requisitos e configurar o Exchange, o SharePoint e a infraestrutura de classificação de arquivos para usar o Gerenciamento de Direitos.

Para a maioria das organizações, a configuração automática com a ferramenta de configuração do servidor para o conector do Microsoft RMS será a melhor opção, pois proporciona mais eficiência e confiabilidade do que a configuração manual.

Depois de fazer as alterações de configuração nos servidores, você deve reiniciá-los se eles estiverem executando o Exchange ou o SharePoint e previamente configurados para usar o AD RMS. Não é necessário reiniciar esses servidores, se você estiver configurando-os para o Gerenciamento de Direitos pela primeira vez. Você sempre deve reiniciar o servidor de arquivos que estiver configurado para usar a infraestrutura de classificação de arquivos depois de fazer essas alterações de configuração.

### Como usar a ferramenta de configuração do servidor para o conector Microsoft RMS

1.  Se você ainda não tiver baixado o script para a ferramenta de configuração do servidor do conector Microsoft RMS (GenConnectorConfig.ps1), baixe-o da [Central de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

2.  Salve o arquivo GenConnectorConfig.ps1 no computador em que a ferramenta será executada. Se você executar a ferramenta localmente, ela deve ser o servidor que você deseja configurar para se comunicar com o conector do RMS. Caso contrário, você poderá salvá-la em qualquer computador.

3.  Decida como executar a ferramenta:

    -   **Localmente**: Você pode executar a ferramenta interativamente, do servidor a ser configurado para se comunicar com o conector do RMS. Isso é útil para uma configuração única, como um ambiente de teste.

    -   **Implantação de Software**: Você pode executar a ferramenta para produzir arquivos de registro que você implanta em um ou mais servidores relevantes usando um aplicativo de gerenciamento de sistemas que oferece suporte à implantação de software, como o System Center Configuration Manager.

    -   **Política de Grupo**: você pode executar a ferramenta para produzir um script que será dada a um administrador que pode criar objetos de Política de Grupo para os servidores a serem configurados. Este script cria um objeto de Política de Grupo para cada tipo de servidor a ser configurado, que o administrador pode atribuir aos servidores relevantes.

    > [!NOTE]
    > Essa ferramenta configura os servidores que se comunicarão com o conector do RMS e que estão listados no começo desta seção. Não execute essa ferramenta em servidores que executam o conector do RMS.

4.  Inicie o Windows PowerShell com a opção **Executar como administrador** e use o comando Get-help para ler as instruções sobre como usar a ferramenta para seu método de configuração escolhido:

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Para executar o script, você deve inserir a URL do conector RMS de sua organização. Digite o prefixo de protocolo (HTTP:// ou HTTPS://) e o nome do conector que você definiu no DNS para o endereço de balanceamento de carga do seu conector. Por exemplo, https://connector.contoso.com. A ferramenta, então, usa essa URL em contato com os servidores que executam o conector RMS e obtém outros parâmetros que são usados ​​para criar as configurações necessárias.

> [!IMPORTANT]
> Quando você executar essa ferramenta, certifique-se de especificar o nome do conector do RMS com o balanceamento de carga para sua organização e não o nome de um único servidor que executa o serviço de conector do RMS.

Use as seguintes seções para obter informações específicas para cada tipo de serviço:

-   [Configurando um servidor Exchange para usar o conector](#configuring-an-exchange-server-to-use-the-connector)

-   [Configurando um servidor SharePoint para usar o conector](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configurando um servidor de arquivos para a Infraestrutura de Classificação de Arquivos usar o conector](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> Depois que um servidor for configurado para usar o conector, os aplicativos clientes que estiverem instalados localmente no servidor poderão não funcionar com o RMS. Isso acontece porque os aplicativos tentam usar o conector em vez de usar o RMS diretamente, o que não tem suporte.
>
> Além disso, se o Office 2010 for instalado localmente em um servidor Exchange, os recursos do IRM do aplicativo cliente poderão funcionar nesse computador depois que o servidor estiver configurado para usar o conector, mas isso não tem suporte.
>
> Nos dois casos, é preciso instalar os aplicativos cliente em computadores separados que não estejam configurados para usar o conector. Assim, eles usarão corretamente o RMS de maneira direta.

## Configurando um servidor Exchange para usar o conector
As seguintes funções do Exchange se comunicam com o conector do RMS:

-   Para o Exchange 2016 e Exchange 2013: servidores de acesso para cliente e servidores de caixa de correio

-   Para o Exchange 2010: Servidor de acesso para clientes e servidor de transporte de hub

Para usar o conector do RMS, esses servidores que executam o Exchange devem estar executando uma das seguintes versões do software:

-   Exchange Server 2016

-   Exchange Server 2013 com o Exchange 2013 Atualização Cumulativa 3

-   Exchange Server 2010 com o Exchange 2010 Service Pack 3 Atualização Cumulativa 6

Você também precisará instalar nestes servidores uma versão do cliente RMS que inclui suporte para o Modo Criptográfico do RMS 2. A versão mínima com suporte no Windows Server 2008 está incluída no hotfix que você pode baixar do [comprimento da chave RSA é aumentado para 2048 bits para AD RMS no Windows Server 2008 R2 e no Windows Server 2008](http://support.microsoft.com/kb/2627272). A versão mínima do Windows Server 2008 R2 pode ser baixada de [comprimento da chave RSA é aumentado para 2048 bits para AD RMS no Windows 7 ou no Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). O Windows Server 2012 e o Windows Server 2012 R2 suportam nativamente o Modo crptográfico 2.

> [!IMPORTANT]
> Se essas versões ou versões posteriores do Exchange e o cliente RMS não estiverem instalados, não será possível configurar o Exchange para usar o conector. Verifique se essas versões estão instaladas antes de continuar.

### Para configurar servidores Exchange para usar o conector

1. Certifique-se de que os servidores Exchange estão autorizados a usar o conector RMS, usando a ferramenta de administração do conector RMS e as informações da seção [Autorizando servidores para usar o conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Essa configuração é necessária para que o Exchange possa usar o conector RMS.

2.  Sobre as funções de servidor do Exchange que se comunicam com o conector do RMS, siga um destes procedimentos:

    -   Execute a ferramenta de configuração do servidor para o conector Microsoft RMS. Para obter mais informações, consulte [Como usar a ferramenta de configuração do servidor para o conector Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) neste artigo.

        Por exemplo, para executar a ferramenta localmente para configurar um servidor executando o Exchange 2016 ou Exchange 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   Faça edições de Registro manualmente usando as informações em [Configurações do Registro para o conector RMS](rms-connector-registry-settings.md) para adicionar manualmente as configurações do Registro nos servidores. 

3.  Habilite a funcionalidade do IRM no Exchange. Para obter mais informações, consulte [Procedimentos de Gerenciamento de Direitos de Informação](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) na biblioteca do Exchange.

    > [!NOTE]
    > Por padrão, após a execução de **Set-IRMConfiguration - InternalLicensingEnabled $true**, o IRM é habilitado automaticamente para o Outlook Web App e dispositivos móveis, e também para as caixas de correio. No entanto, os administradores podem desabilitar o IRM em níveis diferentes, por exemplo, para um servidor de Acesso para Cliente, para o diretório virtual do Outlook Web App ou a política de caixa de correio do Outlook Web App e para uma política de caixa de correio do dispositivo móvel. Se os usuários não puderem ver nenhum dos modelos do Azure RMS d no Outlook Web App (após aguardar um dia) ou em dispositivos móveis quando podem ver os modelos no cliente Outlook, verifique as configurações relevantes para verificar se o IRM não está desabilitado. Para obter mais informações, consulte [Habilitar ou desabilitar o Gerenciamento de Direitos de Informação nos servidores de acesso para cliente](https://technet.microsoft.com/library/dd876938(v=exchg.150).aspx) na documentação do Exchange. 


## Configurando um servidor SharePoint para usar o conector
As seguintes funções do SharePoint se comunicam com o conector do RMS:

-   Servidores Web de front-end do SharePoint, incluindo aqueles hospedados no servidor de Administração Central

Para usar o conector do RMS, esses servidores que executam o SharePoint devem estar executando uma das seguintes versões do software:

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

Um servidor que executa o SharePoint 2016 ou SharePoint 2013 também deve executar uma versão do cliente MSIPC 2.1 que tem suporte com o conector RMS. Para certificar-se de que você tem uma versão com suporte, baixe o cliente mais recente do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Existem várias versões do cliente MSIPC 2.1, então certifique-se de que você tem a versão 1.0.2004.0 ou posterior.
>
> É possível verificar a versão do cliente, verificando o número de versão do MSIPC.dll, que está localizado em **\Program Files\Active Directory Rights Management Services Client 2.1**. A caixa de diálogo de propriedades mostra o número de versão do cliente MSIPC 2.1.

Servidores que executam o SharePoint 2010 devem ter uma versão do cliente MSDRM instalada que inclui suporte para o modo criptográfico 2 do RMS. A versão mínima com suporte no Windows Server 2008 está incluída no hotfix que você pode baixar do [comprimento da chave RSA é aumentado para 2048 bits para AD RMS no Windows Server 2008 R2 e no Windows Server 2008](http://support.microsoft.com/kb/2627272)e a versão mínima do Windows Server 2008 R2 pode ser baixada em [comprimento da chave RSA é aumentado para 2048 bits para AD RMS no Windows 7 ou no Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). O Windows Server 2012 e o Windows Server 2012 R2 suportam nativamente o Modo crptográfico 2.

### Para configurar servidores SharePoint para usar o conector

1. Certifique-se de que os servidores SharePoint estão autorizados a usar o conector RMS, usando a ferramenta de administração do conector RMS e as informações da seção [Autorizando servidores para usar o conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Essa configuração é necessária para que o Exchange possa usar o conector RMS.

2.  Nos servidores do SharePoint que se comunicam com o conector do RMS, siga um destes procedimentos:

    -   Execute a ferramenta de configuração do servidor para o conector Microsoft RMS. Para obter mais informações, consulte [Como usar a ferramenta de configuração do servidor para o conector Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) neste artigo.

        Por exemplo, para executar a ferramenta localmente para configurar um servidor executando o SharePoint 2016 ou SharePoint 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   Se você estiver usando o SharePoint 2016 ou SharePoint 2013, faça edições de Registro manualmente usando as informações em [Configurações de Registro para o conector RMS](rms-connector-registry-settings.md) para adicionar manualmente as configurações do Registro nos servidores. 

3.  Habilite o IRM no SharePoint. Para obter mais informações, consulte [Configurar o Gerenciamento de Direitos de Informação (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) na biblioteca do SharePoint.

    Quando seguir estas instruções, você deverá configurar o SharePoint para usar o conector especificando **Usar este servidor RMS** e, em seguida, digite a URL do conector de balanceamento de carga que você configurou. Digite o prefixo de protocolo (HTTP:// ou HTTPS://) e o nome do conector que você definiu no DNS para o endereço de balanceamento de carga do seu conector. Por exemplo, se o nome do conector for https://connector.contoso.com, sua configuração ficará como a imagem a seguir:

    ![Configurando o SharePoint Server para o conector RMS](../media/AzRMS_SharePointConnector.png)

    Depois que o IRM é habilitado em um farm do SharePoint, você pode habilitar o IRM em bibliotecas individuais usando a opção **Gerenciamento de Direitos de Informação** na página **Definições da Biblioteca** para cada uma das bibliotecas.


## Configurando um servidor de arquivos para a Infraestrutura de Classificação de Arquivos usar o conector
Para usar o conector RMS e a infraestrutura de classificação de arquivos para proteger documentos do Office, o servidor de arquivos deve estar executando um dos seguintes sistemas operacionais:

-   Windows Server 2012 R2

-   Windows Server 2012

### Para configurar servidores de arquivo para usar o conector

1.  Certifique-se de que os servidores de arquivos estão autorizados a usar o conector RMS, usando a ferramenta de administração do conector RMS e as informações da seção [Autorizando servidores para usar o conector RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Essa configuração é necessária para que o Exchange possa usar o conector RMS.

2.  Nos servidores de arquivos configurados para a infraestrutura de classificação de arquivos e que se comunicarão com o conector do RMS, siga um destes procedimentos:

    -   Execute a ferramenta de configuração do servidor para o conector Microsoft RMS. Para obter mais informações, consulte [Como usar a ferramenta de configuração do servidor para o conector Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) neste artigo.

        Por exemplo, para executar a ferramenta localmente para configurar um servidor executando o FCI:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - Faça edições de Registro manualmente usando as informações em [Configurações do Registro para o conector RMS](rms-connector-registry-settings.md) para adicionar manualmente as configurações do Registro nos servidores. 

3.  Criar regras de classificação e tarefas de gerenciamento de arquivos para proteger documentos com a criptografia do RMS e, em seguida, especificar um modelo de RMS para aplicar automaticamente as políticas do RMS. Para obter mais informações, consulte [Visão Geral do Gerenciador de Recursos do Servidor de Arquivos](http://technet.microsoft.com/library/hh831701.aspx) na biblioteca de documentação do Windows Server.

## Próximas etapas
Agora que o conector RMS está instalado e configurado e que seus servidores estão configurados para usá-lo, os administradores de TI e os usuários podem proteger e consumir mensagens de email e documentos usando o Azure RMS. Para facilitar isso para os usuários, implante o aplicativo de compartilhamento do RMS, que instala um complemento do Office e adiciona novas opções de atalho para o Explorador de Arquivos. Para saber mais, confira o [Guia do administrador do aplicativo de compartilhamento do Rights Management](../rms-client/sharing-app-admin-guide.md).

Você pode usar o [Mapa de implantação do Azure Rights Management](../plan-design/deployment-roadmap.md) para verificar se existem outras etapas de configuração que você possa precisar executar antes de lançar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para os usuários e administradores.

Para monitorar o conector RMS, consulte [Monitor the Azure Rights Management connector](monitor-rms-connector.md) (Monitorar o conector do Azure Rights Management). 



<!--HONumber=Jun16_HO4-->


