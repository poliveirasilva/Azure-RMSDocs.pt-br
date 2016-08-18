---
title: Registrando em log e analisando o uso do Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/05/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2082620eb152aa88af4141b88985adce22769168
ms.openlocfilehash: fbf614bf7b30165a78f6312267243ad6fdb81435


---

# Registrando em log e analisando o uso do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use as informações neste tópico para ajudá-lo a entender como usar registro em log com o Azure RMS (Azure Rights Management). O serviço Azure Rights Management pode registrar cada solicitação feita para sua organização, incluindo solicitações de usuários, ações realizadas por administradores do Rights Management na sua organização e ações realizadas por operadores da Microsoft para dar suporte à sua implantação do Azure Rights Management.

Você pode usar esses logs do Azure Rights Management para dar suporte aos cenários de negócios a seguir:

-   **Analisar ideias de negócios**

    Os logs gerados pelo Azure Rights Management podem ser importados em um repositório de sua escolha (como um banco de dados, um sistema de processamento analítico online (OLAP), ou um sistema de redução de mapa). Como um exemplo, você pode identificar quem está acessando seus dados protegidos pelo RMS. Você pode determinar quais dados protegidos pelo RMS as pessoas acessam e de quais dispositivos e de onde. Você pode descobrir se as pessoas podem ler com êxito o conteúdo protegido. Você também pode identificar quais pessoas leram um documento importante que foi protegido.

-   **Monitorar abuso**

    As informações de log do Azure Rights Management estão disponíveis quase em tempo real para que você possa monitorar continuamente o uso do Rights Management por sua empresa. 99.9% dos logs estão disponíveis após 15 minutos de uma ação iniciada pelo RMS.

    Por exemplo, você pode querer se alertado se há um aumento repentino de pessoas lendo os dados protegidos pelo RMS fora das horas de trabalho padrão, que pode indicar que um usuário mal-intencionado está coletando informações para vendê-las a concorrentes. Ou, se o mesmo usuário aparentemente acessa dados de dois endereços de IP diferentes em um intervalo de tempo curto, que pode indicar que uma conta de usuário foi comprometida.

-   **Executar análise forense**

    Se você tiver um vazamento de informação, é provável que seja solicitado quem acessou recentemente documentos específicos e que informações a pessoa suspeitosa acessou recentemente. Você pode responder a esse tipo de pergunta quando usa o Azure Rights Management e o registro em log porque as pessoas que usam o conteúdo protegido sempre devem obter uma licença do Rights Management para abrir documentos e imagens que sejam projetadas pelo Azure Rights Management, mesmo que esses arquivos sejam movidos por email ou copiados para unidades USB ou outros dispositivos de armazenamento. Isso significa que você pode usar os logs do Azure Rights Management como uma fonte definitiva de informações para análise forense ao proteger seus dados usando o Azure Rights Management.

> [!NOTE]
> Se você estiver interessado somente no registro em log de tarefas administrativas para o Azure Rights Management e não quiser controlar como os usuários estão usando o Rights Management, poderá usar o cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) do Windows PowerShell do Azure Rights Management.
> 
> Você também pode usar o portal clássico do Azure para relatórios de uso de alto nível que incluem **Resumo do RMS**, **Usuários RMS ativos**, **Plataformas do dispositivo RMS** e **Uso do aplicativo RMS**. Para acessar esses relatórios no portal clássico do Azure, clique em **Active Directory**, selecione e abra um diretório e clique em **RELATÓRIOS**,

Use as seguintes seções para obter mais informações sobre registro em log do uso do Azure Rights Management.

## Como habilitar o registro em log de uso do Azure Rights Management
A partir de fevereiro de 2016, o registro em log do uso do Azure Rights Management é habilitado por padrão para todos os clientes. Isto aplica-se aos clientes que ativaram seu serviço Azure RMS antes de fevereiro de 2016 e aos clientes que ativaram o serviço depois de fevereiro de 2016. 

