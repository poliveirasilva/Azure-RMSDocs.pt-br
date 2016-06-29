---
# required metadata

title: Atualizar modelos | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/06/2016
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


# Atualizar modelos para os utilizadores

*Aplica-se a: Azure Rights Management, Office 365*

Quando utiliza o Azure RMS, os modelos são automaticamente transferidos para computadores cliente para os utilizadores poderem selecioná-los a partir das suas aplicações. No entanto, poderá ter de efetuar passos adicionais se fizer alterações aos modelos:

|Aplicação ou serviço|Como os modelos são atualizados depois das alterações|
|--------------------------|---------------------------------------------|
|Exchange Online|Configuração manual necessária para atualizar os modelos.<br /><br />Para obter os passos de configuração, consulte a secção [Apenas para o Exchange Online: como configurar o Exchange para transferir modelos personalizados modificados](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates)..|
|Office 365|Atualizados automaticamente – não existem passos adicionais necessários.|
|Office 2016 e Office 2013<br /><br />Aplicação de partilha RMS para Windows|Atualizados automaticamente – com base numa agenda:<br /><br />Para estas versões posteriores do Office: o intervalo de atualização predefinido é de 7 dias.<br /><br />Para a aplicação de partilha RMS para Windows: a partir da versão 1.0.1784.0, o intervalo de atualização predefinido é de 1 dia. As versões anteriores têm um intervalo de atualização predefinido de 7 dias.<br /><br />Para forçar uma atualização mais cedo do que a agendada, consulte a secção [Office 2016, Office 2013 e aplicação de partilha RMS para Windows: como forçar uma atualização de um modelo personalizado modificado](#office-2016-office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Atualizado quando os utilizadores iniciam sessão.<br /><br />Para forçar uma atualização, peça ou force os utilizadores a terminarem e a iniciarem a sessão novamente. Em alternativa, consulte a secção [Apenas para Office 2010: como forçar uma atualização de um modelo personalizado modificado](#office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template).|
Para dispositivos móveis que utilizam a aplicação de partilha RMS, os modelos são automaticamente transferidos (e atualizados se necessário) sem ser necessária uma configuração adicional.

## Apenas para Exchange Online: como configurar o Exchange para transferir modelos personalizados modificados
Se já tiver configurado a Gestão de Direitos de Informação (IRM) para o Exchange Online, os utilizadores não poderão transferir os modelos personalizados até fazer as seguintes alterações com o Windows PowerShell no Exchange Online.

> [!NOTE]
> Para mais informações sobre como utilizar o Windows PowerShell no Exchange Online, consulte [Utilizar o PowerShell com o Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Tem de efetuar este procedimento sempre que alterar um modelo.

### Para atualizar modelos para o Exchange Online

1.  Com o Windows PowerShell no Exchange Online, ligue-se ao serviço:

    1.  Forneça o nome de utilizador e a palavra-passe do Office 365:

        ```
        $Cred = Get-Credential
        ```

    2.  Execute os dois comandos seguintes para ligar ao serviço do Exchange Online:

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Utilize o cmdlet [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) para voltar a importar o domínio de publicação fidedigno (TPD) do Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Por exemplo, se o nome TPD for **RMS Online – 1** (nome típico para muitas organizações), introduza: **Import-RMSTrustedPublishingDomain -Name "RMS Online – 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Para verificar o seu nome TPD, pode utilizar o cmdlet [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx).

3.  Para confirmar que os modelos foram importados com êxito, aguarde alguns minutos e, em seguida, execute o cmdlet [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) e defina o Tipo para Todos. Por exemplo:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > É útil guardar uma cópia do ficheiro de saída para poder copiar facilmente os nomes dos modelos ou os GUIDs se arquivar um modelo posteriormente.

4.  Para cada modelo importado que pretenda disponibilizar no Outlook Web App, tem de utilizar o cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) e definir o Tipo para Distribuído:

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Como o Outlook Web Access coloca a IU em cache durante 24 horas, os utilizadores não poderão ver o novo modelo até ao dia seguinte.

Além disso, se arquivar um modelo (personalizado ou predefinido) e utilizar o Exchange Online com o Office 365, os utilizadores irão continuar a ver os modelos arquivados se utilizarem o Outlook Web App ou os dispositivos móveis que utilizam o Protocolo do Exchange ActiveSync.

Para os utilizadores deixarem de ver estes modelos, ligue-se ao serviço com o Windows PowerShell no Exchange Online e, em seguida, utilize o cmdlet [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) ao executar o seguinte comando:

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

## Office 2016, Office 2013 e aplicação de partilha RMS para Windows: como forçar uma atualização de um modelo personalizado modificado
Ao editar o registo nos computadores ao executar o Office 2016, Office 2013 ou a aplicação de partilha Rights Management (RMS) para Windows, pode alterar o agendamento automático para os modelos modificados serem atualizados nos computadores com mais frequência do que o respetivo valor predefinido. Também pode forçar uma atualização imediata ao eliminar os dados existentes num valor de registo.

> [!WARNING]
> A utilização incorreta do Editor de Registo poderá causar problemas graves que exijam a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.

### Para alterar o agendamento automático

1.  Através de um editor de registo, crie e defina um dos seguintes valores do registo:

    - Para definir uma frequência de atualização em dias (mínimo de 1 dia): crie um novo valor de registo com o nome **TemplateUpdateFrequency** e defina um valor inteiro para os dados, que especifica a frequência em dias para transferir quaisquer alterações a um modelo transferido. Utilize as seguintes informações para localizar o caminho do registo para criar este novo valor de registo.

        **Caminho do registo:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valor:** TemplateUpdateFrequency

    - Para definir uma frequência de atualização em segundos (mínimo de 1 segundo): crie um novo valor de registo com o nome **TemplateUpdateFrequencyInSeconds** e defina um valor inteiro para os dados, que especifica a frequência em segundos para transferir alterações para um modelo transferido. Utilize as seguintes informações para localizar o caminho do registo para criar este novo valor de registo.

        **Caminho do registo:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valor:** TemplateUpdateFrequencyInSeconds

    Certifique-se de que cria e configura um destes valores do registo, não ambos. Se ambos estiverem presentes, o **TemplateUpdateFrequency** será ignorado.

2.  Se quiser forçar uma atualização imediata dos modelos, avance para o procedimento seguinte. Caso contrário, reinicie as suas aplicações do Office e instâncias do Explorador de Ficheiros agora.

### Para forçar uma atualização imediata

1.  Através de um editor de registo, elimine os dados do valor **LastUpdatedTime**. Por exemplo, os dados poderão apresentar **2015-04-20T15:52**. Elimine 2015-04-20T15:52 para não serem apresentados dados. Utilize as seguintes informações para localizar o caminho do registo para eliminar os dados deste valor de registo.

    **Caminho do registo:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **Tipo:** REG_SZ

    **Valor:** LastUpdatedTime

    > [!TIP]
        > No caminho do registo, *MicrosoftRMS_FQDN*> refere-se ao seu FQDN do serviço Microsoft RMS. Se quiser verificar este valor:

    > 1.  Execute o cmdlet [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS. Se ainda não instalou o módulo do Windows PowerShell para o Azure RMS, consulte [Instalar o Windows PowerShell para o Azure Rights Management](install-powershell.md).
    > 2.  A partir da saída, identifique o valor **LicensingIntranetDistributionPointUrl**.
    > 
    >     Por exemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  No valor, remova **https://** e **/_wmcs/licensing** desta cadeia. O valor restante é o seu FQDN do serviço Microsoft RMS. No nosso exemplo, o FQDN do serviço Microsoft RMS teria o seguinte valor:
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Elimine a seguinte pasta e todos os ficheiros nela contidos: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie as suas aplicações do Office e instâncias do Explorador de Ficheiros.

## Apenas para Office 2010: como forçar uma atualização de um modelo personalizado modificado
Ao editar o registo nos computadores ao executar o Office 2010, pode definir um valor para que os modelos alterados sejam atualizados em computadores sem ter de esperar que os utilizadores terminem sessão e voltem a iniciá-la. Também pode forçar uma atualização imediata ao eliminar os dados existentes num valor de registo.

> [!WARNING]
> A utilização incorreta do Editor de Registo poderá causar problemas graves que exijam a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.

### Para alterar a frequência de atualização

1.  Através de um editor de registo, crie um novo valor de registo com o nome **UpdateFrequency** e defina um valor inteiro para os dados, que especifica a frequência em dias para transferir alterações para um modelo transferido. Utilize a seguinte tabela para localizar o caminho do registo para criar este novo valor de registo.

    **Caminho do registo:** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **Tipo:** REG_DWORD

    **Valor:** UpdateFrequency

2.  Se quiser forçar uma atualização imediata dos modelos, avance para o procedimento seguinte. Caso contrário, reinicie as aplicações do Office agora.

### Para forçar uma atualização imediata

1.  Através de um editor de registo, elimine os dados do valor **LastUpdatedTime**. Por exemplo, os dados poderão apresentar **2015-04-20T15:52**. Elimine 2015-04-20T15:52 para não serem apresentados dados. Utilize a seguinte tabela para localizar o caminho do registo para eliminar os dados deste valor de registo.

    **Caminho do registo:** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **Tipo:** REG_SZ

    **Valor:** lastUpdatedTime


2.  Elimine a seguinte pasta e todos os ficheiros nela contidos: **%localappdata%\Microsoft\MSIPC\Templates**

3.  Reinicie as aplicações do Office.

## Consulte Também
[Configurar modelos personalizados para o Azure Rights Management](configure-custom-templates.md)

<!--HONumber=May16_HO1-->


