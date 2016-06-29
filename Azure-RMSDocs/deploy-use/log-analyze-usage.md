---
# required metadata

title: Registo e análise da utilização do Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Registo e análise da utilização do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Utilize as informações deste tópico para o ajudar a compreender como pode utilizar o registo da utilização com o Azure Rights Management (RMS do Azure). O serviço Azure Rights Management pode registar cada pedido que faz para a sua organização, incluindo pedidos de utilizadores, ações realizadas por administradores de Gestão de Direitos na sua organização e ações realizadas por operadores da Microsoft relacionadas com a sua implementação do Azure Rights Management.

Em seguida, pode utilizar estes registos do Azure Rights Management para ajudar nos seguintes cenários empresariais:

-   **Analisar informações empresariais**

    Os registos gerados pelo Azure Rights Management podem ser importados para um repositório à sua escolha (tal como uma base de dados, um sistema OLAP (Online Analytical Processing) ou um sistema MapReduce) para analisar as informações e criar relatórios. A título de exemplo, poderia identificar quem está a aceder aos seus dados protegidos pelo RMS. Pode determinar o tipo de dados protegidos pelo RMS a que as pessoas estão a aceder, bem como os dispositivos e o local a partir dos quais estão a aceder. Pode descobrir se as pessoas conseguem ler conteúdos protegidos com êxito. Também pode identificar as pessoas que leram um documento importante que estava protegido.

-   **Monitorizar abusos**

    As informações de registo do Azure Rights Management são-lhe disponibilizadas quase em tempo real, para que possa monitorizar continuamente a utilização do Rights Management da sua empresa. 99,9% dos registos estão disponíveis no prazo de 15 minutos após uma ação iniciada pelo RMS.

    Por exemplo, poderá querer ser alertado caso ocorra um aumento súbito de pessoas que estão a ler dados protegidos pelo RMS fora do horário de trabalho normal, o que pode significar que um utilizador mal-intencionado está a recolher informações para vender à concorrência. Em alternativa, poderá querer ser alertado se o mesmo utilizador parecer aceder a dados a partir de dois endereços IP diferentes num curto período de tempo, o que pode significar que uma conta de utilizador foi comprometida.

-   **Efetuar análises forenses**

    Se ocorrer uma fuga de informações, é provável que lhe seja pedido para indicar quem acedeu recentemente a documentos específicos e a que tipo de informações uma pessoa suspeita acedeu recentemente. Se utilizar o Azure Rights Management e os registos, poderá responder a este tipo de questões, porque as pessoas que utilizam conteúdos protegidos têm sempre de obter uma licença de Rights Management para abrir documentos e imagens protegidos pelo Azure Rights Management, mesmo que estes ficheiros sejam movidos por e-mail ou copiados para unidades USB ou para outros dispositivos de armazenamento. Isto significa que, se proteger os seus dados com o Azure Rights Management, pode utilizar os registos do mesmo como fonte definitiva de informações para análises forenses.

> [!NOTE] Caso só esteja interessado no registo de tarefas administrativas para o Azure Rights Management e não queira controlar a forma como os utilizadores estão a utilizar o Rights Management, pode utilizar o cmdlet [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) do Windows PowerShell para o Azure Rights Management.
> 
> Também pode utilizar o portal clássico do Azure para relatórios gerais de utilização que incluam **Resumo do RMS**, **Utilizadores ativos do RMS**, **Plataformas de dispositivos do RMS** e **Utilização da aplicação do RMS**. Para aceder a estes relatórios a partir do portal clássico do Azure, clique em **Active Directory**, selecione e abra um diretório e, em seguida, clique em **RELATÓRIOS**.

Utilize as seguintes secções para obter mais informações sobre o registo de utilização do Azure Rights Management.

## Como ativar o registo de utilização do Azure Rights Management
A partir de fevereiro de 2016, o registo de utilização do Azure Rights Management passou a ser ativado por predefinição para todos os clientes. Isto aplica-se aos clientes que ativaram o serviço Azure RMS antes e após fevereiro de 2016. 

> [!NOTE] Não existem custos adicionais associados ao armazenamento dos registos nem à funcionalidade do registo.
> 
> Se utilizava o registo de utilização para o Azure RMS antes de fevereiro de 2016, precisava de uma subscrição do Azure e de espaço de armazenamento suficiente no Azure, o que já não é o caso.



