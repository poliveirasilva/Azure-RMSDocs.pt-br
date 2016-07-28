---
title: Guia do administrador do aplicativo de compartilhamento Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a58d50b33db95570b43fe1ec0f76bdf490ddd024
ms.openlocfilehash: 164df467632b38f179d1c1192835f919641331a5


---


# Guia do administrador do aplicativo de compartilhamento Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*


Use as seguintes informações se você for responsável pelo aplicativo de compartilhamento Microsoft Rights Management em uma rede corporativa, ou se você quiser obter mais informações técnicas do que há no [Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md) ou [perguntas frequentes para aplicativo de compartilhamento Microsoft Rights Management para Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

O aplicativo de RMS sharing é ideal para trabalhar com o Azure RMS, porque essa configuração de implantação oferece suporte ao envio de anexos protegidos aos usuários de outra organização, e opções como notificações por email e controle de documento com revogação.  No entanto, com algumas limitações, também funciona com a versão local, AD RMS. Para obter uma comparação abrangente dos recursos que têm suporte pelo Azure RMS e pelo AD RMS, consulte [Comparando o Azure Rights Management e o AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). Se você tiver o AD RMS e desejar migrar para o Azure RMS, consulte [Migrando do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

Para obter uma visão geral técnica do aplicativo de compartilhamento Rights Management, informações sobre proteção nativa e genérica e os tipos de arquivo com suporte, extensões de nome de arquivo e como alterar o nível de proteção padrão, consulte [Technical overview and protection details for the Rights Management sharing application](sharing-app-admin-guide-technical.md) (Visão geral técnica e detalhes da proteção do aplicativo de compartilhamento Rights Management). 

## Implantação automática para o aplicativo de compartilhamento Microsoft Rights Management
A versão do Windows do aplicativo de RMS sharing oferece suporte a uma instalação com script, o que a torna adequada para implantações corporativas.

Os únicos pré-requisitos para as instalações são que os computadores executem uma versão mínima do Windows 7 Service Pack 1 e o Microsoft Framework, versão mínima 4.0 esteja instalada. Se você precisar instalar o Microsoft .NET Framework 4.0, você pode [baixá-lo para instalação do Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=17718).

### Para baixar o aplicativo RMS sharing para implantação automática

1.  Vá para a página do [aplicativo de compartilhamento Microsoft Rights Management para Windows](http://www.microsoft.com/download/details.aspx?id=40857) no Microsoft Download Center e clique em **Baixar**.

2.  Selecione e baixe os arquivos que você precisa. Existem dois pacotes de instalação de cliente: um para Windows de 64 bits (Microsoft Rights Management sharing application x64.zip) e outro para Windows de 32 bits (Microsoft Rights Management sharing application x86.zip).

3.  Extraia os arquivos dos pacotes de instalação compactados, por exemplo, ao clicar duas vezes neles. Depois, copie os arquivos extraídos para um local de rede que os computadores cliente possam acessar.

Os pacotes de instalação para o aplicativo de RMS sharing oferece suporte a diferentes cenários de implantação e inclui o seguinte:

|Descrição|Cenário de implantação|
|---------------|-----------------------|
|Assistente de Conexão do Microsoft Online|Office 2010 e Azure RMS<br /><br />Office 2013 e Azure RMS se você não tiver instalado a [atualização para o Office 2013 de 9 de junho de 2015](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Hotfix para Office (KB 2596501)|Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS|
|Hotfix para habilitar o cliente AD RMS 1.0 para trabalhar com o Azure RMS (2843630 KB)|Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS|
|Cliente AD RMS e o aplicativo RMS sharing|Office 2016 ou Office 2013 e Azure RMS ou Active Directory RMS<br /><br />Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS<br /><br />Apenas o aplicativo RMS sharing e suplemento do Office|
|Suplemento do Office para a faixa de opções|Office 2016 ou Office 2013 e Azure RMS ou Active Directory RMS<br /><br />Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS<br /><br />Apenas o aplicativo RMS sharing e suplemento do Office|
|Ferramenta de Preparação do Rights Management do Active Directory do Azure|Office 2010 e Azure RMS|
Use os procedimentos a seguir para identificar os comandos necessários para implantar o aplicativo RMS sharing para esses cenários de implantação:

-   **Office 2016 ou Office 2013 e Azure RMS ou Active Directory RMS**

    Seus usuários estão executando o Office 2016 ou Office 2013, sua organização usa o Azure RMS ou o Active Directory RMS e os usuários colaboram com outras organizações que usam o Azure RMS ou Active Directory RMS.

-   **Office 2010 e Azure RMS**

    Seus usuários estão executando o Office 2010, sua organização usa o Azure RMS, e os usuários colaboram com outras organizações que usam o Azure RMS ou Active Directory RMS.

-   **Office 2010 e Active Directory RMS**

    Seus usuários estão executando o Office 2010, sua organização usa o AD RMS, e os usuários colaboram com outras organizações que usam o Azure RMS.

-   **Apenas o aplicativo RMS sharing e suplemento do Office**

    Seus usuários estão executando o Office 2016, Office 2013 ou o Office 2010, sua organização usa o AD RMS, e os usuários não precisam colaborar com outras organizações que usam o Azure RMS. Essa instalação permite que você instale apenas o aplicativo de compartilhamento e o suplemento do Office.

> [!NOTE]
> Nesses cenários, se a sua organização está executando o AD RMS, seus usuários poderão receber conteúdo protegido de outras organizações que usam o Azure RMS, mas os seus usuários não podem enviar conteúdos protegidos aos usuários em uma organização que usa o Azure RMS. No entanto, se sua organização estiver executando o Azure RMS, os seus usuários podem enviar e receber conteúdo protegido de outras organizações.

Para concluir a instalação para cada procedimento, o computador deve ser reiniciado. Você pode iniciar uma reinicialização automática usando um comando como **shutdown /i**.

### Para implantar o aplicativo RMS sharing para Office 2016 ou o Office 2013 e o Azure RMS ou Active Directory RMS

-   Em cada computador no qual você deseja instalar o aplicativo RMS sharing e componentes relacionados, execute o seguinte comando com privilégios elevados:

    ```
    setup.exe /s
    ```

Para verificar o sucesso, consulte a seção [Verificando o sucesso da instalação](#verifying-installation-success) neste artigo.

### Para implantar o aplicativo RMS sharing para Office 2010 e o Azure RMS

1.  Você deve ser o administrador global para seu locatário Office 365 ou Azure Active Directory para que você possa obter a URL do serviço de certificação da sua organização, executando a ferramenta de preparação do Azure Active Directory Rights Management. Você precisa executar essa ferramenta apenas uma vez em um único computador. Você usará a URL do serviço de certificação em cada computador em que instalar o aplicativo de RMS sharing:

    1.  Fazer logon em um computador usando uma conta de administrador local.

    2.  Nesse computador, [baixe e instale o Assistente de conexão Microsoft Online](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Execute o seguinte comando para ver exibida na tela a URL de serviço de certificação, que você pode copiar e salvar para a próxima etapa:

        -   Para Windows 8.1 e Windows 8, 64 bits:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para Windows 8.1 e Windows 8, 32 bits:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para o Windows 7 de 64 bits:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Esse comando pode solicitar que você insira suas credenciais do Azure. Se o computador não tiver ingressado em um domínio, você será solicitado. Se o computador tiver ingressado em um domínio, a ferramenta poderá usar credenciais armazenadas em cache.

2.  Em cada computador no qual você instalará o aplicativo RMS sharing, execute o seguinte comando uma vez com privilégios elevados:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  Em cada computador no qual você instalará o aplicativo RMS sharing, cada usuário nesse computador deve executar o seguinte comando (não necessita de privilégios elevados). Há diferentes maneiras de alcançar isso, incluindo pedir aos usuários para executar o comando (por exemplo, um link em uma mensagem de email ou um link no portal help desk) ou você pode adicioná-lo para o script de logon:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Para verificar o sucesso, consulte a seção [Verificando o sucesso da instalação](#verifying-installation-success) neste artigo.

### Para implantar o aplicativo RMS sharing para Office 2010 e o Active Directory RMS

1.  Em cada computador no qual você deseja instalar o aplicativo RMS sharing, execute o seguinte comando com privilégios elevados:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  Em cada computador no qual você deseja instalar o aplicativo RMS sharing, os usuários devem executar o seguinte comando (não necessita de privilégios elevados). Há diferentes maneiras de alcançar isso, incluindo pedir aos usuários para executar o comando (por exemplo, um link em uma mensagem de email ou um link no portal help desk) ou você pode adicioná-lo para o script de logon:

    -   Para Windows 10, Windows 8.1 e Windows 8, 64 bits:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Para Windows 10, Windows 8.1 e Windows 8, 32 bits:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Para o Windows 7 de 64 bits:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

Para verificar o sucesso, consulte a seção [Verificando o sucesso da instalação](#verifying-installation-success) neste artigo.

### Para instalar apenas o aplicativo RMS sharing e suplemento do Office

1.  Instale o cliente AD RMS e o aplicativo RMS sharing usando o seguinte comando:

    -   Para Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Para Windows de 32 bits:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Por exemplo: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Instale o suplemento do Office usando os seguintes comandos:

    -   Para as versões de 64 bits do Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Para as versões de 32 bits do Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    Por exemplo: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

Para verificar o sucesso, consulte a seção [Verificando o sucesso da instalação](#verifying-installation-success) neste artigo.

## Verificando o sucesso da instalação
Você pode usar os arquivos de log da instalação para verificar uma instalação bem-sucedida.

### Para verificar o sucesso da instalação para o aplicativo RMS sharing para Office 2016 ou o Office 2013 e o Azure RMS ou Active Directory RMS

-   Para verificar o sucesso do comando Setup.exe, em cada computador, procure o arquivo de log da instalação **RMInstaller.log** na pasta *%temp%\RMS_installer_&lt;guid&gt;* e identifique o código de saída.

    Uma instalação bem sucedida tem o código de saída 0 e qualquer outro número indica uma falha na instalação.

    Exemplo de nome do arquivo de log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### Para verificar o sucesso da instalação para o aplicativo RMS sharing para Office 2010 e Azure RMS

1.  Para verificar o sucesso do comando Setup.exe, em cada computador, procure o arquivo de log da instalação **RMInstaller.log** na pasta *%temp%\RMS_installer_&lt;guid&gt;* e identifique o código de saída.

    Uma instalação bem sucedida tem o código de saída 0 e qualquer outro número indica uma falha na instalação.

    Exemplo de nome do arquivo de log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para verificar o sucesso do comando RMSSetup.exe, o usuário deve ter os seguintes arquivos criados na sua pasta *%localappdata%\microsoft\drm*:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    Exemplo de um arquivoCLC-&#42;.drm:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### Para verificar o sucesso da instalação para o aplicativo RMS sharing para Office 2010 e Active Directory RMS

1.  Para verificar o sucesso do comando Setup.exe, em cada computador, procure o arquivo de log da instalação na pasta *%temp%\RMS_installer_&lt;guid&gt;* e identifique o código de saída.

    Uma instalação bem sucedida tem o código de saída 0 e qualquer outro número indica uma falha na instalação.

    Exemplo de nome do arquivo de log: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para verificar o êxito do comando aadrmprep.exe, em cada computador, procure o seguinte texto no arquivo de log da instalação: **aadrmprep.exe foi encerrado com o status de SUCESSO**

    > [!NOTE]
    > Às vezes, a instalação pode executar duas vezes; a primeira ocorrência falhará e a segunda é bem-sucedida.

    Se você quiser verificar manualmente as alterações no registro realizadas por essa ferramenta, são os seguintes:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### Para verificar o sucesso da instalação apenas para o aplicativo RMS sharing e suplemento Office

1.  Para verificar o êxito do comando Setup_ipviewer.exe, pesquise pelo seguinte texto no arquivo de log da instalação: **Status de êxito ou erro de instalação: 0**

    Linhas de exemplo de uma instalação bem-sucedida:

    **MSI (s) (F0:B8) [14:19:57:854]: Produto: Active Directory Rights Management Services Client 2.1 - Instalação concluída com êxito.**

    **MSI (s) (F0:B8) [14:19:57:854]: O Windows Installer instalou o produto. Nome do Produto: Active Directory Rights Management Services Client 2.1. Versão do produto: 1.0.1179.1. Idioma do produto: 1033. Fabricante: Microsoft Corporation. Status de sucesso ou erro na instalação: 0.**

2.  Para verificar o êxito do suplemento do Office, pesquise cada computador pelo seguinte texto no arquivo de log da instalação: **Status de êxito ou erro de instalação: 0**

    Linhas de exemplo de uma instalação bem-sucedida:

    **MSI (s) (9C:88) [18:49:04:007]: Produto: Suplementos do Microsoft RMS Office - Instalação concluída com êxito.**

    **MSI (s) (9C:88) [18:49:04:007]: O Windows Installer instalou o produto. Nome do Produto: Suplementos do Microsoft Office RMS. Versão do produto: 1.0.7. Idioma do produto: 1033. Fabricante: Microsoft. Status de sucesso ou erro na instalação: 0.**

## Comandos de desinstalação
Nem todos os comandos de instalação que são necessários para essas implantações oferecem suporte a um comando de desinstalação. Você pode desinstalar o cliente AD RMS e o aplicativo de compartilhamento, e você pode desinstalar o suplemento do Office. Use os seguintes comandos para desinstalar esses elementos.

### Para desinstalar o Cliente AD RMS e o aplicativo RMS sharing

-   Use os seguintes comandos:

    -   Para Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Para Windows de 32 bits:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### Para desinstalar o suplemento do Office

-   Use os seguintes comandos:

    -   Para as versões de 64 bits do Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Para versões 32 bits do Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## Suprimindo atualizações automáticas
Como padrão, os usuários são notificados se houver uma versão posterior do aplicativo de compartilhamento do RMS e solicitados a baixá-lo. Você pode suprimir esta notificação fazendo a seguinte edição no registro:

1.  Navegue até **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e crie uma nova chave chamada **RmsSharingApp** se esta ainda não estiver presente.

2.  Selecione **RmsSharingApp**, crie um novo valor DWORD de **AllowUpdatePrompt**, e defina o valor como **0**.

Embora o aplicativo RMS sharing não seja suportado pelo WSUS, você pode usar a técnica a seguir para testar qualquer novas versões do aplicativo RMS sharing antes de implantá-lo em todos os usuários:

1.  Nos computadores de todos os usuários, execute um script para suprimir as atualizações automáticas. Nos computadores usados pelos administradores para testar as novas versões, não execute esse script.

2.  Quando uma nova versão estiver disponível, os administradores a baixarão e a testarão.

3.  Quando o teste for concluído e quaisquer problemas resolvidos, implante a versão mais recente para todos os usuários usando as instruções de implantação automática neste guia.

## Apenas Azure RMS: Configurando o controle de documentos
Se você tiver uma [assinatura que dê suporte ao rastreamento de documentos](https://technet.microsoft.com/dn858608), o site de rastreamento de documentos estará habilitado por padrão para todos os usuários em sua organização.  O controle de documento mostra informações como os endereços de email das pessoas que tentaram acessar documentos protegidos que os usuários compartilharam, quando essas pessoas tentavam acessá-los e sua localização. Se exibir essas informações for proibido em sua organização devido aos requisitos de privacidade, você poderá desabilitar o acesso ao site de rastreamento de documentos usando o cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). Você pode reabilitar o acesso ao site a qualquer momento usando [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), e você pode verificar se o acesso está habilitado ou desabilitado atualmente usando [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Para executar esses cmdlets, você deve ter pelo menos a versão **2.3.0.0** do módulo Azure RMS para Windows PowerShell.  Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Se você tiver baixado e instalado o módulo anteriormente, verifique o número da versão executando: `(Get-Module aadrm –ListAvailable).Version`

As seguintes URLs são usadas para controle de documentos e devem ser permitidas (por exemplo, adicioná-los aos seus Sites Confiáveis se você estiver usando o Internet Explorer com Segurança Reforçada):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > Esta URL é para o Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## Somente AD RMS: Suporte para vários domínios de email dentro de sua organização
Se você usa o AD RMS e usuários em sua organização tem vários domínios de email, talvez como resultado de uma fusão ou aquisição, você deve fazer a seguinte edição no registro:

1.  Navegue até **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e crie uma nova chave chamada **RmsSharingApp** se esta ainda não estiver presente.

2.  Selecione **RmsSharingApp**, crie um novo valor de cadeia múltipla de caracteres chamado **FederatedDomains**, e adicione os domínios e todos os subdomínios que sua organização usa. Não há suporte caracteres curinga.

    Por exemplo: a empresa Coho Vineyard &amp; Winery tem um domínio de email padrão de **cohovineyardandwinery.com**, mas devido a fusões, eles também usam os domínios de email **cohowinery.com**, **eastcoast.cohowinery.com**, e **cohovineyard**. Para o valor de dados **FederatedDomains**, o administrador insere: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

Se você não alterar esse registro, os usuários não poderão consumir conteúdo protegido por outros usuários em sua organização. Esta edição do registro não é necessária se você usar o Azure RMS.


## Próximas etapas
Para obter informações técnicas adicionais que incluem a explicação da diferença entre os níveis de proteção (nativa e genérica), os tipos de arquivo e extensões de nome do arquivo com suporte e como alterar o nível de proteção padrão, consulte [Visão geral técnica para o aplicativo de compartilhamento Rights Management](sharing-app-admin-guide-technical.md).




<!--HONumber=Jul16_HO3-->


