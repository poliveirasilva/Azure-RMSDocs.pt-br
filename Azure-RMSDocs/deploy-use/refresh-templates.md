---
# required metadata

title: Atualizar modelos | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Atualizando modelos para usuários
Ao usar o Azure RMS, os modelos são baixados automaticamente para os computadores clientes para que os usuários possam selecioná-los em seus aplicativos. No entanto, talvez seja necessário tomar medidas adicionais se forem feitas alterações nos modelos:

|Aplicativo ou serviço|Como os modelos são atualizados após as alterações|
|--------------------------|---------------------------------------------|
|Exchange Online|Configuração manual necessária para atualizar os modelos.<br /><br />Para as etapas de configuração, consulte a seção a seguir, [Exchange Online somente: como configurar o Exchange para baixar modelos personalizados alterados](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates).|
|Office 365|Atualizado automaticamente, não são necessários outros procedimentos.|
|Office 2016 e Office 2013<br /><br />Aplicativo de compartilhamento RMS para Windows|Atualizado automaticamente, por agendamento:<br /><br />Para essas versões posteriores do Office: o intervalo de atualização padrão é a cada 7 dias.<br /><br />Para o aplicativo RMS sharing para Windows: da versão 1.0.1784.0 em diante, o intervalo de atualização padrão é a cada 1 dia. As versões anteriores têm um intervalo de atualização padrão de a cada 7 dias.<br /><br />Para forçar uma atualização antes desse agendamento, expanda a seção a seguir, [Aplicativo RMS sharing para Windows, Office 2013 e Office 2016: como forçar uma atualização de um modelo personalizado alterado](#office-2016-office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Atualizado quando os usuários fazem logon.<br /><br />Para forçar uma atualização, peça ou force os usuários a fazerem logoff e logon novamente. Ou consulte a seção a seguir: [Somente Office 2010: como forçar uma atualização para um modelo personalizado alterado](#office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template).|
Para dispositivos móveis que usam o aplicativo RMS sharing, os modelos são baixados (e atualizados, se necessário) automaticamente sem configuração adicional necessária.

## Somente Exchange Online: como configurar o Exchange para baixar modelos personalizados alterados
Se você já configurou o IRM (Gerenciamento de Direitos de Informação) para o Exchange Online, os modelos personalizados não serão baixados para os usuários até que as alterações a seguir sejam feitas usando o Windows PowerShell no Exchange Online.

> [!NOTE]
> Para obter mais informações sobre como usar o Windows PowerShell no Exchange Online, consulte [Usar o PowerShell com o Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Esse procedimento deve ser feito cada vez que um modelo for alterado.

### Para atualizar modelos para o Exchange Online

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

## Office 2016, Office 2013 e aplicativo RMS sharing para Windows: como forçar uma atualização de um modelo personalizado alterado
Editando o registro nos computadores que executam o Office 2016, o Office 2013 ou o aplicativo Rights Management (RMS) sharing para Windows, você pode alterar o agendamento automático para que os modelos alterados sejam atualizados em computadores com mais frequência do que seus valores padrão. Você também pode forçar uma atualização imediata excluindo os dados existentes em um valor de registro.

> [!WARNING]
> Se o Editor de Registro for usado de forma incorreta, podem ocorrer problemas graves que podem exigir a reinstalação do sistema operacional. A Microsoft não garante que seja possível solucionar problemas resultantes do uso incorreto do Editor de Registro. Use o Editor de Registro por sua conta e risco.

### Para alterar o agendamento automático

1.  Ao utilizar um editor de registro, crie e defina um dos seguintes valores de registro:

    - Para definir uma frequência de atualização em dias (mínimo de 1 dia):  Crie um novo valor de registro denominado **TemplateUpdateFrequency** e defina um valor inteiro para os dados que especifica a frequência em dias para baixar todas as alterações para um modelo baixado. Use a tabela a seguir para localizar o caminho do registro para criar esse novo valor de registro.

        **Caminho de Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valor:** TemplateUpdateFrequency


    - To set an update frequency in seconds (minimum of 1 second):  Create a new registry value named **TemplateUpdateFrequencyInSeconds** and define an integer value for the data, which specifies the frequency in seconds to download any changes to a downloaded template. Use the following table to locate the registry path to create this new registry value.

        **Registry path:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type:** REG_DWORD

        **Value:** TemplateUpdateFrequencyInSeconds

    Make sure that you create and set one of these registry values, not both. If both are present, **TemplateUpdateFrequency** is ignored.

2.  Se você quiser forçar uma atualização imediata dos modelos, vá para o próximo procedimento. Caso contrário, reinicie seus aplicativos do Office e instâncias do Explorador de arquivos agora.

### Para forçar uma atualização imediata

1.  Usando um editor de registro, exclua os dados do valor **LastUpdatedTime** . Por exemplo, os dados poderão exibir **2015-04-20T15:52**; exclua 2015-04-20T15:52 para que nenhum dado seja exibido. Use as informações a seguir para localizar o caminho do Registro de forma a excluir esses dados de valor de registro.

    **Caminho de Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **Tipo:** REG_SZ

    **Valor:** LastUpdatedTime

    > [!TIP]
        > No caminho do Registro, <*MicrosoftRMS_FQDN*> refere-se ao FQDN do serviço Microsoft RMS. Se você quiser verificar este valor:

    > 1.  Execute o cmdlet [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS. Se você ainda não instalou o módulo do Windows PowerShell para o Azure RMS, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).
    > 2.  A partir da saída, identifique o valor **LicensingIntranetDistributionPointUrl**
    > 
    >     Por exemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  No valor, remova **https://** e **/_wmcs/licensing** dessa cadeia de caracteres. O valor restante é o FQDN do serviço Microsoft RMS. Em nosso exemplo, o FQDN do serviço Microsoft RMS seria o seguinte valor:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Exclua a seguinte pasta e todos os arquivos que ela contém: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie seus aplicativos do Office e instâncias do Explorador de arquivos.

## Somente Office 2010: como forçar uma atualização de um modelo personalizado alterado
Ao editar o registro nos computadores que executam o Office 2010, você pode definir um valor para que os modelos alterados sejam atualizados em computadores sem esperar que os usuários façam logoff e logon novamente. Você também pode forçar uma atualização imediata excluindo os dados existentes em um valor de registro.

> [!WARNING]
> Se o Editor de Registro for usado de forma incorreta, podem ocorrer problemas graves que podem exigir a reinstalação do sistema operacional. A Microsoft não garante que seja possível solucionar problemas resultantes do uso incorreto do Editor de Registro. Use o Editor de Registro por sua conta e risco.

### Para alterar a frequência de atualização

1.  Usando um editor de registro, crie um novo valor de registro denominado **UpdateFrequency** e defina um valor inteiro para os dados que especifica a frequência em dias para baixar todas as alterações para um modelo baixado. Use a tabela a seguir para localizar o caminho do registro para criar esse novo valor de registro.

    **Caminho de Registro:** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **Tipo:** REG_DWORD

    **Valor:** UpdateFrequency

2.  Se você quiser forçar uma atualização imediata dos modelos, vá para o próximo procedimento. Caso contrário, reinicie os aplicativos do Office agora.

### Para forçar uma atualização imediata

1.  Usando um editor de registro, exclua os dados do valor **LastUpdatedTime** . Por exemplo, os dados poderão exibir **2015-04-20T15:52**; exclua 2015-04-20T15:52 para que nenhum dado seja exibido. Use a tabela a seguir para localizar o caminho do registro de forma a excluir esses dados de valor de registro.

    **Caminho de Registro:** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **Tipo:** REG_SZ

    **Valor:** lastUpdatedTime


2.  Exclua a seguinte pasta e todos os arquivos que ela contém: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie seus aplicativos do Office.

## Consulte também
[Configurar modelos personalizados do Azure Rights Management](configure-custom-templates.md)

<!--HONumber=Apr16_HO3-->


