---
# required metadata

title: Migração do AD RMS para o Azure Rights Management - Fase 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Fase de migração 2 - configuração do lado do cliente
Use as informações a seguir para a Fase 2 da migração do AD RMS para o Azure RMS (Azure Rights Management). Esses procedimentos abrangem a etapas 5 de [Migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Etapa 5. Reconfigurar clientes para usar o Azure RMS
Para clientes Windows:

1.  [Baixe os scripts de migração](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Esses scripts redefinem a configuração em computadores com Windows para que os mesmos usem o serviço do Azure RMS em vez do AD RMS.

2.  Siga as instruções no script de redirecionamento (Redirect_OnPrem.cmd) modificando-o para apontar para o novo locatário do Azure RMS.

3.  Nos computadores Windows, execute esses scripts com privilégios elevados no contexto do usuário.

Para clientes de dispositivos móveis e computadores Mac:

-   Remova os registros SRV do DNS criados quando você implantou a [extensão de dispositivos móveis AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

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

-   Exclua os seguintes valores de registro:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   Crie os seguintes valores de registro para cada URL fornecida como um parâmetro em cada um destes locais:

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Cada entrada tem um valor REG_SZ de **https://OldRMSserverURL/_wmcs/licensing** com dados no seguinte formato: **https://&lt;YourTenantURL&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* tem o seguinte formato: **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Por exemplo, 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Você pode encontrar esse valor por meio da identificação do valor **RightsManagementServiceId** quando você executar o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS.


## Próximas etapas
Para continuar a migração, vá para [fase 3 -configuração de serviços de suporte](migrate-from-ad-rms-phase3.md).

<!--HONumber=Apr16_HO3-->


