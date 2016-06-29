---
# required metadata

title: Migrar do AD RMS para o Azure Rights Management – Fase 2 | Azure RMS
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
# Fase 2 da migração – configuração do lado do cliente

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*

Utilize as seguintes informações para a Fase 2 da migração do AD RMS para o Azure Rights Management (Azure RMS). Estes procedimentos incluem o passo 5 do tópico [Migrar do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passo 5. Reconfigurar clientes para utilizarem o Azure RMS
Para clientes Windows:

1.  [Transfira os scripts de migração](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Estes scripts repõem a configuração em computadores Windows para que utilizem o serviço do Azure RMS em vez do AD RMS.

2.  Siga as instruções no script de redirecionamento (Redirect_OnPrem.cmd) para modificar o script para apontar para o novo inquilino do Azure RMS.

3.  Nos computadores Windows, execute estes scripts com privilégios elevados no contexto do utilizador.

Para clientes de dispositivos móveis e computadores Mac:

-   Remova os registos SRV de DNS que criou quando implementou a [extensão de dispositivo móvel do AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### Alterações efetuadas pelos scripts de migração
Esta secção documenta as alterações que os scripts de migração efetuam. Pode utilizar estas informações apenas para efeitos de referência, para resolução de problemas ou para o caso de preferir efetuar estas alterações sozinho.

CleanUpRMS_RUN_Elevated.cmd:

-   Elimine o conteúdo das pastas %userprofile%\AppData\Local\Microsoft\DRM e %userprofile%\AppData\Local\Microsoft\MSIPC, incluindo quaisquer subpastas e ficheiros com nomes de ficheiro longos.

-   Elimine o conteúdo das seguintes chaves de registo:

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Elimine os seguintes valores do registo:

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
Para continuar a migração, consulte a [fase 3 – configuração de serviços de suporte](migrate-from-ad-rms-phase3.md).

<!--HONumber=Apr16_HO4-->


