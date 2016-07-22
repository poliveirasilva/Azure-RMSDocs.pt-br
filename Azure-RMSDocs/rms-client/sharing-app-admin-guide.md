---
title: "Guia do administrador da aplicação de partilha Rights Management|Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: e67d0ab5537aa7444940a5e7ce3a653cc6e66993


---


# Guia do administrador da aplicação de partilha Rights Management

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*


Utilize as seguintes informações se for o responsável pela aplicação de partilha Microsoft Rights Management numa rede empresarial ou se quiser obter mais informações técnicas além das que se encontram no [Guia do utilizador da aplicação de partilha Rights Management](sharing-app-user-guide.md) ou nas [FAQ sobre a Aplicação de Partilha Microsoft Rights Management do Windows](http://go.microsoft.com/fwlink/?LinkId=303971).

A aplicação de partilha RMS funciona melhor com o Azure RMS, porque esta configuração de implementação suporta o envio de anexos protegidos para utilizadores de outra organização e opções como notificações por e-mail e o controlo de documentos com revogação.  No entanto, a aplicação também funciona com a versão no local, o AD RMS, embora com algumas limitações. Para ver uma comparação detalhada das funcionalidades suportadas pelo Azure RMS e pelo AD RMS, consulte [Comparing Azure Rights Management and AD RMS (Comparação entre o Azure Rights Management e o AD RMS – em inglês)](../understand-explore/compare-azure-rms-ad-rms.md). Se tiver o AD RMS e quiser migrar para o Azure RMS, consulte [Migrar do AD RMS para o Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## Implementação automática da aplicação de partilha Microsoft Rights Management
A versão para Windows da aplicação de partilha RMS suporta uma instalação com script, o que a torna adequada para implementações empresariais.

Os únicos pré-requisitos de instalação são que os computadores consigam executar pelo menos o Windows 7 Service Pack 1 ou superior e que esteja instalada a versão 4.0 ou superior do Microsoft Framework. Se precisar de instalar o Microsoft .NET Framework 4.0, pode [transferi-lo no Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=17718).

### Para transferir a aplicação de partilha RMS para implementações automáticas

1.  Aceda à página da [aplicação de partilha Microsoft Rights Management para Windows](http://www.microsoft.com/download/details.aspx?id=40857) no Centro de Transferências da Microsoft e clique em **Transferir**.

2.  Selecione e transfira os ficheiros de que precisa. Existem dois pacotes de instalação de clientes: um para o Windows de 64 bits (Microsoft Rights Management sharing application x64.zip) e outro para o Windows de 32 bits (Microsoft Rights Management sharing application x86.zip).

3.  Pode extrair os ficheiros dos pacotes de instalação comprimidos ao fazer duplo clique sobre os mesmos, por exemplo. Em seguida, copie os ficheiros extraídos para uma localização na rede à qual os computadores cliente possam aceder.

Os pacotes de configuração para a aplicação de partilha RMS suportam diferentes cenários de implementação e incluem o seguinte:

|Descrição|Cenário de implementação|
|---------------|-----------------------|
|Assistente de Início de Sessão Online da Microsoft|Office 2010 e Azure RMS<br /><br />Office 2013 e Azure RMS se não tiver instalado a [atualização do Office 2013 de 9 de junho de 2015](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Correção para o Office (KB 2596501)|Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS|
|Correção para permitir que o AD RMS Client 1.0 funcione com o Azure RMS (KB 2843630)|Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS|
|Cliente de AD RMS e a aplicação de partilha RMS|Office 2016 ou 2013 e Azure RMS ou Active Directory RMS<br /><br />Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS<br /><br />Apenas a aplicação de partilha RMS e o suplemento do Office|
|Suplemento do Office para o friso|Office 2016 ou 2013 e Azure RMS ou Active Directory RMS<br /><br />Office 2010 e Azure RMS<br /><br />Office 2010 e Active Directory RMS<br /><br />Apenas a aplicação de partilha RMS e o suplemento do Office|
|Ferramenta de preparação do Azure Active Directory Rights Management|Office 2010 e Azure RMS|
Utilize os seguintes procedimentos para identificar os comandos necessários para implementar a aplicação de partilha RMS nestes cenários de implementação:

-   **Office 2016 ou 2013 e Azure RMS ou Active Directory RMS**

    Os seus utilizadores estão a utilizar o Office 2016 ou 2013, a sua organização utiliza o Azure RMS ou o Active Directory RMS e os utilizadores colaboram com outras organizações que utilizam o Azure RMS ou o Active Directory RMS.

-   **Office 2010 e Azure RMS**

    Os seus utilizadores estão a executar o Office 2010, a sua organização utiliza o Azure RMS e os utilizadores colaboram com outras organizações que utilizam o Azure RMS ou o Active Directory RMS.

-   **Office 2010 e Active Directory RMS**

    Os seus utilizadores estão a utilizar o Office 2010, a sua organização utiliza o AD RMS e os utilizadores colaboram com outras organizações que utilizam o Azure RMS.

-   **Apenas a aplicação de partilha RMS e o suplemento do Office**

    Os seus utilizadores estão a utilizar o Office 2016, o Office 2013 ou o Office 2010, a sua organização utiliza o AD RMS e os utilizadores não precisam de colaborar com outras organizações que utilizam o Azure RMS. Esta instalação permite-lhe instalar apenas a aplicação de partilha e o suplemento do Office.

> [!NOTE]
> Nestes cenários, se a sua organização estiver a executar o AD RMS, os seus utilizadores podem receber conteúdos protegidos de outras organizações que utilizam o Azure RMS, mas não podem enviar conteúdos protegidos para outros utilizadores de uma organização que utiliza o Azure RMS. No entanto, se a sua organização estiver a executar o Azure RMS, os seus utilizadores podem enviar e receber conteúdos protegidos de outras organizações.

Para concluir a instalação em cada procedimento, é necessário reiniciar o computador. Pode fazer um reinício automático através de um comando como o **shutdown /i**.

### Para implementar a aplicação de partilha RMS para o Office 2016 ou Office 2013 e Azure RMS ou Active Directory RMS

-   Nos computadores em que pretende instalar a aplicação de partilha RMS e os componentes relacionados, execute o seguinte comando com privilégios elevados:

    ```
    setup.exe /s
    ```

Para confirmar o êxito da operação, consulte a secção [Confirmar o êxito da instalação](#verifying-installation-success) neste artigo.

### Para implementar a aplicação de partilha RMS para o Office 2010 e o Azure RMS

1.  Tem de ser o administrador global do seu inquilino do Office 365 ou do Azure Active Directory para obter o URL do serviço de certificação da sua organização ao executar a ferramenta de preparação do Azure Active Directory Rights Management. Só precisa de executar esta ferramenta uma única vez num computador. O URL do serviço de certificação será utilizado quando instalar a aplicação de partilha RMS em cada computador:

    1.  Inicie sessão num computador com uma conta de administrador local.

    2.  Nesse computador, [transfira e instale o Assistente de Início de Sessão Online da Microsoft](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Execute o seguinte comando para apresentar no ecrã o URL do serviço de certificação, que poderá copiar e guardar para o próximo passo:

        -   Para o Windows 8.1 e o Windows 8 de 64 bits:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para o Windows 8.1 e o Windows 8 de 32 bits:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Para o Windows 7 de 64 bits:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > Este comando poderá pedir-lhe para introduzir as suas credenciais do Azure. Se o computador não estiver associado a um domínio, o pedido será apresentado. Se o computador estiver associado a um domínio, a ferramenta poderá utilizar credenciais em cache.

2.  Nos computadores em que pretende instalar a aplicação de partilha RMS, execute o seguinte comando com privilégios elevados:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  Nos computadores em que pretende instalar a aplicação de partilha RMS, os utilizadores têm de executar o seguinte comando (não são necessários privilégios elevados). Existem várias formas de realizar esta operação. Pode pedir aos utilizadores para executarem o comando (por exemplo, através de uma ligação numa mensagem de e-mail ou de uma ligação no portal de suporte técnico) ou pode adicioná-lo ao script de início de sessão dos mesmos:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

Para confirmar o êxito da operação, consulte a secção [Confirmar o êxito da instalação](#verifying-installation-success) neste artigo.

### Para implementar a aplicação de partilha RMS para o Office 2010 e o Active Directory RMS

1.  Nos computadores em que pretende instalar a aplicação de partilha RMS, execute o seguinte comando com privilégios elevados:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  Nos computadores em que pretende instalar a aplicação de partilha RMS, os utilizadores têm de executar o seguinte comando (não são necessários privilégios elevados). Existem várias formas de realizar esta operação. Pode pedir aos utilizadores para executarem o comando (por exemplo, através de uma ligação numa mensagem de e-mail ou de uma ligação no portal de suporte técnico) ou pode adicioná-lo ao script de início de sessão dos mesmos:

    -   Para o Windows 10, Windows 8.1 e Windows 8 de 64 bits:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Para o Windows 10, Windows 8.1 e Windows 8 de 32 bits:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Para o Windows 7 de 64 bits:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

Para confirmar o êxito da operação, consulte a secção [Confirmar o êxito da instalação](#verifying-installation-success) neste artigo.

### Para instalar apenas a aplicação de partilha RMS e o suplemento do Office

1.  Instale o Cliente do AD RMS e a aplicação de partilha RMS através do seguinte comando:

    -   Para o Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   Para o Windows de 32 bits:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    Por exemplo: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Instale o suplemento do Office através dos seguintes comandos:

    -   Para a versão de 64 bits do Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   Para a versão de 32 bits do Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    Por exemplo: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

Para confirmar o êxito da operação, consulte a secção [Confirmar o êxito da instalação](#verifying-installation-success) neste artigo.

## Confirmar o êxito da instalação
Pode utilizar os ficheiros de registo da instalação para verificar se a instalação foi concluída com êxito.

### Para confirmar o êxito da instalação da aplicação de partilha RMS para o Office 2016 ou o Office 2013 e o Azure RMS ou o Active Directory RMS

-   Para confirmar o êxito do comando Setup.exe, em cada computador, procure o ficheiro de registo de instalação **RMInstaller.log** na pasta *%temp%\RMS_installer_&lt;guid&gt;* e, em seguida, identifique o código de saída.

    Uma instalação com êxito apresenta um código de saída com o valor 0 e todos os outros números indicam uma falha na instalação.

    Exemplo de nome de ficheiro de registo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### Para confirmar o êxito da instalação da aplicação de partilha RMS para o Office 2010 e o Azure RMS

1.  Para confirmar o êxito do comando Setup.exe, em cada computador, procure o ficheiro de registo de instalação **RMInstaller.log** na pasta *%temp%\RMS_installer_&lt;guid&gt;* e, em seguida, identifique o código de saída.

    Uma instalação com êxito apresenta um código de saída com o valor 0 e todos os outros números indicam uma falha na instalação.

    Exemplo de nome de ficheiro de registo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para confirmar o êxito do comando RMSSetup.exe, o utilizador deve ter os seguintes ficheiros criados na pasta *%localappdata%\microsoft\drm*:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    Exemplo de um ficheiro CLC-&#42;.drm:

    **CLC-ines@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### Para confirmar o êxito da instalação da aplicação de partilha RMS para o Office 2010 e o Active Directory RMS

1.  Para confirmar o êxito do comando Setup.exe, em cada computador, procure o ficheiro de registo de instalação na pasta *%temp%\RMS_installer_&lt;guid&gt;* e identifique o código de saída.

    Uma instalação com êxito apresenta um código de saída com o valor 0 e todos os outros números indicam uma falha na instalação.

    Exemplo de nome de ficheiro de registo: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  Para confirmar o êxito do comando aadrmprep.exe, em cada computador, procure o seguinte texto no ficheiro de registo de instalação: **aadrmprep.exe saiu com o estado ÊXITO**

    > [!NOTE]
    > Por vezes, a instalação pode ser executada duas vezes; a primeira ocorrência resulta em falha e a segunda é concluída com êxito.

    Se quiser verificar manualmente as alterações de registo feitas pela ferramenta, estas são as seguintes:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### Para confirmar o êxito da instalação apenas para a aplicação de partilha RMS e o suplemento do Office

1.  Para confirmar o êxito do comando Setup_ipviewer.exe, procure o seguinte texto no ficheiro de registo de instalação: **Installation success or error status: 0**

    Exemplos de linhas de uma instalação concluída com êxito:

    **MSI (s) (F0:B8) [14:19:57:854]: Product: Active Directory Rights Management Services Client 2.1 -- Installation completed successfully.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer installed the product. Product Name: Active Directory Rights Management Services Client 2.1. Product Version: 1.0.1179.1. Product Language: 1033. Manufacturer: Microsoft Corporation. Installation success or error status: 0.**

2.  Para confirmar o êxito da instalação do suplemento do Office, procure em cada computador o seguinte texto no ficheiro de registo de instalação: **Installation success or error status: 0**

    Exemplos de linhas de uma instalação concluída com êxito:

    **MSI (s) (9C:88) [18:49:04:007]: Product: Microsoft RMS Office Addins -- Installation completed successfully.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer installed the product. Product Name: Microsoft RMS Office Addins. Product Version: 1.0.7. Product Language: 1033. Manufacturer: Microsoft. Installation success or error status: 0.**

## Comandos de desinstalação
Nem todos os comandos de instalação necessários para efetuar estas implementações suportam um comando de desinstalação. Pode desinstalar o cliente e a aplicação de partilha AD RMS, bem como o suplemento do Office. Utilize os seguintes comandos para desinstalar estes elementos.

### Para desinstalar o Cliente AD RMS e a aplicação de partilha RMS

-   Utilize os seguintes comandos:

    -   Para o Windows de 64 bits:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   Para o Windows de 32 bits:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### Para desinstalar o suplemento do Office

-   Utilize os seguintes comandos:

    -   Para a versão de 64 bits do Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   Para a versão de 32 bits do Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## Suprimir as atualizações automáticas
Por predefinição, os utilizadores recebem uma notificação quando existe uma versão mais recente da aplicação de partilha RMS e é-lhes pedido que a transfiram. Pode suprimir esta notificação ao fazer a seguinte edição de registo:

1.  Navegue para **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e, se esta ainda não existir, crie uma nova chave com o nome **RmsSharingApp**.

2.  Selecione **RmsSharingApp**, crie um novo Valor DWORD para **AllowUpdatePrompt** e defina o valor para **0**.

Dado que a aplicação de partilha RMS não é suportada pelo WSUS, pode utilizar o seguinte método para testar as novas versões da aplicação de partilha RMS antes de as implementar para todos os utilizadores:

1.  Execute um script nos computadores de todos os utilizadores para suprimir as atualizações automáticas. Não execute este script nos computadores utilizados pelos administradores para testar novas versões.

2.  Quando uma nova versão se encontra disponível, os administradores devem transferi-la e testá-la.

3.  Após a conclusão dos testes e a resolução de eventuais problemas, implemente a versão mais recente para todos os utilizadores através das instruções de implementação automática existentes neste guia.

## Apenas Azure RMS: configurar o controlo de documentos
Se tiver uma [subscrição que suporta o controlo de documentos](https://technet.microsoft.com/dn858608), o site de controlo de documentos é ativado por predefinição para todos os utilizadores da sua organização.  O controlo de documentos apresenta informações como os endereços de e-mail das pessoas que tentaram aceder a documentos protegidos partilhados por utilizadores, quando essas pessoas tentaram aceder aos mesmos e a sua localização. Se a apresentação deste tipo de informações é proibida dentro da sua organização devido a requisitos de privacidade, pode desativar o acesso ao site de controlo de documentos através do cmdlet [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032). Pode reativar o acesso ao site em qualquer altura através de [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) e ainda verificar se o acesso ao site está ativado ou desativado com [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

Para executar estes cmdlets, tem de ter no mínimo a versão **2.3.0.0** do módulo do Azure RMS para o Windows PowerShell.  Para obter instruções de instalação, consulte [Instalar o Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

> [!TIP]
> Se já transferiu e instalou o módulo anteriormente, verifique o número da versão ao executar: `(Get-Module aadrm –ListAvailable).Version`

Os URLs seguintes são utilizados para o controlo de documentos e têm de ser permitidos (por exemplo, adicione-os à sua lista de Sites Fidedignos se estiver a utilizar o Internet Explorer com Segurança Avançada):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > Este URL é destinado aos mapas Bing.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## Apenas AD RMS: suporte para múltiplos domínios de e-mail dentro da sua organização
Se utilizar o AD RMS e os utilizadores da sua organização tiverem múltiplos domínios de e-mail, possivelmente como resultado de uma fusão ou aquisição, tem de criar a seguinte edição de registo:

1.  Navegue para **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** e, se esta ainda não existir, crie uma nova chave com o nome **RmsSharingApp**.

2.  Selecione **RmsSharingApp**, crie um novo Valor de Múltiplas Cadeias com o nome **FederatedDomains** e, em seguida, adicione todos os domínios e subdomínios utilizados pela sua organização. Os carateres universais não são suportados.

    Por exemplo: a empresa Coho Vineyard &amp; Winery tem o domínio de e-mail padrão **cohovineyardandwinery.com** mas, devido a fusões, também utilizam os domínios de e-mail **cohowinery.com**, **eastcoast.cohowinery.com** e **cohovineyard**. Para os dados do valor **FederatedDomains**, o administrador deve introduzir: **cohowinery.com;eastcoast.cohowinery.com;cohovineyard**

Se não fizer esta alteração de registo, é possível que os utilizadores não consigam consumir conteúdos que foram protegidos por outros utilizadores da organização. Esta edição de registo não é necessária se utilizar o Azure RMS.


## Passos seguintes
Para obter informações técnicas adicionais com explicações sobre os diferentes níveis de proteção (nativa e genérica), os tipos de ficheiro e as extensões de nome de ficheiro suportados e como pode alterar o nível de proteção predefinido, consulte [Descrição geral técnica da aplicação de partilha Rights Management](sharing-app-admin-guide-technical.md).




<!--HONumber=Jul16_HO2-->


