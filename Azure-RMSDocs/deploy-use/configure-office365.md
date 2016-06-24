---
# required metadata

title: Office 365&colon; Configuração para clientes e serviços online | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Office 365: Configuração para clientes e serviços online

*Aplica-se a: Azure Rights Management, Office 365*

Como o Office 365 oferece suporte nativo ao Azure RMS, nenhuma configuração do computador cliente é necessária para oferecer suporte aos recursos do gerenciamento de direitos de informação (IRM) para aplicativos como Word, Excel, PowerPoint, Outlook e o Outlook Web App. Tudo o que os usuários precisam fazer é entrar em seus aplicativos do Office com suas credenciais do [!INCLUDE[o365_1](../includes/o365_1_md.md)] e eles poderão proteger arquivos e emails, e usar arquivos e emails que foram protegidos por outras pessoas.

No entanto, recomendamos que você complemente esses aplicativos com o aplicativo de compartilhamento do Rights Management, de modo que os usuários se beneficiem do suplemento do Office. Para mais informações, consulte [Aplicativo de compartilhamento do Rights Management: instalação e configuração para clientes](configure-sharing-app.md).

## Exchange Online: Configuração do IRM
Para configurar o Exchange Online para suportar o Azure RMS, é necessário configurar o gerenciamento de direitos de informação (IRM) para o Exchange Online. Para fazer isso, use o Windows PowerShell (sem necessidade de instalar um módulo separado) e execute os [comandos do PowerShell para Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> No momento não é possível configurar o Exchange Online para suportar o Azure RMS se você estiver usando uma chave de locatário gerenciada pelo cliente (BYOK) para o Azure RMS, em vez da configuração padrão de uma chave de locatário gerenciada pela Microsoft. Para obter mais informações, consulte [Preços e restrições do BYOK](../plan-design/byok-price-restrictions.md).
>
> Se você tentar configurar o Exchange Online quando o Azure RMS estiver usando o BYOK, o comando para importar a chave (etapa 5, no seguinte procedimento) falhará com a mensagem de erro **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

As seguintes etapas fornecem um conjunto comum de comandos que você executaria para habilitar o Exchange Online para usar o Azure RMS:

1.  Se esta for a primeira vez que você usou o Windows PowerShell para o Exchange Online no seu computador, você deve configurar o Windows PowerShell para executar scripts assinados. Iniciar sessão do Windows PowerShell usando a opção **Executar como administrador** e em seguida, digite:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Na sua sessão do Windows PowerShell, entre no Exchange Online usando uma conta que está habilitada para acesso remoto do Shell. Por padrão, todas as contas criadas no Exchange Online são ativadas para acesso remoto do Shell, mas essa função pode ser desabilitada (e habilitada) usando o comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Para entrar, digite:

    ```
    $Cred = Get-Credential
    ```
    Na caixa de diálogo de **solicitação de credencial do Windows PowerShell** , forneça seu nome e senha de usuário do Office 365.

3.  Conecte-se ao serviço Exchange Online executando os seguintes dois comandos:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Especifique a localização da chave de locatário do Azure RMS de acordo com o local em que foi criado o locatário da sua organização:

    Para a América do Norte (e assinaturas do governo):

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

5.  Importar dados de configuração do Azure RMS para o Exchange Online, na forma de domínio de publicação confiável (TPD). Isso inclui a chave de locatário do Azure RMS e modelos do Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    Neste comando, usamos o nome de **RMS Online** para o nome base do TPD para o Azure RMS no Exchange Online. Depois que o TPD é importado, ele é nomeado **RMS Online - 1** no Exchange Online.

6.  Habilite a funcionalidade do Azure RMS para que os recursos do IRM estejam disponíveis para o Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Após executar esse comando, o gerenciamento de direitos é habilitado automaticamente para o cliente do Outlook, Outlook Web app e Exchange Active Sync.

7.  Opcionalmente, teste se essa configuração é bem-sucedida, usando o seguinte comando:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Por exemplo, **Test-IRMConfiguration -Sender  adams@contoso.com**

    Esse comando executa uma série de verificações que inclui verificação da conectividade ao serviço, recuperação da configuração, recuperação de todos os modelos, licenças e URIs. Na sessão do Windows PowerShell, você verá os resultados de cada um e no final, se tudo passa essas verificações: **RESULTADO GERAL: PASSAGEM**

8.  Desconecte a sua sessão remota do PowerShell:

    ```
    Remove-PSSession $Session
    ```

Os usuários agora podem proteger suas mensagens de email usando o Azure RMS. Por exemplo, no Outlook Web App, selecione **Definir permissões** no menu estendido (**...**) e, em seguida, escolha **Não Encaminhar** ou um dos modelos disponíveis para aplicar a proteção de informações para mensagem de email e anexos. No entanto, como o Outlook Web App armazena em cache a interface do usuário por um dia, aguarde esse período de tempo de espera antes de tentar aplicar proteção de informações para mensagens de email e depois de executar estes comandos de configuração. Antes que a interface do usuário seja atualizada para refletir a nova configuração, você não verá as opções do menu **definir permissões** .

> [!IMPORTANT]
> Se você criar novos [modelos personalizados](configure-custom-templates.md) para o Azure RMS ou atualizar os modelos, todas as vezes, você deverá executar o seguinte comando do PowerShell do Exchange Online (se necessário, execute as etapas 2 e 3 primeiro) para sincronizar essas alterações para o Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Como um administrador do Exchange, agora você pode configurar recursos que se aplicam à proteção de informações automaticamente, como [regras de transporte](https://technet.microsoft.com/library/dd302432.aspx), [políticas de DLP (prevenção de perda de dados)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) e [caixa postal protegida](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (Unificação de Mensagens).

Para obter instruções detalhadas sobre como configurar o Exchange Online para habilitar a funcionalidade do IRM, consulte a documentação na biblioteca do Exchange. Por exemplo:

-   [Conexão com o Exchange Online usando o PowerShell remoto](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Configurar o IRM para usar o Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### Criptografia de mensagens do Office 365
Execute as mesmas etapas, conforme documentado na seção anterior, mas se você não quiser que os modelos sejam exibidos, antes da etapa 6, execute o seguinte comando para impedir que os modelos IRM estejam disponíveis no cliente do Outlook e no Outlook Web App: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Em seguida, você está pronto para configurar [regras de transporte](https://technet.microsoft.com/library/dd302432.aspx) para modificar automaticamente a segurança da mensagem quando os destinatários estão localizados fora da organização e selecione a opção **Apply Office 365 Message Encryption** .

Para obter mais informações sobre criptografia de mensagem, consulte [criptografia no Office 365](https://technet.microsoft.com/library/dn569286.aspx) na biblioteca do Exchange.

## SharePoint Online e OneDrive para a empresa: Configuração do IRM
Para configurar o SharePoint Online para oferecer suporte ao One Drive para Empresas, primeiro deve ativar o serviço de gerenciamento de direitos de informação (IRM) para o SharePoint Online através do centro de administração do SharePoint Online. Em seguida, os proprietários de sites podem proteger por IRM as suas listas do SharePoint e as bibliotecas de documentos e os usuários podem proteger por IRM sua biblioteca do OneDrive para Empresas para que os documentos que são guardados na mesma e compartilhados com outras pessoas, sejam automaticamente protegidos pelo Azure RMS.

Para habilitar o serviço de gestão de direito de informação (IRM) para o SharePoint Online, consulte as seguintes instruções no site do Office:

-   [Configurar o Gerenciamento de Direitos de Informação (IRM) no centro de administração do SharePoint](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Essa configuração é feita pelo administrador do Office 365.

### Configurando o IRM para bibliotecas e listas
Depois que você tiver ativado o serviço IRM para SharePoint, os proprietários de sites podem proteger por IRM suas bibliotecas de documentos e listas do SharePoint. Para obter instruções, consulte o seguinte no site do Office:

-   [Aplicar o Gerenciamento de Direitos de Informação a uma lista ou biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Essa configuração é feita pelo administrador local do SharePoint.

### Configurando o IRM para OneDrive para Empresas
Depois que você tiver ativado o serviço IRM para o SharePoint Online, a biblioteca de documentos OneDrive for Business dos usuários poderá, então, ser configurada para proteção do Rights Management.  Os usuários podem configurá-la para si mesmos usando o ícone **Configurações** em seu OneDrive. Embora os administradores não possam configurar o Rights Management para os usuários do OneDrive for Business usando o centro de administração do SharePoint, você pode fazê-lo usando o Windows PowerShell.

> [!NOTE]
> Para mais informações sobre como configurar o OneDrive for Business, consulte a documentação do Office, [Configurar o OneDrive for Business no Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

#### Configuração para usuários
Dê essas instruções aos usuários para que eles possam configurar o OneDrive for Business e proteger seus arquivos corporativos por IRM.

1.  No OneDrive, clique no ícone **Configurações** para abrir o menu Configurações e, em seguida, clique em **Conteúdo do Site**.

2.  Passe o mouse sobre o bloco **Documentos**, selecione as reticências (**...**) e, em seguida, clique em **CONFIGURAÇÕES.**

3.  Na página **Configurações**, na seção **Permissões e Gerenciamento**, clique em **Gerenciamento de Direitos de Informação**.

4.  Na página **Configurações de Gerenciamento de Direitos de Informação**, marque a caixa de seleção **Restringir permissões nesta biblioteca no download**, especifique sua opção de nome e uma descrição para as permissões e, opcionalmente, clique em **MOSTRAR OPÇÕES** para configurar opções adicionais e depois clique em **OK**.

    Para obter mais informações sobre as opções de configuração, consulte as instruções em [Aplicar Gerenciamento de Direitos de Informações para uma lista ou biblioteca](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) na documentação do Office.

Como esta configuração confia nos usuários em vez de confiar em um administrador para proteger a biblioteca do OneDrive for Business  por IRM, instrua os usuários sobre os benefícios de proteger seus arquivos e como fazê-lo. Por exemplo, explique que quando compartilham um documento do OneDrive para Empresas, somente as pessoas autorizadas podem acessá-lo com quaisquer restrições que forem configuradas, mesmo se o arquivo é renomeado e copiado em outro lugar.

#### Configurações para administradores
Embora você não possa configurar o IRM para usuários do OneDrive for Business usando o centro de administração do SharePoint, você pode fazê-lo usando o Windows PowerShell. Para ativar o IRM para essas bibliotecas, siga estas etapas:

1.  Baixe e instale o [SDK de componentes do cliente SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Baixe e instale o [Shell de gerenciamento do SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Copie o conteúdo do script a seguir e nomeie o arquivo Set-IRMOnOneDriveForBusiness.ps1 no seu computador.

    *&#42;&#42;Aviso de isenção de responsabilidade&#42;&#42;*: não há suporte para esse script de exemplo em qualquer serviço ou programa de suporte padrão da Microsoft. Esse script de exemplo é fornecido como está sem garantias de qualquer tipo.

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

4.  Examine o script e faça as seguintes alterações:

    1.  Procure `$sharepointAdminCenterUrl` e substitua o valor de exemplo por sua própria URL do centro de administração do SharePoint.

        Você encontrará este valor como a URL base quando for ao centro de administração do SharePoint, e ele terá seguinte formato: https://*&lt;tenant_name&gt;*-admin.sharepoint.com

        Por exemplo, se o nome do locatário for "contoso", então, você deverá especificar: **https://contoso-admin.sharepoint.com**

    2.  Procure `$tenantAdmin` e substitua o valor de exemplo por sua própria conta de administrador global totalmente qualificado para o Office 365.

        Esse valor é o mesmo que você usa para entrar no portal de administrador do Office 365 como o administrador global e tem o seguinte formato: user_name@*&lt;tenant domain name&gt;*.com

        Por exemplo, se o nome de usuário do administrador global do Office 365 for "admin" para o domínio de locatário "contoso.com", você deverá especificar: **admin@contoso.com**

    3.  Procure `$webUrls` e substitua os valores de exemplo pelas URLs da web do OneDrive for Business dos seus usuários, adicionando ou excluindo quantas entradas forem necessárias.

        Como alternativa, consulte os comentários no script sobre como substituir essa matriz através da importação de um arquivo .CSV que contenha todas as URLs que você precisa configurar.  Fornecemos outro script de amostra para pesquisar automaticamente e extrair as URLs para preencher este arquivo .CSV. Quando você estiver pronto para fazer isso, expanda a seção [Script adicional para enviar todas as URLs do OneDrive for Business para um arquivo .CSV](#BKMK_Script_OD4B_URLS) imediatamente após estas etapas.

        A URL da Web do OneDrive for Business do usuário tem o seguinte formato: https://*&lt;tenant name&gt;*-my.sharepoint.com/personal/*&lt;user_name&gt;*_*&lt;tenant name&gt;*_com

        Por exemplo, se o usuário no locatário contoso tiver um nome de usuário de "rsimone", você deverá especificar: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

    4.  Visto que estamos usando o script para configurar o OneDrive for Business, não altere o valor de **Documentos** para a variável `$listTitle`.

    5.  Pesquise por `ADMIN INSTRUCTIONS`. Se você não fizer nenhuma alteração nesta seção, o OneDrive for Business do usuário será configurado para IRM com o título de política "Arquivos Protegidos" e a descrição "Esta política restringe o acesso a usuários autorizados".  Nenhuma outra opção de IRM será definida, o que provavelmente é apropriado para a maioria dos ambientes. No entanto, você poderá mudar o título da política e a descrição sugeridos e também adicionar outras opções de IRM que sejam apropriadas para seu ambiente. Consulte o exemplo comentado no script para ajudá-lo a construir seu próprio conjunto de parâmetros para o comando Set-IrmConfiguration.

5.  Salve o script e assine-o. Se você não assinar o script (mais seguro), o Windows PowerShell deverá ser configurado em seu computador para executar scripts não assinados. Por exemplo, inicie uma sessão do Windows PowerShell com a opção **Executar como Administrador** e, em seguida, digite: **Set-ExecutionPolicy Unrestricted**. No entanto, essa configuração permite que todos os scripts não assinados sejam executados (menos seguro).

    Para mais informações sobre a assinatura de scripts do Windows PowerShell, consulte [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) na biblioteca de documentação do PowerShell.

6.  Execute o script e, se solicitado, forneça a senha para a conta de administrador do Office 365. Se você modificar o script e executá-lo na mesma sessão do Windows PowerShell, você não receberá uma solicitação para inserir suas credenciais.

> [!TIP]
> Você também poderá usar este script para configurar o IRM para uma biblioteca do SharePoint Online. Para essa configuração, você provavelmente desejará habilitar a opção adicional **Não permitir que os usuários carreguem documentos sem suporte ao IRM** para garantir que a biblioteca contenha somente documentos protegidos.    Para isso, adicione o parâmetro `-IrmReject` ao comando Set-IrmConfiguration no script.
>
> Você também precisará modificar a variável `$webUrls` (por exemplo, **https://contoso.sharepoint.com**) e a `$listTitle` variável (por exemplo, **$Reports**).

Se você precisar desabilitar o IRM para as bibliotecas do OneDrive for Business do usuário, consulte a seção [Script para desabilitar o IRM para OneDrive for Business](#script-to-disable-irm-for-onedrive-for-business).

##### Script adicional para fornecer todas as URLs do OneDrive for Business em um arquivo .CSV
Para a etapa 4c acima, você poderá usar o seguinte script do Windows PowerShell para extrair as URLs para todas as bibliotecas de usuários do OneDrive for Business, as quais você poderá, então, conferir, editar, se necessário, e depois importar para o script principal.

Este script também requer o [SDK do SharePoint Online Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=42038) e o [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Siga as mesmas instruções para copiá-lo e colá-lo, salve o arquivo localmente (por exemplo, "Report-OneDriveForBusinessSiteInfo.ps1"), modifique os valores `$sharepointAdminCenterUrl` e `$tenantAdmin` como antes e, em seguida, execute o script.

*&#42;&#42;Aviso de isenção de responsabilidade&#42;&#42;*: não há suporte para esse script de exemplo em qualquer serviço ou programa de suporte padrão da Microsoft. Esse script de exemplo é fornecido como está sem garantias de qualquer tipo.

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

##### Script para desativar o IRM do OneDrive for Business
Use o seguinte script de amostra se você precisar desativar o IRM do OneDrive for Business para usuários.

Este script também requer o [SDK do SharePoint Online Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=42038) e o [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Copie e cole o conteúdo, salve o arquivo localmente (por exemplo,"Disable-IRMOnOneDriveForBusiness.ps1") e modifique os valores `$sharepointAdminCenterUrl` e `$tenantAdmin`. Especifique as URLs do OneDrive for Business manualmente ou use o script na seção anterior para que você possa importá-las e, em seguida, execute o script.

*&#42;&#42;Aviso de isenção de responsabilidade&#42;&#42;*: não há suporte para esse script de exemplo em qualquer serviço ou programa de suporte padrão da Microsoft. Esse script de exemplo é fornecido como está sem garantias de qualquer tipo.

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



<!--HONumber=Apr16_HO4-->