## Como aceder e utilizar os seus registos de utilização do Azure Rights Management
O Azure Rights Management escreve registos na sua conta de armazenamento do Azure como uma série de blobs. Cada blob contém um ou mais registos num formato de registo expandido W3C. Os nomes dos blobs são números, pela ordem em que foram criados. A secção [Como interpretar os seus registos de utilização do Azure Rights Management](#how-to-interpret-your-azure-rights-management-usage-logs), que se encontra mais adiante neste documento, contém mais informações sobre os conteúdos dos registos e a criação dos mesmos.

Após uma ação do Azure Rights Management, os registos poderão demorar algum tempo a serem apresentados na sua conta de armazenamento. A maioria dos registos é apresentada no espaço de 15 minutos. Recomendamos que transfira os registos para o armazenamento local, por exemplo para uma pasta local, uma base de dados ou um repositório MapReduce.

Para transferir os seus registos de utilização, deverá utilizar o módulo de administração do Azure RMS para o Windows PowerShell. Para obter instruções de instalação, consulte [Installing Windows PowerShell for Azure Rights Management (Instalar o Windows PowerShell para o Azure Rights Management – em inglês)](install-powershell.md). Caso já tenha transferido este módulo do Windows PowerShell, execute o seguinte comando para verificar se o seu número de versão é **2.4.0.0** ou posterior: `(Get-Module aadrm -ListAvailable).Version` 

### Para transferir os seus registos de utilização através do PowerShell

1.  Inicie o Windows PowerShell com a opção **Executar como administrador** e utilize o cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) para efetuar uma ligação ao serviço Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    
2.  Execute o seguinte comando para transferir os registos de uma data específica: 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    Por exemplo, depois de criar uma pasta denominada Registos na unidade E:
    
    * Para transferir os registos de uma data específica (como 1/2/2016), execute o seguinte comando: `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Para transferir os registos de um intervalo de datas (como de 1/2/2016 a 14/2/2016), execute o seguinte comando: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Quando especifica apenas o dia (tal como acontece nos nossos exemplos), assume-se que a hora é 00:00:00 na sua hora local, que é então convertida para UTC. Se especificar uma hora com os parâmetros -fromdate ou -todate (por exemplo, -fromdate "1/2/2016 15:00:00"), essa data e hora será convertida para UTC. Em seguida, o comando Get-AadrmUserLog obtém os registos correspondentes a esse período de tempo UTC.

Não pode especificar menos de um dia inteiro para transferir.

Por predefinição, este cmdlet utiliza três threads para transferir os registos. Se tiver largura de banda de rede suficiente e quiser diminuir o tempo necessário para transferir os registos, utilize o parâmetro -NumberOfThreads, que suporta um valor de 1 a 32. Por exemplo, se executar o seguinte comando, o cmdlet cria 10 threads para transferir os registos: `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> Pode agregar todos os seus ficheiros de registo transferidos num ficheiro em formato CSV através do [Log Parser da Microsoft](https://www.microsoft.com/download/details.aspx?id=24659), uma ferramenta de conversão para diversos formatos de registo comuns. Também pode utilizar esta ferramenta para converter dados no formato SYSLOG ou para os importar para uma base de dados. Após instalar a ferramenta, execute o ficheiro `LogParser.exe /?` para obter ajuda e informações relativamente à utilização desta ferramenta. 
>
> Por exemplo,pode executar o seguinte comando para importar todas as informações para um ficheiro com o formato .log: `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### Se ativou manualmente o registo da utilização do Azure RMS antes da alteração do registo de 22 de fevereiro de 2016


Se utilizou o registo da utilização antes da alteração do registo, terá registos de utilização na sua conta de armazenamento do Azure configurada. A Microsoft não copiará estes registos da sua conta de armazenamento para a nova conta de armazenamento gerida pelo Azure RMS como parte desta alteração de registo. Você é responsável por gerir o ciclo de vida dos registos gerados anteriormente e pode utilizar o cmdlet [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) para transferir os registos antigos. Por exemplo:

- Para transferir todos os registos disponíveis para a sua pasta E:\logs: `Get-AadrmUsageLog -Path "E:\Logs"`
    
- Para transferir um intervalo específico de blobs: `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

Tenha em atenção que não é necessário transferir registos com o cmdlet Get-AadrmUsageLog, caso se verifique uma das situações abaixo:

-  Ativou o Azure Rights Management a 22 de fevereiro de 2016 ou antes desta data, mas não ativou a funcionalidade de registo da utilização.

- Ativou o Azure Rights Management depois de 22 de fevereiro de 2016.

## Como interpretar os seus registos de utilização do Azure Rights Management
Utilize as seguintes informações para saber como interpretar os registos de utilização do Azure Rights Management.

### A sequência de registo
O Azure Rights Management escreve os registos como uma série de blobs. 

Cada entrada no registo tem um carimbo de data/hora UTC. Como o Azure Rights Management é executado em múltiplos servidores de múltiplos centros de dados, por vezes os registos podem parecer não estar em sequência, mesmo quando se encontram ordenados pelo respetivo carimbo de data/hora. No entanto, a diferença é pequena e, normalmente, não é superior a um minuto. Na maioria dos casos, isto não representa um problema para a análise de registos.

### O formato de blob
Cada blob está num formato de registo expandido W3C. Começa com estas duas linhas:

**#Software: RMS**

**#Version: 1.1**

A primeira linha indica que estes são registos do Azure Rights Management. A segunda linha indica que o resto do blob segue a especificação da versão 1.1. Recomendamos que todas as aplicações que analisem estes registos verifiquem estas duas linhas antes de continuar a analisar o resto do blob.

A terceira linha apresenta uma lista composta por nomes de campos que são separados por tabulações:

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

Cada uma das linhas subsequentes é um registo. Os valores dos campos estão na mesma ordem da linha anterior e são separados por tabulações. Utilize a seguinte tabela para interpretar os campos.

|Nome do campo|Tipo de dados W3C|Descrição|Valor de exemplo|
|--------------|-----------------|---------------|-----------------|
|date|Data|Data UTC em que o pedido foi servido.<br /><br />A origem é o relógio local no servidor que serviu o pedido.|2013-06-25|
|time|Hora|Hora UTC, em formato de 24 horas, em que o pedido foi servido.<br /><br />A origem é o relógio local no servidor que serviu o pedido.|21:59:28|
|row-id|Texto|GUID exclusivo deste registo.<br /><br />Este valor é útil quando agrega registos ou copia registos para outro formato.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nome|Nome da API de RMS que foi pedida.|AcquireLicense|
|user-id|Cadeia|O utilizador que efetuou o pedido.<br /><br />O valor está entre plicas. Alguns tipos de pedido são anónimos. Se assim for, o valor será ”.|‘joao@contoso.com’|
|result|Cadeia|‘Êxito’, se o pedido tiver sido servido com êxito.<br /><br />O tipo de erro entre plicas se o pedido tiver falhado.|‘Êxito’|
|correlation-id|Texto|GUID que é comum entre o registo de cliente do RMS e o registo do servidor para um determinado pedido.<br /><br />Este valor pode ser útil para ajudar na resolução de problemas do cliente.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Texto|GUID, entre chavetas, que identifica os conteúdos protegidos (por exemplo, um documento).<br /><br />Este campo só terá um valor se o request-type for AcquireLicense e estiver em branco para todos os outros tipos de pedido.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|Cadeia|Endereço de e-mail do proprietário do documento.|ines@contoso.com|
|issuer|Cadeia|Endereço de e-mail do emissor do documento.|ines@contoso.com (ou) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Template-id|Cadeia|ID do modelo utilizado para proteger o documento.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|File-name|Cadeia|Nome de ficheiro do documento que foi protegido. <br /><br />Atualmente, alguns ficheiros (como documentos do Office) são apresentados como GUIDs em vez do nome de ficheiro real.|DocumentoConfidencial.docx|
|Date-published|Data|Data em que o ficheiro foi protegido.|2015-10-15T21:37:00|
|c-info|Cadeia|Informações sobre a plataforma de cliente que está a efetuar o pedido.<br /><br />A cadeia específica varia em função da aplicação (por exemplo, do sistema operativo ou do browser).|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|Endereço|Endereço IP do cliente que efetua o pedido.|64.51.202.144|

#### Exceções para o campo user-id
Apesar de o campo user-id indicar geralmente o utilizador que efetuou o pedido, existem duas exceções onde o valor não é mapeado para um utilizador real:

-   O valor **"microsoftrmsonline@&lt;IDDoSeuInquilino&gt;.rms.&lt;região&gt;.aadrm.com"**.

    Isto indica que o pedido está a ser efetuado por um serviço do Office 365, tal como o Exchange Online ou o SharePoint Online. Na cadeia, *&lt;IDDoSeuInquilino&gt;* é o GUID para o seu inquilino e *&lt;região&gt;* é a região em que o seu inquilino está registado. Por exemplo, **na** significa North America (América do Norte), **eu** significa Europa e **ap** significa Ásia.

-   Se estiver a utilizar o conector RMS.

    Os pedidos efetuados a partir deste conector são registados com o nome do principal do serviço que o RMS gera automaticamente quando o conector RMS é instalado.

#### Tipos de pedido comuns
Há muitos tipos de pedido para o Azure Rights Management, mas a seguinte tabela apresenta alguns dos tipos de pedido mais frequentemente utilizados.

|Tipo de pedido|Descrição|
|----------------|---------------|
|AcquireLicense|Um cliente de um computador baseado no Windows está a pedir uma licença para conteúdos protegidos pelo RMS.|
|AcquirePreLicense|Um cliente está a pedir, em nome do utilizador, uma licença para conteúdos protegidos pelo RMS.|
|AcquireTemplates|Foi efetuada uma chamada para adquirir modelos com base em IDs de modelo|
|AcquireTemplateInformation|Foi efetuada uma chamada para obter as ID do modelo a partir do serviço.|
|AddTemplate|É efetuada uma chamada a partir do portal clássico do Azure para adicionar um modelo.|
|BECreateEndUserLicenseV1|É efetuada uma chamada a partir de um dispositivo móvel para criar uma licença de utilizador final.|
|BEGetAllTemplatesV1|É efetuada uma chamada a partir de um dispositivo móvel (back-end) para obter todos os modelos.|
|Certify|O cliente está a certificar os conteúdos para proteção.|
|Desencriptar|O cliente está a tentar desencriptar os conteúdos protegidos pelo RMS.|
|DeleteTemplateById|É efetuada uma chamada a partir do portal clássico do Azure para eliminar um modelo por ID de modelo.|
|ExportTemplateById|É efetuada uma chamada a partir do portal clássico do Azure para exportar um modelo baseado num ID de modelo.|
|FECreateEndUserLicenseV1|É semelhante ao pedido AcquireLicense, mas este pedido é efetuado a partir de dispositivos móveis.|
|FECreatePublishingLicenseV1|É igual à combinação dos pedidos Certify e GetClientLicensorCert, feito a partir de clientes móveis.|
|FEGetAllTemplates|É efetuada uma chamada a partir de um dispositivo móvel (front-end) para obter os modelos.|
|GetAllTemplates|É efetuada uma chamada a partir do portal clássico do Azure para obter todos os modelos.|
|GetClientLicensorCert|O cliente está a pedir um certificado de publicação (que é posteriormente utilizado para proteger conteúdos) a partir de um computador baseado no Windows.|
|GetConfiguration|É chamado um cmdlet do PowerShell do Azure para obter a configuração do inquilino do Azure RMS.|
|GetConnectorAuthorizations|É efetuada uma chamada a partir dos conectores do RMS para obter a configuração destes a partir da nuvem.|
|GetTenantFunctionalState|O portal clássico do Azure está a verificar se o Azure RMS está ativado.|
|GetTemplateById|É efetuada uma chamada a partir do portal clássico do Azure para obter um modelo através da especificação de um ID de modelo.|
|ExportTemplateById|Está a ser efetuada uma chamada a partir do portal clássico do Azure para exportar um modelo através da especificação de um ID de modelo.|
|FindServiceLocationsForUser|É efetuada uma chamada de consulta de URL, que é utilizada para chamar o pedido Certify ou AcquireLicense.|
|ImportTemplate|É efetuada uma chamada a partir do portal clássico do Azure para importar um modelo.|
|ServerCertify|É efetuada uma chamada a partir de um cliente com RMS ativado (tal como o SharePoint) para certificar o servidor.|
|SetUsageLogFeatureState|É efetuada uma chamada para ativar o registo de utilização.|
|SetUsageLogStorageAccount|É efetuada uma chamada para especificar a localização dos registos do Azure RMS.|
|SignDigest|É efetuada uma chamada quando é utilizada uma chave para fins de assinatura. Esta opção é normalmente chamada uma vez por cada pedido AcquireLicence (ou FECreateEndUserLicenseV1), Certify e GetClientLicensorCert (ou FECreatePublishingLicenseV1).|
|UpdateTemplate|É efetuada uma chamada a partir do portal clássico do Azure para atualizar um modelo existente.|

## Referência do Windows PowerShell
A partir de fevereiro de 2016, o único cmdlet do Windows PowerShell de que necessita para o registo de utilização do Azure RMS é o [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx). 

Antes desta alteração, para os registos de utilização do Azure RMS, eram necessários os seguintes cmdlets, que estão agora preteridos:  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Se, no seu armazenamento do Azure, tiver registos criados em datas anteriores à da alteração do registo do Azure RMS, pode transferi-los com os cmdlets mais antigos Get-AadrmUsageLog e Get-AadrmUsageLogLastCounterValue, tal como faria anteriormente. No entanto, todos os novos registos de utilização escreverão no novo armazenamento do Azure RMS e têm de ser transferidos com o cmdlet Get-AadrmUserLog.

Para mais informações sobre como utilizar o Windows PowerShell para o Azure Rights Management, consulte [Administrar o Azure Rights Management através do Windows PowerShell](administer-powershell.md).





<!--HONumber=May16_HO3-->


