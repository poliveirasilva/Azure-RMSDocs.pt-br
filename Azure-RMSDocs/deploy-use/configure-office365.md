---
title: "Office 365&colon; Configuração para clientes e serviços online | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 7a2436a6ebb17e4336f1321b8f3742e34ea59689


---

# Office 365: Configuração para clientes e serviços online

*Aplica-se a: Azure Rights Management, Office 365*

Como o Office 365 suporta nativamente o Azure RMS, não é necessária nenhuma configuração de computador cliente para suportar as funcionalidades de gestão de direitos de informação (IRM) em aplicações como o Word, o Excel, o PowerPoint, o Outlook e o Outlook Web App. Os utilizadores só têm de iniciar sessão nas aplicações do Office com as respetivas credenciais do [!INCLUDE[o365_1](../includes/o365_1_md.md)] para poderem proteger ficheiros e e-mails e utilizar ficheiros e e-mails protegidos por outras pessoas.

No entanto, recomendamos que complemente estas aplicações com a aplicação de partilha Rights Management, para que os utilizadores possam beneficiar do suplemento do Office. Para obter mais informações, consulte [Aplicação de partilha Rights Management: instalação e configuração para clientes](configure-sharing-app.md).

## Exchange Online: configuração de IRM
Para configurar o Exchange Online para suportar o Azure RMS, tem de configurar o serviço de gestão de direitos de informação (IRM) para o Exchange Online. Para isso, tem de utilizar o Windows PowerShell (não é necessário instalar um módulo separado) e executar os [comandos do PowerShell para o Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Atualmente, não pode configurar o Exchange Online para suportar o Azure RMS caso esteja a utilizar uma chave de inquilino gerida pelo cliente (BYOK) para o Azure RMS, em vez da configuração predefinida de uma chave de inquilino gerida pela Microsoft. Para obter mais informações, consulte [Preços e restrições do BYOK](../plan-design/byok-price-restrictions.md).
>
> Se tentar configurar o Exchange Online quando o Azure RMS está a utilizar uma BYOK, o comando para importar a chave (passo 5 no procedimento seguinte) falha com a mensagem de erro **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Os passos seguintes fornecem um conjunto típico de comandos que executaria para ativar o Exchange Online de forma a utilizar o Azure RMS:

1.  Se esta é a primeira vez que utiliza o Windows PowerShell para o Exchange Online no seu computador, tem de configurar o Windows PowerShell para executar scripts assinados. Inicie sessão do Windows PowerShell através da opção **Executar como administrador** e, em seguida, escreva:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Na sessão do Windows PowerShell, inicie sessão no Exchange Online com uma conta ativada para acesso remoto à Shell. Por predefinição, todas as contas criadas no Exchange Online têm o acesso remoto à Shell ativado, embora possa desativar (e ativar) esta funcionalidade através do comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Para iniciar sessão, escreva:

    ```
    $Cred = Get-Credential
    ```
    Na caixa de diálogo **Pedido de Credencial do Windows PowerShell**, forneça o seu nome de utilizador e palavra-passe do Office 365.

3.  Execute os dois comandos seguintes para ligar ao serviço Exchange Online:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Especifique a localização da chave de inquilino do Azure RMS, em conformidade com a localização onde foi criado o inquilino da sua empresa:

    Para a América do Norte (e subscrições para a administração pública):

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para a Europa:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para a Ásia:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Para a América do Sul:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importe dados de configuração a partir do Azure RMS para o Exchange Online sob a forma de um domínio de publicação fidedigno (TPD). Isto inclui a chave de inquilino do Azure RMS e modelos do Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    Neste comando, utilizámos o nome **RMS Online** como nome de base do TPD para o Azure RMS no Exchange Online. Após a importação do TPD, terá o nome **RMS Online – 1** no Exchange Online.

6.  Ative a funcionalidade do Azure RMS para que as funcionalidades da IRM estejam disponíveis no Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Após executar este comando, o Rights Management é automaticamente ativado para o cliente do Outlook, o Outlook Web App e o Exchange Active Sync.

7.  Opcionalmente, pode testar se esta configuração tem êxito através do seguinte comando:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Por exemplo: **Test-IRMConfiguration -Sender andrade@contoso.com**

    Este comando executa um conjunto de verificações que inclui a verificação da conectividade ao serviço, a obtenção da configuração, a obtenção de URIs, licenças e modelos. Na sessão do Windows PowerShell, verá os resultados de cada verificação e, no final, se nenhuma delas encontrar problemas, verá a mensagem: **RESULTADO GERAL: APROVADO**

8.  Desligue a sua sessão remota do PowerShell:

    ```
    Remove-PSSession $Session
    ```

Agora, os utilizadores podem proteger as suas mensagens de email através do Azure RMS. Por exemplo, no Outlook Web App, selecione **Definir permissões** no menu expandido (**...**) e, em seguida, selecione **Não Reencaminhar** ou um dos modelos disponíveis para aplicar a proteção da informação à mensagem de e-mail e respetivos anexos. Contudo, como o Outlook Web App coloca a IU em cache durante um dia, espere que este período de tempo termine antes de tentar aplicar a proteção da informação às mensagens de e-mail e depois de executar estes comandos de configuração. Antes da atualização da IU para refletir a nova configuração, não verá nenhuma opção no menu **Definir permissões**.

> [!IMPORTANT]
> Se criar novos [modelos personalizados](configure-custom-templates.md) para o Azure RMS ou atualizar os modelos, de cada vez que o fizer, terá de executar o seguinte comando do Exchange Online PowerShell (se for necessário, execute primeiro os passos 2 e 3) para sincronizar estas alterações com o Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Como administrador do Exchange, já pode configurar funcionalidades que apliquem automaticamente a proteção da informação, como, por exemplo, [regras de transporte](https://technet.microsoft.com/library/dd302432.aspx), [políticas de prevenção de perda de dados (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) e [voice mail protegido](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (Unified Messaging).

Para obter instruções detalhadas para configurar o Exchange Online de forma a ativar a funcionalidade IRM, consulte a documentação na biblioteca do Exchange. Por exemplo:

-   [Connect to Exchange Online using remote PowerShell (Ligar ao Exchange Online através do PowerShell remoto – em inglês)](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Configure IRM to use Azure Rights Management (Configurar a IRM para utilizar o Azure Rights Management – em inglês)](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### Encriptação de Mensagens do Office 365
Execute os mesmos passos conforme indicado na secção anterior. Contudo, se não pretender que os modelos sejam apresentados, antes de chegar ao passo 6, execute o comando seguinte para impedir que os modelos IRM estejam disponíveis no Outlook Web App e no cliente do Outlook: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Em seguida, estará pronto para configurar [regras de transporte](https://technet.microsoft.com/library/dd302432.aspx), para modificar automaticamente a segurança da mensagem quando os destinatários estão fora da organização, e selecionar a opção **Aplicar a Encriptação de Mensagens do Office 365**.

Para mais informações sobre a encriptação de mensagens, consulte [Encryption in Office 365 (Encriptação no Office 365 – em inglês)](https://technet.microsoft.com/library/dn569286.aspx) na biblioteca do Exchange.

## SharePoint Online e OneDrive para Empresas: configuração de IRM
Para configurar o SharePoint Online e o OneDrive para Empresas para suportar o Azure RMS, primeiro tem de ativar o serviço de gestão de direitos de informação (IRM) para o SharePoint Online através do centro de administração do SharePoint. Em seguida, os proprietários de sites podem proteger as respetivas listas e bibliotecas de documentos do SharePoint com IRM e, além disso, os utilizadores podem proteger a respetiva biblioteca do OneDrive para Empresas com a IRM para que os documentos aí guardados e partilhados com outras pessoas, sejam automaticamente protegidos pelo Azure RMS.

Para ativar o serviço de gestão de direitos de informação (IRM) para o SharePoint Online, consulte as instruções seguintes a partir do site do Office:

-   [Configurar a Gestão de Direitos de Informação (IRM) no centro de administração do SharePoint](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Esta configuração é efetuada pelo administrador do Office 365.

### Configurar a IRM para listas e bibliotecas
Após ativar o serviço de IRM para o SharePoint, os proprietários de sites podem proteger as respetivas listas e bibliotecas de documentos do SharePoint com a IRM. Para obter instruções, consulte o seguinte a partir do site do Office:

-   [Aplicar a Gestão de Direitos de Informação a uma lista ou biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Esta configuração é efetuada pelo administrador do site do SharePoint.

### Configurar a IRM para o OneDrive para Empresas
Após ativar o serviço de IRM para o SharePoint Online, a biblioteca de documentos do OneDrive para Empresas dos utilizadores pode ser configurada para a proteção Rights Management.  Os próprios utilizadores podem configurar isto através do ícone **Definições** no respetivo OneDrive. Embora os administradores não possam configurar o Rights Management para o OneDrive para Empresas dos utilizadores através do centro de administração do SharePoint, o utilizador pode fazê-lo através do Windows PowerShell.

> [!NOTE]
> Para obter mais informações sobre como configurar o OneDrive para Empresas, consulte a documentação do Office, [Configurar o OneDrive para Empresas no Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

#### Configuração para os utilizadores
Dê estas instruções aos utilizadores para que possam configurar o OneDrive para Empresas e proteger os respetivos ficheiros empresariais com IRM.

1.  No OneDrive, clique no ícone **Definições** para abrir o menu Definições e, em seguida, clique em **Conteúdos do Site**.

2.  Paire o rato sobre o mosaico **Documentos**, selecione as reticências (**...**) e, em seguida, clique em **DEFINIÇÕES**.

3.  Na página **Definições**, na secção **Permissões e Gestão**, clique em **Gestão de Direitos de Informação**.

4.  Na página **Definições de Gestão de Direitos de Informação**, selecione a caixa de verificação **Restringir as permissões nesta biblioteca durante a transferência**, especifique a sua escolha de nome e uma descrição para as permissões e, opcionalmente, clique em **MOSTRAR OPÇÕES** para definir configurações opcionais e, em seguida, clique em **OK**.

    Para mais informações sobre as opções de configuração, consulte as instruções em [Aplicar a Gestão de Direitos de Informação a uma lista ou biblioteca](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) na documentação do Office.

Como esta configuração se baseia nos utilizadores em vez de num administrador para proteger a respetiva biblioteca do OneDrive para Empresas com a IRM, informe os utilizadores sobre os benefícios de proteger os seus ficheiros e sobre como proceder nesse sentido. Por exemplo, explique que quando partilham um documento do OneDrive para Empresas, apenas as pessoas a quem concederem autorização poderão aceder ao mesmo, com as restrições que configurarem, mesmo que o nome e a localização do ficheiro tenham sido alterados.

#### Configuração para administradores
Embora não possa configurar a IRM para o OneDrive para Empresas dos utilizadores através do centro de administração do SharePoint, pode fazê-lo através do Windows PowerShell. Para ativar a IRM para estas bibliotecas, siga estes passos:

1.  Transfira e instale o [SDK de Componentes de Cliente do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Transfira e instale a [Shell de Gestão do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Copie o conteúdo do seguinte script e, no seu computador, dê ao ficheiro o nome Set-IRMOnOneDriveForBusiness.ps1.

    *&#42;&#42;Exclusão de responsabilidade&#42;&#42;*: este script de exemplo não é suportado por qualquer serviço ou programa de suporte padrão da Microsoft. Este script de exemplo é fornecido TAL COMO ESTÁ, sem qualquer tipo de garantia.

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       http://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       http://www.microsoft.com/en-us/download/details.aspx?id=35588

    ======
    #>

    # URL will be in the format https://<tenant-name>-admin.sharepoint.com
    $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

    $tenantAdmin = "admin@contoso.com"

    $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

    <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
       Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

    #>

    $listTitle = "Documents"

    function Load-SharePointOnlineClientComponentAssemblies
    {
        [cmdletbinding()]
        param()

        process
        {
            # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
            try
            {
                Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                return $true
            }
            catch
            {
                if($_.Exception.Message -match "Could not load file or assembly")
                {
                    Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
                }
                else
                {
                    Write-Error -Exception $_.Exception
                }
                return $false
            }
        }
    }

    function Load-SharePointOnlineModule
    {
        [cmdletbinding()]
        param()

        process
        {
            do
            {
                # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
                $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

                if(-not $spoModule)
                {
                    try
                    {
                        Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                        return $true
                    }
                    catch
                    {
                        if($_.Exception.Message -match "Could not load file or assembly")
                        {
                            Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                        }
                        else
                        {
                            Write-Error -Exception $_.Exception
                        }
                        return $false
                    }
                }
                else
                {
                    return $true
                }
            }
            while(-not $spoModule)
        }
    }

    function Set-IrmConfiguration
    {
        [cmdletbinding()]
        param(
            [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
            [parameter(Mandatory=$true)][string]$PolicyTitle,
            [parameter(Mandatory=$true)][string]$PolicyDescription,
            [parameter(Mandatory=$false)][switch]$IrmReject,
            [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
            [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
            [parameter(Mandatory=$false)][switch]$AllowPrint,
            [parameter(Mandatory=$false)][switch]$AllowScript,
            [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
            [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
            [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
            [parameter(Mandatory=$false)][string]$GroupName
        )

        process
        {
            Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

            # reset the value to the default settings
            $list.InformationRightsManagementSettings.Reset()

            $list.IrmEnabled = $true

            # IRM Policy title and description

                $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
                $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

            # Set additional IRM library settings

                # Do not allow users to upload documents that do not support IRM
                $list.IrmReject = $IrmReject.IsPresent

                $parsedDate = Get-Date
                if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
                {
                    # Stop restricting access to the library at <date>
                    $list.IrmExpire = $true
                    $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
                }

                # Prevent opening documents in the browser for this Document Library
                $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

            # Configure document access rights

                # Allow viewers to print
                $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

                # Allow viewers to run script and screen reader to function on downloaded documents
                $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

                # Allow viewers to write on a copy of the downloaded document
                $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

                if($DocumentAccessExpireDays)
                {
                    # After download, document access rights will expire after these number of days (1-365)
                    $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                    $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
                }

            # Set group protection and credentials interval

                if($LicenseCacheExpireDays)
                {
                    # Users must verify their credentials using this interval (days)
                    $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                    $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
                }

                if($GroupName)
                {
                    # Allow group protection. Default group:
                    $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                    $list.InformationRightsManagementSettings.GroupName             = $GroupName
                }
        }
        end
        {
            if($list)
            {
                Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
                $list.InformationRightsManagementSettings.Update()
                $list.Update()
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()
            }
        }
    }

    function Get-CredentialFromCredentialCache
    {
        [cmdletbinding()]
        param([string]$CredentialName)

        #if( Test-Path variable:\global:CredentialCache )
        if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
        {
            if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
            {
                Write-Verbose "Credential Cache Hit: $CredentialName"
                return $global:O365TenantAdminCredentialCache[$CredentialName]
            }
        }
        Write-Verbose "Credential Cache Miss: $CredentialName"
        return $null
    }

    function Add-CredentialToCredentialCache
    {
        [cmdletbinding()]
        param([System.Management.Automation.PSCredential]$Credential)

        if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
        {
            Write-Verbose "Initializing the Credential Cache"
            $global:O365TenantAdminCredentialCache = @{}
        }

        Write-Verbose "Adding Credential to the Credential Cache"
        $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
    }

    # load the required assemblies and Windows PowerShell modules

        if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

    # Add the credentials to the client context and SharePoint Online service connection

        # check for cached credentials to use
        $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

        if(-not $o365TenantAdminCredential)
        {
            # when credentials are not cached, prompt for the tenant admin credentials
            $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

            if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
            {
                Write-Error -Message "Could not validate the supplied tenant admin credentials"
                return
            }

            # add the credentials to the cache
            Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
        }

    # connect to Office365 first, required for SharePoint Online cmdlets to run

        Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

    # enumerate each of the specified site URLs

        foreach($webUrl in $webUrls)
        {
            $grantedSiteCollectionAdmin = $false

            try
            {
                # establish the client context and set the credentials to connect to the site
                $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
                $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

                # initialize the site and web context
                $script:clientContext.Load($script:clientContext.Site)
                $script:clientContext.Load($script:clientContext.Web)
                $script:clientContext.ExecuteQuery()

                # load and ensure the tenant admin user account if present on the target SharePoint site
                $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
                $script:clientContext.Load($tenantAdminUser)
                $script:clientContext.ExecuteQuery()

                # check if the tenant admin is a site admin
                if( -not $tenantAdminUser.IsSiteAdmin )
                {
                    try
                    {
                        # grant the tenant admin temporary admin rights to the site collection
                        Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                        $grantedSiteCollectionAdmin = $true
                    }
                    catch
                    {
                        Write-Error $_.Exception
                        return
                    }
                }

                try
                {
                    # load the list orlibrary using CSOM

                    $list = $null
                    $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                    $script:clientContext.Load($list)
                    $script:clientContext.ExecuteQuery()

                    # **************  ADMIN INSTRUCTIONS  **************
                    # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                    # The supplied options and values are for example only
                    # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                    Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
                }
                catch
                {
                    Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
                }
           }
           finally
           {
                if($grantedSiteCollectionAdmin)
                {
                    # remove the temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
                }
           }
        }

    Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  Reveja o script e efetue as seguintes alterações:

    1.  Procure o `$sharepointAdminCenterUrl` e substitua o valor de exemplo pelo seu próprio URL do centro de administração do SharePoint.

        Pode encontrar este valor como o URL de base ao aceder ao centro de administração do SharePoint, com o seguinte formato: https://*&lt;nome_de_inquilino&gt;*-admin.sharepoint.com

        Por exemplo, se o nome do inquilino for "contoso", tem de especificar: **https://contoso-admin.sharepoint.com**

    2.  Procure o `$tenantAdmin` e substitua o valor de exemplo pela sua própria conta de administrador global completamente qualificado do Office 365.

        Este valor é o mesmo que utiliza para iniciar sessão no portal de administração do Office 365 como administrador global e tem o seguinte formato: nome_de_utilizador@*&lt;nome de domínio do inquilino&gt;*.com

        Por exemplo, se o nome de utilizador de administrador global do Office 365 for "admin" para o domínio de inquilino "contoso.com", tem de especificar: **admin@contoso.com**

    3.  Procure os `$webUrls` e substitua os valores de exemplo pelos URLs da Web do OneDrive para Empresas dos seus utilizadores, adicionando ou eliminando tantas entradas quantas for necessário.

        Em alternativa, veja os comentários no script sobre como substituir esta matriz ao importar um ficheiro .CSV que contenha todos os URLs que tem de configurar.  Fornecemos outro script de exemplo que permite procurar e extrair automaticamente os URLs para popular este ficheiro .CSV. Quando estiver pronto para efetuar este procedimento, expanda a secção [Script adicional para exportar todos os URLs do OneDrive para Empresas para um ficheiro .CSV](#BKMK_Script_OD4B_URLS) imediatamente após estes passos.

        O URL da Web do OneDrive para Empresas do utilizador tem o seguinte formato: https://*&lt;nome do inquilino&gt;*-my.sharepoint.com/personal/*&lt;nome_de_utilizador&gt;*_*&lt;nome do inquilino&gt;*_com

        Por exemplo, se o utilizador no inquilino contoso tiver o nome de utilizador "sferreira", tem de especificar: **https://contoso-my.sharepoint.com/personal/sferreira_contoso_com**

    4.  Uma vez que estamos a utilizar o script para configurar o OneDrive para Empresas, não altere o valor da variável de **Documentos**`$listTitle`.

    5.  Procure as `ADMIN INSTRUCTIONS`. Se não efetuar alterações nesta secção, o OneDrive para Empresas do utilizador será configurado para a IRM com o título de política "Ficheiros Protegidos" e a descrição "Esta política restringe o acesso a utilizadores autorizados".  Não serão definidas outras opções de IRM, o que provavelmente será o mais adequado para a maioria dos ambientes. No entanto, pode alterar o título e a descrição sugeridos para a política, bem como adicionar outras opções de IRM que se adequem ao seu ambiente. Consulte o exemplo comentado no script para o ajudar a criar o seu próprio conjunto de parâmetros para o comando Set-IrmConfiguration.

5.  Guarde o script e assine-o. Se não assinar o script (mais seguro), tem de configurar o Windows PowerShell no seu computador para executar scripts não assinados. Para o fazer, execute uma sessão do Windows PowerShell com a opção **Executar como Administrador** e escreva: **Set-ExecutionPolicy Unrestricted**. No entanto, esta configuração permite executar todos os scripts não assinados (menos seguro).

    Para mais informações sobre como assinar os scripts do Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) na biblioteca de documentação do PowerShell.

6.  Execute o script e, se lhe for pedido, forneça a palavra-passe da conta de administrador do Office 365. Se modificar o script e o executar na mesma sessão do Windows PowerShell, não lhe serão pedidas credenciais.

> [!TIP]
> Também pode utilizar este script para configurar a IRM para uma biblioteca do SharePoint Online. Para esta configuração, recomenda-se que ative a opção adicional **Não permitir que os utilizadores carreguem documentos que não suportem a IRM**, para se certificar de que a biblioteca contém apenas documentos protegidos.    Para tal, adicione o parâmetro `-IrmReject` ao comando Set-IrmConfiguration no script.
>
> Também terá de modificar a variável `$webUrls` (por exemplo, **https://contoso.sharepoint.com**) e a variável `$listTitle` (por exemplo, **$Reports**).

Se precisar de desativar a IRM para as bibliotecas do OneDrive para Empresas do utilizador, consulte a secção [Script para desativar a IRM para o OneDrive para Empresas](#script-to-disable-irm-for-onedrive-for-business).

##### Script adicional para exportar todos os URLs do OneDrive para Empresas para um ficheiro .CSV
No passo 4c acima, pode utilizar o seguinte script do Windows PowerShell para extrair os URLs de todas as bibliotecas do OneDrive para Empresas dos utilizadores, os quais pode verificar e, se necessário, editar e, em seguida, importar para o script principal.

Este script também requer o [SDK de Componentes de Cliente do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) e a [Shell de Gestão do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Siga as mesmas instruções para o copiar e colar, guarde o ficheiro localmente (por exemplo, "Report-OneDriveForBusinessSiteInfo.ps1"), modifique os valores `$sharepointAdminCenterUrl` e `$tenantAdmin` como fez anteriormente e, em seguida, execute o script.

*&#42;&#42;Exclusão de responsabilidade&#42;&#42;*: este script de exemplo não é suportado por qualquer serviço ou programa de suporte padrão da Microsoft. Este script de exemplo é fornecido TAL COMO ESTÁ, sem qualquer tipo de garantia.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### Script para desativar a IRM para o OneDrive para Empresas
Utilize o seguinte script de exemplo caso precise de desativar a IRM do OneDrive para Empresas dos utilizadores.

Este script também requer o [SDK de Componentes de Cliente do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) e a [Shell de Gestão do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Copie e cole o conteúdo, guarde o ficheiro localmente (por exemplo, "Disable-IRMOnOneDriveForBusiness.ps1") e modifique os valores `$sharepointAdminCenterUrl` e `$tenantAdmin`. Especifique manualmente os URLs do OneDrive para Empresas ou utilize o script da secção anterior para poder importar os mesmos e, em seguida, execute o script.

*&#42;&#42;Exclusão de responsabilidade&#42;&#42;*: este script de exemplo não é suportado por qualquer serviço ou programa de suporte padrão da Microsoft. Este script de exemplo é fornecido TAL COMO ESTÁ, sem qualquer tipo de garantia.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint Online cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list                 
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```




<!--HONumber=Jun16_HO4-->


