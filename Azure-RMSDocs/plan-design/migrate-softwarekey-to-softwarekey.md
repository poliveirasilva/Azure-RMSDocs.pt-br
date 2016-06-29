---
# required metadata

title: Passo 2&colon; Migração de chave protegida por software para chave protegida por software | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Passo 2: migração de chave protegida por software para chave protegida por software

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*


Estas instruções fazem parte do [caminho de migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e são aplicáveis apenas se a sua chave de AD RMS estiver protegida por software e pretender migrar para o Azure Rights Management com uma chave de inquilino protegida por software. 

Se este não for o cenário de configuração escolhido, volte ao [Passo 2. Exporte os dados de configuração do AD RMS, importe-os para o Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) e escolha uma configuração diferente.

Utilize o seguinte procedimento para importar a configuração do AD RMS para o Azure RMS, que resultará na sua chave de inquilino do Azure RMS que é gerida pela Microsoft.

## Para importar os dados de configuração para o Azure RMS

1.  Numa estação de trabalho com ligação à Internet, transfira e instale o módulo do Windows PowerShell para o Azure RMS (versão mínima 2.1.0.0), que inclui o cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Se já transferiu e instalou o módulo anteriormente, verifique o número da versão ao executar: `(Get-Module aadrm -ListAvailable).Version`

    Para obter instruções de instalação, consulte [Instalar o Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

2.  Inicie o Windows PowerShell com a opção **Executar como administrador** e utilize o cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) para efetuar uma ligação ao serviço do Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando for solicitado, introduza as credenciais de administrador de inquilinos do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, utilizará uma conta de um administrador global do Azure Active Directory ou do Office 365).

3.  Utilize o cmdlet [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) para carregar o primeiro ficheiro de domínio de publicação fidedigno exportado (.xml). Se tiver mais do que um ficheiro .xml, porque tinha vários domínios de publicação fidedignos, escolha o ficheiro que contém o domínio de publicação fidedigno exportado que pretende utilizar no Azure RMS para proteger conteúdo após a migração. Utilize o seguinte comando:

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Por exemplo: **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Quando for solicitado, introduza a palavra-passe que especificou anteriormente e confirme que pretende efetuar esta ação.

4.  Quando o comando for concluído, repita o passo 3 para cada ficheiro .xml restante que criou ao exportar os seus domínios de publicação fidedignos. No entanto, para esses ficheiros, defina **-Active** para **false** ao executar o comando Import. Por exemplo: **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Utilize o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) para desligar do serviço do Azure RMS:

    ```
    Disconnect-AadrmService
    ```

Agora, está pronto para ir para o [Passo 3. Ativar o inquilino do RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO4-->


