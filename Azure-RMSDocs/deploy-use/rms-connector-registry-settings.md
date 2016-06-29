---
# required metadata

title: Definições de registo para o conetor RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Definição de registo para o conetor Rights Management

*Aplica-se a: Azure Rights Management, Office 365*


Utilize as tabelas nas secções seguintes apenas se pretender adicionar manualmente ou verificar as definições de registo nos servidores a executar o Exchange, o SharePoint ou o Windows Server, que configura os servidores a utilizar o [conetor RMS](deploy-rms-connector.md). O método recomendado para configurar estes servidores é utilizar a ferramenta de configuração do servidor do conetor Microsoft RMS.

Instruções ao utilizar estas definições:

-   *MicrosoftRMSURL* é o URL do serviço do Microsoft RMS da sua organização. Para localizar este valor:

    1.  Execute o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS. Se ainda não instalou o módulo do Windows PowerShell para o Azure RMS, consulte [Instalar o Windows PowerShell para o Azure Rights Management](install-powershell.md).

    2.  A partir da saída, identifique o valor **LicensingIntranetDistributionPointUrl**.

        Por exemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  No valor, remova **/_wmcs/licensing** desta cadeia. A cadeia restante é o URL do Microsoft RMS. No nosso exemplo, o URL do Microsoft RMS seria o seguinte valor:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* é o nome de balanceamento de carga que definiu no DNS para o conetor. Por exemplo, **rmsconnector.contoso.com**.

-   Utilize o prefixo HTTPS para o URL do conetor se configurou o conetor para utilizar o HTTPS para comunicar com os servidores no local. Para obter mais informações, consulte a secção [Configurar o conetor RMS para utilizar HTTPS](deploy-rms-connector.md#BKMK_ConfiguringHTTPS) deste tópico. Os URLs do Microsoft RMS utilizam sempre HTTPS.


## Definições de registo do Exchange 2016 ou Exchange 2013

**Caminho do registo:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*


**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange server para o conetor RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*


**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange server para o conetor RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Definições de registo do Exchange 2010

**Caminho do registo:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*

**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange server para o conetor RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*

**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange server para o conetor RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Definições de registo do SharePoint 2016 ou SharePoint 2013

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*/_wmcs/licensing


**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no SharePoint server para o conetor RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no SharePoint server para o conetor RMS:

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** predefinido


**Dados:** um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no SharePoint server para o conetor RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## Servidor de ficheiros e definições de registo de Infraestrutura de Classificação de Ficheiros

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** http://*ConnectorFQDN*/_wmcs/licensing

---

**Caminho do registo:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** predefinido

**Dados:** http://*ConnectorFQDN*/_wmcs/certification


Voltar a [Implementar o conetor Azure Rights Management](deploy-rms-connector.md)

<!--HONumber=Apr16_HO4-->


