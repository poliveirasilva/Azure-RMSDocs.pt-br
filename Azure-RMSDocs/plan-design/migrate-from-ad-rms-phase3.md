---
title: "Migração do AD RMS para o Azure Rights Management - Fase 3 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 75cce1d0e5a1cff0d4f6609d0f084fda1af62951


---

# Fase de migração 3 - suporte da configuração de serviços

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management*


Use as informações a seguir para a Fase 3 da migração do AD RMS para o Azure RMS (Azure Rights Management). Esses procedimentos abrangem as etapas 6 a 7 de [Migração do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Etapa 6. Configurar a integração do IRM com o Exchange Online

Se tiver importado anteriormente o TDP do AD RMS para o Exchange Online, você deve remover essa TDP para evitar modelos e políticas conflitantes depois de migrar para o Azure RMS. Para fazer isso, use o cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) do Exchange Online.

Se você escolher uma topologia de chave de locatário do Azure RMS que seja **gerida pela Microsoft**:

-   Consulte a seção [Exchange Online: configuração do IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) no artigo [Office 365: configuração de clientes e serviços online](../deploy-use/configure-office365.md). Esta seção inclui comandos típicos para executar que se conectam ao serviço Exchange Online, importam a chave de locatário do Azure RMS e habilitam a funcionalidade do IRM para o Exchange Online. Depois de concluir tais etapas, você terá a funcionalidade completa do RMS com o Exchange Online.

Se você escolher uma topologia de chave de locatário do Azure RMS que seja **gerenciada pelo cliente (BYOK)**:

-   Você terá reduzido uma funcionalidade do RMS com o Exchange Online reduzida, conforme descrito no artigo [Preços e restrições do BYOK](byok-price-restrictions.md).

## Etapa 7. Implantar o conector RMS
Se usou a funcionalidade de Gerenciamento de Direitos de Informação (IRM) do Exchange Server ou do SharePoint Server com o AD RMS, primeiro desative o IRM nesses servidores e remova a configuração do AD RMS. Em seguida, implante o conector do RMS (Rights Management), que atua como uma interface de comunicação (um retransmissor) entre os servidores locais e o Azure RMS.

Por fim, nesta etapa, se importou vários TPDs para o Azure RMS que foram usados para proteger as mensagens de email, edite manualmente o registro nos computadores do Exchange Server para redirecionar todas as URLs de TPDs para o conector RMS.

> [!NOTE]
> Antes de começar, verifique as versões dos servidores locais à quais o Azure RMS dá suporte em [Servidores locais que dão suporte ao Azure RMS](../get-started/requirements-servers.md).

### Desativar o IRM nos Exchange Servers e remover a configuração do AD RMS

1.  Em cada Exchange Server, localize a seguinte pasta e exclua todas as entradas da mesma: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Em um dos Exchange Servers, use o cmdlet [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) do Exchange para primeiro desativar os recursos do IRM para as mensagens enviadas para destinatários internos:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Em seguida, use o mesmo cmdlet para desabilitar recursos do IRM para mensagens enviadas a destinatários externos:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Use o mesmo cmdlet para desabilitar o IRM no Microsoft Office Outlook Web App e dn Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Por fim, use o mesmo cmdlet para limpar todos os certificados armazenados em cache:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  Em cada Exchange Server, redefina então o IIS, por exemplo, executando um prompt de comando como um administrador e digitando **iisreset**.

### Desativar o IRM nos SharePoint Servers e remover a configuração do AD RMS

1.  Certifique-se de que não haja nenhum documento desmarcado das bibliotecas protegidas pelo RMS. Se houver, eles ficarão inacessíveis no final deste procedimento.

2.  No site da Administração Central do SharePoint, na seção **Início Rápido** , clique em **Segurança**.

3.  Na página de **Segurança** na seção **Diretiva de informações** , clique em **Configurar o gerenciamento de direitos de informação**.

4.  Na página de **Gerenciamento de Direitos de Informação** , na seção **Gerenciamento de Direitos de Informação** , selecione **Não usar o IRM neste servidor**e clique em **OK**.

5.  Em cada um dos computadores do SharePoint Server, exclua o conteúdo da pasta \ProgramData\Microsoft\MSIPC\Server\*&lt;SID da conta que está usando o SharePoint Server&gt;*.

#### Instalar e configurar o conector RMS

-   Use as instruções no artigo [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

#### Somente para o Exchange e vários TPDs: Editar o registro

-   Em cada Exchange Server, adicione manualmente as chaves de registro abaixo para cada TPD adicional que você importou para redirecionar as URLs do TPD para o conector RMS. Essas entradas de registro são específicas para a migração e não são adicionadas pela ferramenta de configuração do servidor para o conector Microsoft RMS.

    Ao fazer essas edições de registro, use estas instruções:

    -   Substitua o *ConnectorFQDN* com o nome que você definiu no DNS para o conector. Por exemplo, **rmsconnector.contoso.com**.

    -   Use o prefixo HTTPS ou HTTPS para a URL do conector se você tiver configurado o conector para usar HTTPS ou HTTPS para se comunicar com os servidores locais.

Para o Exchange 2013 - edição de Registro 1:


**Caminho de Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Dados:**

Um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Para o Exchange 2013 - edição de Registro 2:

**Caminho de Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Dados:**

Um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Para o Exchange 2010 - edição de Registro 1:



**Caminho de Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Dados:**

Um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Para o Exchange 2010 - edição de Registro 2:


**Caminho de Registro:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Dados:**

Um dos seguintes, dependendo se você estiver usando HTTP ou HTTPS do servidor Exchange para o conector RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Após concluir esses procedimentos, leia a seção **Próximas etapas** no artigo [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Próximas etapas
Para continuar a migração, vá para [fase 4 - tarefas pós-migração](migrate-from-ad-rms-phase4.md).


<!--HONumber=Jun16_HO4-->


