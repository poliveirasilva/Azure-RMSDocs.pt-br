---
title: "Configurações de Registro para o conector RMS | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 935c354f9bcd3be23a953cdeb08c7860257637d6
ms.openlocfilehash: 5099a10a183f1c78595794511654226265e740c8


---


# Configurações de Registro para o conector do Rights Management

*Aplica-se a: Azure Rights Management, Office 365*


Use as tabelas das seções a seguir apenas se quiser adicionar manualmente ou verificar as configurações do Registro nos servidores que executam o Exchange, SharePoint ou Windows Server, que configuram os servidores para usar o [conector RMS](deploy-rms-connector.md). O método recomendado para configurar esses servidores é usar a ferramenta de configuração do servidor para o conector Microsoft RMS.

Instruções para quando você usar essas configurações:

-   *MicrosoftRMSURL* é a URL de serviço do Microsoft RMS da sua organização. Para encontrar esse valor:

    1.  Execute o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para o Azure RMS. Se você ainda não instalou o módulo do Windows PowerShell para o Azure RMS, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

    2.  A partir da saída, identifique o valor **LicensingIntranetDistributionPointUrl**

        Por exemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  No valor, remova **/_wmcs/licensing** desta cadeia de caracteres. A cadeia de caracteres restante é sua URL do Microsoft RMS. No nosso exemplo, a URL do Microsoft RMS teria o seguinte valor:

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

-   *ConnectorFQDN* é o nome de balanceamento de carga que você definiu no DNS para o conector. Por exemplo, **rmsconnector.contoso.com**.

-   Use o prefixo HTTPS para a URL de conector se você tiver configurado o conector para usar HTTPS para se comunicar com os servidores locais. Para obter mais informações, consulte a seção [Configurando o conector RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https) das instruções principais. As URLs do Microsoft RMS sempre usam HTTPS.


## Configurações de Registro do Exchange 2016 ou Exchange 2013

**Caminho de Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Caminho do Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*


**Dados:** um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*


**Dados:** um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Configurações de Registro do Exchange 2010

**Caminho de Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** https://*MicrosoftRMSURL*/_wmcs/certification

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** https://*MicrosoftRMSURL*/_wmcs/Licensing

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*

**Dados:** um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*

**Dados:** um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://*ConnectorFQDN*

- https://*ConnectorFQDN*


## Tabela para configurações de registro do SharePoint 2016 ou SharePoint 2013

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**Tipo:** Reg_SZ

**Valor:** https://*MicrosoftRMSURL*/_wmcs/licensing


**Dados:** uma das seguintes opções, dependendo da utilização de HTTP ou HTTPS do servidor do SharePoint para o conector RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** uma das seguintes opções, dependendo da utilização de HTTP ou HTTPS do servidor do SharePoint para o conector RMS:

- http://*ConnectorFQDN*/_wmcs/certification

- https://*ConnectorFQDN*/_wmcs/certification

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** padrão


**Dados:** uma das seguintes opções, dependendo da utilização de HTTP ou HTTPS do servidor do SharePoint para o conector RMS:

- http://*ConnectorFQDN*/_wmcs/licensing

- https://*ConnectorFQDN*/_wmcs/licensing




## Configurações de Registro da Infraestrutura de Classificação de Arquivos e servidor de arquivo

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** http://*ConnectorFQDN*/_wmcs/licensing

---

**Caminho de Registro:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**Tipo:** Reg_SZ

**Valor:** padrão

**Dados:** http://*ConnectorFQDN*/_wmcs/certification


Volte para [Implantando o conector do Azure Rights Management](deploy-rms-connector.md)


<!--HONumber=Jul16_HO3-->


