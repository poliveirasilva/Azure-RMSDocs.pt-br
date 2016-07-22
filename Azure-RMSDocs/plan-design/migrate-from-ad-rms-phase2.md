---
title: "Migrar do AD RMS para o Azure Rights Management – Fase 2 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/23/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a9dc45fb5146b0a4d2f013bff9d090723ce95ee5
ms.openlocfilehash: 1016ecdd77e818840f2a2cfab8212e908291bb89


---
# Fase 2 da migração – configuração do lado do cliente

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*

Utilize as seguintes informações para a Fase 2 da migração do AD RMS para o Azure Rights Management (Azure RMS). Estes procedimentos incluem o passo 5 do tópico [Migrar do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passo 5. Reconfigurar clientes para utilizarem o Azure RMS
Para clientes Windows:

1.  [Transfira os scripts de migração](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Estes scripts repõem a configuração em computadores Windows para que utilizem o serviço do Azure RMS em vez do AD RMS.

2.  Siga as instruções no script de redirecionamento (Redirect_OnPrem.cmd) para modificar o script para apontar para o novo inquilino do Azure RMS.

    > [!IMPORTANT]
    > As instruções incluem substituir endereços de exemplo de **adrms** e **adrms.contoso.com** pelos endereços dos seus próprios servidores AD RMS. Ao fazê-lo, certifique-se de que não existem sem espaços adicionais antes ou depois dos endereços, uma vez que estes interrompem o script de migração e são muito difícil identificar como a causa de raiz do problema. Algumas ferramentas de edição adicionam automaticamente um espaço depois do texto colado.

3. Se os utilizadores tiverem o Office 2016: os scripts não foram ainda atualizados para incluir a configuração para o Office 2016, pelo que se os utilizadores tiverem esta versão do Office, têm de atualizar manualmente os scripts:

    - Para **CleanUpRMS.cmd** - procure a linha `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` e, imediatamente abaixo desta, adicione a seguinte linha:

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - Para **Redirect_Onprem.cmd** - procure a linha `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F1` e, imediatamente abaixo desta, adicione a seguinte linha:

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    Opcional: os scripts não mencionam o Office 2016 nos comentários. Se quiser atualizar os comentários para refletir estas adições do 2016 do Office, altere **Redirect_Onprem.cmd** da seguinte forma:

    - Procure `::     or MSIPC (Office 2013) with on-premises AD RMS` e substitua por:
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - Procure `echo Redirect SCP for Office 2013` e substitua por:
    
            echo Redirect SCP for Office versions based on MSIPC

    - Procure `echo Redirect MSIPC for Office 2013` e substitua por:
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  Em computadores com o Windows:

    - Execute estes scripts com privilégios elevados no contexto do utilizador.

    Para clientes de dispositivos móveis e computadores Mac:

    -  Remova os registos SRV de DNS que criou quando implementou a [extensão de dispositivo móvel do AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### Alterações efetuadas pelos scripts de migração
Esta secção documenta as alterações que os scripts de migração efetuam. Pode utilizar estas informações apenas para efeitos de referência, para resolução de problemas ou para o caso de preferir efetuar estas alterações sozinho.

CleanUpRMS_RUN_Elevated.cmd:

-   Elimine o conteúdo das pastas %userprofile%\AppData\Local\Microsoft\DRM e %userprofile%\AppData\Local\Microsoft\MSIPC, incluindo quaisquer subpastas e ficheiros com nomes de ficheiro longos.

-   Elimine o conteúdo das seguintes chaves de registo:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Adicione os seguintes valores de registo:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Crie os seguintes valores do registo para cada URL fornecido como um parâmetro em cada uma das seguintes localizações:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Cada entrada tem um valor REG_SZ de **https://OldRMSserverURL/_wmcs/licensing** com os dados no seguinte formato: **https://&lt;URLdeInquilino&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;URLdeInquilino&gt;* tem o seguinte formato: **{GUID}.rms.[Região].aadrm.com**.
    > 
    > Por exemplo: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Pode encontrar este valor ao identificar o valor **RightsManagementServiceId** quando executar o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) do Azure RMS.


## Passos seguintes
Para continuar a migração, consulte a [fase 3 – suportar a configuração de serviços](migrate-from-ad-rms-phase3.md).


<!--HONumber=Jul16_HO2-->


