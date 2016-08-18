---
title: "Etapa 2&colon; Migração de chave protegida por software para chave protegida por software | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bb152f428c8e0b9a065035aaad2de6353265a562
ms.openlocfilehash: a739da3fbebc8dfa4c6715fd64ccd72f87d2a686


---


# Etapa 2: Migração de chave protegida por software para chave protegida por software

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*


Estas instruções fazem parte do [caminho de migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e são aplicáveis somente se a chave do AD RMS é protegida por software e se você deseja migrar para o Azure Rights Management com uma chave de locatário protegida por software. 

Se este não for o cenário de configuração escolhido, volte para a [Etapa 2. Exporte os dados de configuração do AD RMS e importe-os para o Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) e escolha uma configuração diferente.

Use o seguinte procedimento para importar a configuração do AD RMS para o Azure RMS, para resultar na sua chave de locatário do Azure RMS gerenciada pela Microsoft.

## Para importar os dados de configuração para o Azure RMS

1.  Em uma estação de trabalho conectada à Internet, baixe e instale o módulo do Windows PowerShell para o Azure RMS (versão mínima 2.1.0.0), que inclui o cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Se você tiver baixado e instalado o módulo anteriormente, verifique o número da versão executando: `(Get-Module aadrm -ListAvailable).Version`

    Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2.  Inicie o Windows PowerShell com a opção **Executar como administrador** e use o cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) para conectar-se ao serviço do Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando solicitado, insira suas credenciais de administrador de locatário [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, você usará uma conta que seja um administrador global do Azure Active Directory ou do Office 365).

3.  Use o cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) para carregar o primeiro arquivo de domínio de publicação confiável exportado (.xml). Se você tiver mais de um arquivo. xml porque você tinha vários domínios de publicação confiáveis, escolha o arquivo que contenha o domínio de publicação confiável exportado que você deseja usar no Azure RMS para proteger o conteúdo após a migração. Execute o seguinte comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Por exemplo: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Quando solicitado, digite a senha que você especificou antes e confirme que deseja executar esta ação.

4.  Quando o comando for concluído, repita a etapa 3 para cada arquivo .xml restante que você criou exportando seus domínios de publicação confiáveis. Mas, para esses arquivos, defina **-Active** como **false** ao executar o comando de importação. Por exemplo: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Use o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) para se desconectar do serviço do Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Agora você está pronto para ir para a [Etapa 3. Ativar o seu locatário do RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).




<!--HONumber=Jul16_HO3-->