> [!NOTE]
> Não há nenhum custo extra para o armazenamento de log ou para a funcionalidade de recurso de registro em log.
> 
> Se você usou o log de uso para Azure RMS antes de fevereiro de 2016, você precisava de uma assinatura do Azure e de armazenamento suficiente no Azure, o que não é mais o caso.



## Como acessar e usar seus logs de uso Azure Rights Management
O Azure Rights Management grava logs na sua conta de armazenamento do Azure como uma série de blobs. Cada blob contém um ou mais registros de log, no formato de log estendido W3C. Os nomes de blob são números, na ordem em que eles são criados. A seção [Como interpretar seus logs de uso do Azure Rights Management](#how-to-interpret-your-azure-rights-management-usage-logs) mais adiante neste documento contém mais informações sobre o conteúdo do log e sua criação.

Pode levar um tempo para que os logs apareçam na sua conta de armazenamento depois de uma ação do Azure Rights Management. A maioria dos logs aparecem dentro de 15 minutos. Recomendamos que você baixe os logs no armazenamento local, como uma pasta local, um banco de dados, ou um repositório de redução de mapa.

Para baixar os logs de seu uso, você usará o módulo de administração do Azure RMS para o Windows PowerShell. Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md). Se você já tiver baixado este módulo do Windows PowerShell anteriormente, execute o seguinte comando para verificar se o seu número de versão é pelo menos, **2.4.0.0**: `(Get-Module aadrm -ListAvailable).Version` 

### Para baixar seus logs de uso usando o PowerShell

1.  Inicie o Windows PowerShell com a opção **Executar como administrador** e use o cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) para conectar-se ao serviço do Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    
2.  Execute o comando a seguir para baixar os logs para uma data específica: 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    Por exemplo, depois de criar uma pasta chamada Logs na sua unidade E:
    
    * Para baixar os logs para uma data específica (por exemplo, 01/02/2016), execute o seguinte comando: `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Para baixar os logs para um intervalo de datas (por exemplo, a partir de 01/02/2016 até 14/02/2016), execute o seguinte comando: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Quando você especifica apenas o dia, como em nossos exemplos, o horário é presumido como 00:00:00 em sua hora local e depois convertido para UTC. Quando você especifica um horário com seus parâmetros -fromdate ou -todate (por exemplo, -fordate "2/1/2016 15:00:00"), essa data e hora são convertidas para UTC. O comando Get-AadrmUserLog então obtém os logs para esse período de tempo em horário UTC.

Você não pode especificar menos de um dia inteiro para baixar.

Por padrão, esse cmdlet usa três threads para baixar os logs. Se você tem suficiente largura de banda de rede e quer diminuir o tempo necessário para baixar os logs, use o parâmetro -NumberOfThreads, que dá suporte a um valor de 1 a 32. Por exemplo, se você executar o comando a seguir, o cmdlet gerará 10 threads para baixar os logs: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> Você pode agregar todos os arquivos de log baixados em um formato CSV usando o [Log Parser da Microsoft](https://www.microsoft.com/download/details.aspx?id=24659), que é uma ferramenta para converter entre vários formatos de log conhecidos. Você também pode usar esta ferramenta para converter dados para o formato SYSLOG, ou importá-lo em um banco de dados. Depois de instalar a ferramenta, execute `LogParser.exe /?` para obter ajuda e informações para usar essa ferramenta. 
>
> Por exemplo, você pode executar o seguinte comando para importar todas as informações em um formado de arquivo .log: `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### Se você habilitou manualmente o log de uso do Azure RMS antes da alteração do registro em log em 22 de fevereiro de 2016


Se você usou o log de uso antes da alteração do registro em log, você terá os logs de uso em sua conta de armazenamento Azure configurada. A Microsoft não copiará esses logs de sua conta de armazenamento para a nova conta de armazenamento gerenciada do Azure RMS como parte desta alteração do registro em log. Você é responsável por gerenciar o ciclo de vida dos logs gerados anteriormente e pode usar o cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) para baixar seus logs antigos. Por exemplo:

