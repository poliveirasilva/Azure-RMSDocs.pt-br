---
title: "Migrar do AD RMS para o Azure Rights Management – fase 3 | Azure RMS"
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
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 75cce1d0e5a1cff0d4f6609d0f084fda1af62951


---

# Fase 3 da migração – configuração de serviços de suporte

*Aplica-se a: Serviços de Gestão de Direitos do Active Directory, Azure Rights Management*


Utilize as seguintes informações para a Fase 3 da migração do AD RMS para o Azure Rights Management (Azure RMS). Estes procedimentos incluem os passos de 6 a 7 da secção [Migrar do AD RMS para o Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passo 6. Configurar a integração de IRM para o Exchange Online

Se tiver importado anteriormente o TDP do AD RMS para o Exchange Online, tem de remover este TDP para evitar modelos e políticas em conflito após a migração para o Azure RMS. Para tal, utilize o cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) do Exchange Online.

Se optou por uma topologia de chave de inquilino do Azure RMS **gerida pela Microsoft**:

-   Consulte a secção [Exchange Online: configuração da IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) do artigo [Office 365: configuração para clientes e serviços online](../deploy-use/configure-office365.md). Esta secção inclui comandos típicos a executar que ligam ao serviço do Exchange Online, importam a chave de inquilino do Azure RMS e ativam a funcionalidade de IRM para o Exchange Online. Depois de concluir estes passos, terá acesso à funcionalidade integral do RMS com o Exchange Online.

Se optou por uma topologia de chave de inquilino do Azure RMS **gerida pelo cliente (BYOK)**:

-   Terá funcionalidades do RMS reduzidas com o Exchange Online, conforme descrito no artigo [Preços e restrições do BYOK](byok-price-restrictions.md).

## Passo 7. Implementar o conetor RMS
Se tiver utilizado a funcionalidade de Gestão de Direitos de Informação (IRM) do Exchange Server ou o SharePoint Server com o AD RMS, tem primeiro de desativar a IRM nestes servidores e remover a configuração do AD RMS. Em seguida, implemente o conetor Rights Management (RMS), que funciona como uma interface de comunicações (um reencaminhamento) entre os servidores no local e o Azure RMS.

Por fim, para este passo, se tiver importado vários TPD para o Azure RMS que foram utilizados para proteger mensagens de e-mail, tem de editar manualmente o registo nos computadores do Exchange Server para redirecionar todos os URLs de TPD para o conetor RMS.

> [!NOTE]
> Antes de começar, verifique as versões dos servidores no local que o Azure RMS suporta em [Servidores no local que suportam o Azure RMS](../get-started/requirements-servers.md).

### Desativar a IRM nos Servidores do Exchange e remover a configuração do AD RMS

1.  Em cada Exchange Server, localize a pasta seguinte e elimine todas as entradas nessa pasta: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Num dos Exchange Servers, utilize o cmdlet [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) do Exchange para primeiro desativar as funcionalidades de IRM para mensagens enviadas a destinatários internos:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Em seguida, utilize o mesmo cmdlet para desativar as funcionalidades de IRM para mensagens enviadas a destinatários externos:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Em seguida, utilize o mesmo cmdlet para desativar a IRM no Microsoft Office Outlook Web App e no Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Por fim, utilize o mesmo cmdlet para limpar todos os certificados em cache:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  Em cada Exchange Server, reponha o IIS, por exemplo, ao executar uma linha de comandos como administrador e escrever **iisreset**.

### Desativar a IRM em SharePoint Servers e remover a configuração do AD RMS

1.  Certifique-se de que não existem documentos com saída dada em bibliotecas protegidas por RMS. Se existirem, vão tornar-se inacessíveis no final deste procedimento.

2.  No Web site de Administração Central do SharePoint , na secção **Iniciação Rápida**, clique em **Segurança**.

3.  Na página **Segurança**, na secção **Política de Informações**, clique em **Configurar gestão de direitos de informação**.

4.  Na página **Gestão de Direitos de Informação**, na secção **Gestão de Direitos de Informação**, selecione **Não utilizar IRM neste servidor** e, em seguida, clique em **OK**.

5.  Em cada computador do SharePoint Server, elimine o conteúdo da pasta \ProgramData\Microsoft\MSIPC\Server\\*&lt;SID da conta que está a executar o SharePoint Server&gt;*.

#### Instalar e configurar o conetor RMS

-   Utilize as instruções no artigo [Implementar o conetor Azure Rights Management](../deploy-use/deploy-rms-connector.md).

#### Apenas para o Exchange e vários TPD: editar o registo

-   Em cada Exchange Server, adicione manualmente as chaves do registo seguintes para cada TPD adicional que tenha importado para redirecionar os URLs de TPD para o conetor RMS. Estas entradas do registo são específicas da migração e não são adicionadas pela ferramenta de configuração do servidor para o conetor Microsoft RMS.

    Quando efetuar estas edições de registo, utilize as instruções seguintes:

    -   Substitua *ConnectorFQDN* pelo nome que definiu no DNS para o conector. Por exemplo, **rmsconnector.contoso.com**.

    -   Utilize o prefixo HTTP ou HTTPS para o URL do conetor, dependendo se configurou o conetor para utilizar HTTP ou HTTPS para comunicar com os servidores no local.

Para o Exchange 2013 – edição de registo 1:


**Caminho do registo:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Dados:**

Um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange Server para o conetor RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Para o Exchange 2013 – edição de registo 2:

**Caminho do registo:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Dados:**

Um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange Server para o conetor RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Para o Exchange 2010 – edição de registo 1:



**Caminho do registo:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Dados:**

Um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange Server para o conetor RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Para o Exchange 2010 – edição de registo 2:


**Caminho do registo:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**Tipo:**

Reg_SZ

**Valor:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Dados:**

Um dos seguintes, dependendo se está a utilizar HTTP ou HTTPS no Exchange Server para o conetor RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Depois de concluir estes procedimentos, está pronto para ler a secção **Passos seguintes** do artigo [Implementar o conetor Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Passos seguintes
Para continuar a migração, consulte a [fase 4 – tarefas de pós-migração](migrate-from-ad-rms-phase4.md).


<!--HONumber=Jul16_HO2-->


