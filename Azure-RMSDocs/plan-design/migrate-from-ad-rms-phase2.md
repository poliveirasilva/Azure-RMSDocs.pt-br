---
title: "Migração do AD RMS para o Azure Rights Management - Fase 2 | Azure RMS"
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
# Fase de migração 2 - configuração do lado do cliente

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*

Use as informações a seguir para a Fase 2 da migração do AD RMS para o Azure RMS (Azure Rights Management). Esses procedimentos abrangem a etapas 5 de [Migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Etapa 5. Reconfigurar clientes para usar o Azure RMS
Para clientes Windows:

1.  [Baixe os scripts de migração](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Esses scripts redefinem a configuração em computadores com Windows para que os mesmos usem o serviço do Azure RMS em vez do AD RMS.

2.  Siga as instruções no script de redirecionamento (Redirect_OnPrem.cmd) modificando-o para apontar para o novo locatário do Azure RMS.

    > [!IMPORTANT]
    > As instruções incluem a substituição dos endereços de exemplo de **adrms** e **adrms.contoso.com** pelos endereços dos seus próprios servidores do AD RMS. Quando você fizer isso, certifique-se de que não há nenhum espaço adicional antes ou depois dos seus endereços, o que interromperá o script de migração e é muito difícil identificar como a causa raiz do problema. Algumas ferramentas de edição adicionam automaticamente um espaço depois de colar o texto.

3. Se os usuários tiverem o Office 2016: os scripts ainda não foram atualizados para incluir a configuração do Office 2016, portanto, se os usuários tiverem essa versão do Office, você deverá atualizar manualmente os scripts:

    - Para **CleanUpRMS.cmd** - pesquise pela linha `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` e imediatamente abaixo dela, adicione a seguinte linha:

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - Para **Redirect_Onprem.cmd** - pesquise pela linha `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F1` e imediatamente abaixo dela, adicione as duas linhas seguintes:

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    Opcional: os scripts não fazem referência ao Office 2016 nos comentários. Se você deseja atualizar os comentários para refletir essas adições para o Office 2016, faça as seguintes alterações em **Redirect_Onprem**:

    - Pesquise por `::     or MSIPC (Office 2013) with on-premises AD RMS` e substitua-o pelo seguinte:
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - Pesquise por `echo Redirect SCP for Office 2013` e substitua-o pelo seguinte:
    
            echo Redirect SCP for Office versions based on MSIPC

    - Pesquise por `echo Redirect MSIPC for Office 2013` e substitua pelo seguinte:
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  Nos com computadores Windows:

    - Execute esses scripts com privilégios elevados no contexto do usuário.

    Para clientes de dispositivos móveis e computadores Mac:

    -  Remova os registros SRV do DNS criados quando você implantou a [extensão de dispositivos móveis AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### Alterações feitas pelos scripts de migração
Esta seção documenta as alterações feitas pelos scripts de migração. Use essas informações apenas para referência, para solucionar problemas ou, se preferir, para fazer essas alterações por conta própria.

CleanUpRMS_RUN_Elevated.cmd:

-   Exclua o conteúdo das pastas %userprofile%\AppData\Local\Microsoft\DRM e %userprofile%\AppData\Local\Microsoft\MSIPC, incluindo todas as subpastas e todos os arquivos com nomes de arquivo longos.

-   Exclua o conteúdo das seguintes chaves de registro:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Adicione os seguintes valores de registro:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Crie os seguintes valores de registro para cada URL fornecida como um parâmetro em cada um destes locais:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Cada entrada tem um valor REG_SZ de **https://OldRMSserverURL/_wmcs/licensing** com os dados no seguinte formato: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* tem o seguinte formato: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Por exemplo, 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Você pode encontrar esse valor por meio da identificação do valor **RightsManagementServiceId** quando você executar o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS.


## Próximas etapas
Para continuar a migração, vá para [fase 3 -configuração de serviços de suporte](migrate-from-ad-rms-phase3.md).


<!--HONumber=Jul16_HO3-->