- Para baixar todos os logs disponíveis na sua pasta E:\logs: `Get-AadrmUsageLog -Path "E:\Logs"`
    
- Para baixar um intervalo específico de blobs: `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

Observe que você não precisará baixar logs usando o cmdlet Get-AadrmUsageLog se qualquer uma das seguintes se aplicar:

-  Você ativou o Azure Rights Management em ou antes de 22 de fevereiro de 2016, mas não habilitou o recurso de log de uso.

- Você ativou o Azure Rights Management após 22 de fevereiro de 2016.

## Como interpretar seus logs de uso do Azure Rights Management
Use as informações a seguir para ajudá-lo interpretar os logs de uso do Azure Rights Management.

### A sequência de log
O Azure Rights Management grava os logs como uma série de blobs. 

Cada entrada no log tem um carimbo de data/hora UTC. Já que o Azure Rights Management é executado em vários servidores entre vários data centers, às vezes os logs podem parecer estar fora de sequência, mesmo quando eles são classificados por seu carimbo de data/hora. No entanto, a diferença é pequena e geralmente menor que um minuto. Na maioria dos casos, essa não é uma questão que possa ser um problema para a análise de log.

### O formato de blob
Cada blob está no formato de log estendido W3C. Começa com as duas linhas a seguir:

**#Software: RMS**

**#Versão 1.1**

A primeira linha identifica que esses são os logs do Azure Rights Management. A segunda linha identifica que o resto do blob segue as especificações da versão 1.1. Recomendamos que qualquer aplicativo que analise estes logs verifique estas duas linhas antes de continuar a analisar o resto do blob.

A terceira linha enumera uma lista de nomes do campo que são separados por guias:

**#Campos: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

Cada uma das linhas subsequentes é um registro de log. Os valores dos campos estão na mesma ordem que a linha precedente, e são separados por guias. Use a seguinte tabela para interpretar os campos.

|Nome do campo|Tipo de dados W3C|Descrição|Valor de exemplo|
|--------------|-----------------|---------------|-----------------|
|date|Data|Data UTC quando a solicitação foi servida.<br /><br />A fonte é o relógio local no servidor que serviu a solicitação.|2013-06-25|
|hora|Hora|Hora UTC no formato de 24 horas quando a solicitação foi servida.<br /><br />A fonte é o relógio local no servidor que serviu a solicitação.|21:59:28|
|row-id|Text|GUID exclusivo para este registro de log. Se não houver um valor, use o valor correlation-id para identificar a entrada.<br /><br />Este valor é usado quando você agrega logs ou cópia logs em um outro formato.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nome|Nome do API do RMS que foi solicitado.|AcquireLicense|
|user-id|Cadeia de caracteres|O usuário que fez a solicitação.<br /><br />O valor que é colocado entre aspas simples. Chamadas de uma chave de locatário gerenciada por você (BYOK) têm um valor de **"**, que também se aplica quando os tipos de solicitação anônimos.|‘joe@contoso.com’|
|result|Cadeia de caracteres|‘Êxito’ se a solicitação foi servida com êxito.<br /><br />O tipo de erro entre aspas simples marca se a solicitação falhou.|‘Êxito’|
|correlation-id|Text|O GUID que seja comum entre o log do cliente do RMS e o log do servidor para uma solicitação especificada.<br /><br />Este valor pode ser útil para ajudar a solucionar problemas de clientes.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Text|O GUID, que se encontra entre chaves que identifica o conteúdo protegido (por exemplo, um documento).<br /><br />Este campo tem um valor somente se o tipo de solicitação é AcquireLicense e é branco par todos os outros tipos de solicitações.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|email proprietário|Cadeia de caracteres|Endereço de email do proprietário do documento.|alice@contoso.com|
|emissor|Cadeia de caracteres|Endereço de email do emissor do documento.|alice@contoso.com (or) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|template-id|Cadeia de caracteres|ID do modelo usado para proteger o documento.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|file-name|Cadeia de caracteres|Nome do arquivo do documento que estava protegido. <br /><br />No momento, alguns arquivos (como documentos do Office) são exibidos como GUIDs em vez do nome do arquivo real.|TopSecretDocument.docx|
|date-published|Data|Data quando o documento foi protegido.|2015-10-15T21:37:00|
|c-info|Cadeia de caracteres|As informações sobre a plataforma do cliente que estão fazendo a solicitação.<br /><br />A cadeia de caracteres varia, dependendo do aplicativo (por exemplo, o sistema operativo ou o navegador).|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Endereço|O endereço IP do cliente que realiza a solicitação.|64.51.202,144|


#### Exceções para o campo user-id
Mesmo que o campo user-id geralmente indica ao usuário que realizou o pedido, há duas exceções onde o valor não mapeia a um usuário real:

-   O valor **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;região&gt;.aadrm.com'**.

    Isso indica que um serviço Office 365, como o Exchange Online ou SharePoint Online, está realizando a solicitação. Na cadeia de caracteres, *&lt;YourTenantID&gt;* é o GUID para seu locatário e *&lt;região&gt;* é a região onde seu locatário é registrado. Por exemplo, **na** representa América do Norte, **eu** representa a Europa e **ap** representa a Ásia.

-   Se você estiver usando o conector do RMS.

    As solicitações deste conector são registrados em log com o nome da entidade de serviço de **Aadrm_S-1-7-0**, gerado automaticamente quando você instala o conector RMS.

#### Tipos de solicitações típicas
Há vários tipos de solicitações no Azure Rights Management, mas a seguinte tabela identifica alguns dos tipos de solicitações mais usados.

|Tipo de solicitação|Descrição|
|----------------|---------------|
|AcquireLicense|Um cliente de um computador baseado no Windows está solicitando uma licença para conteúdo protegido pelo RMS.|
|AcquirePreLicense|Um cliente, em nome do usuário, está solicitando uma licença para conteúdo protegido pelo RMS.|
|AcquireTemplates|Foi feita uma chamada para adquirir modelos baseados nos IDs de modelo|
|AcquireTemplateInformation|Foi feita uma chamada para obter as identificações do modelo do serviço.|
|AddTemplate|É feita uma chamada do portal clássico do Azure para adicionar um modelo.|
|AllDocsCsv|É feita uma chamada do site de rastreamento de documentos para baixar o arquivo CSV na página **Todos os Documentos**.|
|BECreateEndUserLicenseV1|É feita uma chamada de um dispositivo móvel para criar uma licença de usuário final.|
|BEGetAllTemplatesV1|É feita uma chamada de um dispositivo móvel (backend) para obter todos os modelos.|
|Certify|O cliente certifica o conteúdo para proteção.|
|KMSPDecrypt|O cliente está tentando descriptografar o conteúdo protegido pelo RMS. Aplicável somente para uma chave de locatário gerenciada pelo cliente (BYOK).|
|DeleteTemplateById|É feita uma chamada no portal clássico do Azure para excluir um modelo por ID de modelo.|
|DocumentEventsCsv|É feita uma chamada do site de rastreamento de documentos para baixar o arquivo .CSV de um único documento.|
|ExportTemplateById|É feita uma chamada no portal clássico do Azure para excluir um modelo com base no ID de modelo.|
|FECreateEndUserLicenseV1|Semelhante à solicitação AcquireLicense mas de dispositivos móveis.|
|FECreatePublishingLicenseV1|Igual que o Certify e GetClientLicensorCert juntos, de cliente móveis.|
|FEGetAllTemplates|É feita uma chamada de um dispositivo móvel (frontend) para obter todos os modelos.|
|GetAllDocs|É feita uma chamada do site de rastreamento de documentos para carregar a página **todos os documentos** de um usuário ou pesquisar todos os documentos do locatário. Use esse valor com os campos admin-action e acting-as-admin:<br /><br />– admin-action está vazio: um usuário exibe a página **todos os documentos** de seus próprios documentos.<br /><br />– admin-action é true e acting-as-user está vazio: um administrador exibe todos os documentos de seu locatário.<br /><br />– admin-action é true e acting-as-user não está vazio: um administrador exibe a página **todos os documentos** de seu locatário.|
|GetAllTemplates|É feita uma chamada do portal clássico do Azure para obter todos os modelos.|
|GetClientLicensorCert|O cliente está solicitando um certificado de publicação (que é posteriormente usado para proteger conteúdo) de um computador baseado no Windows.|
|GetConfiguration|Um cmdlet do Azure PowerShell é chamado para obter a configuração do locatário do Azure RMS.|
|GetConnectorAuthorizations|É feita uma chamada dos conectores do RMS para obter suas configurações da nuvem.|
|GetRecipients|É feita uma chamada do site de rastreamento de documentos para navegar até a exibição de lista de um único documento.|
|GetSingle|É feita uma chamada do site de rastreamento de documentos para navegar até uma página de um **único documento**.|
|GetTenantFunctionalState|O portal clássico do Azure está verificando se o Azure RMS está ativado.|
|GetTemplateById|É feita uma chamada no portal clássico do Azure para obter um modelo, especificando o ID de modelo.|
|ExportTemplateById|É feita uma chamada no portal clássico do Azure para exportar um modelo, especificando o ID de modelo.|
|FindServiceLocationsForUser|É feita uma chamada para consultas URLs, que é usada para chamar Certify ou AcquireLicense.|
|LoadEventsForMap|É feita uma chamada do site de rastreamento de documentos para navegar até a exibição de mapa de um único documento.|
|LoadEventsForSummary|É feita uma chamada do site de rastreamento de documentos para navegar até a exibição de linha do tempo de um único documento.|
|LoadEventsForTimeline|É feita uma chamada do site de rastreamento de documentos para navegar até a exibição de mapa de um único documento.|
|ImportTemplate|É feita uma chamada do portal clássico do Azure para importar um modelo.|
|RevokeAccess|É feita uma chamada do site de rastreamento de documentos para revogar um documento.|
|SearchUsers |É feita uma chamada do site de rastreamento de documentos para pesquisar todos os usuários em um locatário.|
|ServerCertify|É feita uma chamada de um cliente habilitado para RMS (como SharePoint) para certificar o servidor.|
|SetUsageLogFeatureState|É feita uma chamada para habilitar o registro em log de uso.|
|SetUsageLogStorageAccount|É feita uma chamada para especificar o local dos logs do Azure RMS.|
|SignDigest|É feita uma chamada quando uma chave é usada para fins de assinatura. Isso é chamado geralmente uma vez por AcquireLicence (ou FECreateEndUserLicenseV1), Certify e GetClientLicensorCert (ou FECreatePublishingLicenseV1).|
|UpdateNotificationSettings|É feita uma chamada do site de rastreamento de documentos para alterar as configurações de notificação de um único documento.|
|UpdateTemplate|É feita uma chamada do portal clássico do Azure para atualizar um modelo existente.|



## Referência do Windows PowerShell
A partir de fevereiro de 2016, o único cmdlet do Windows PowerShell que você precisa para o registro em log de uso do Azure RMS é [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx). 

Antes desta alteração, os cmdlets a seguir eram necessários para os logs de uso do Azure RMS e agora são preteridos:  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Se você tem logs em seu próprio armazenamento do Azure de antes da alteração do registro em log do Azure RMS, você pode baixá-los com esses cmdlets mais antigos, usando Get-AadrmUsageLog e Get-AadrmUsageLogLastCounterValue, como antes. Mas todos os logs de uso novo serão gravados no novo armazenamento do Azure RMS e devem ser baixados com Get-AadrmUserLog.

Para obter mais informações sobre o uso do Windows PowerShell para o Azure Rights Management, consulte [Administrando o Azure Rights Management usando Windows PowerShell](administer-powershell.md).






<!--HONumber=Aug16_HO1-->


