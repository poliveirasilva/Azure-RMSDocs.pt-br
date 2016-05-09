---
title: TESTAR o planejamento e implementação de sua chave de locatário do Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# ANTES DE: planejar e implementar sua chave de locatário do Azure Rights Management
Use as informações neste tópico para ajudá-lo a planejar e a gerenciar sua chave de locatário de serviço do Rights Management (RMS) para o Azure RMS. Por exemplo, em vez da Microsoft gerenciar sua chave de locatário (o padrão), caso queira gerenciar a sua própria chave de locatário de acordo com as normas específicas que se aplicam à sua organização.  Gerenciar a sua chave de locatário também é chamado de trazer sua própria chave, ou BYOK.

> [!NOTE]
> A chave de locatário do RMS também é conhecida como chave do certificado de licenciante para servidor (SLC). O Azure RMS mantém uma ou mais chaves para cada organização que assina o Azure RMS. Sempre que uma chave é usada para o RMS dentro de uma organização (tais como chaves de usuário, chaves de computador, chaves de criptografia de documento), eles a encadeiam criptograficamente com a sua chave de locatário do RMS.

**Visão geral:** Use a seguinte tabela como um guia rápido para sua topologia de chave de locatário recomendada. Use as seguintes seções para obter mais informações:

Se você implantar o Azure RMS usando uma chave de locatário gerenciada pela Microsoft, você pode alterar para BYOK posteriormente. No entanto, no momento você não pode alterar sua chave de locatário do Azure RMS de BYOK para gerenciada pela Microsoft.

|Requisito de negócios|Topologia de chave de locatário recomendada|
|------------------------|-----------------------------------|
|Implantar o Azure RMS rapidamente e sem a necessidade de hardware especial|Gerenciada pela Microsoft|
|Precisa de funcionalidade completa do IRM no Exchange Online com o Azure RMS|Gerenciada pela Microsoft|
|As suas chaves são criadas por você e protegidas em um módulo de segurança de hardware (HSM)|BYOK<br /><br />Atualmente, essa configuração resultará em funcionalidade reduzida do IRM no Exchange Online. Para obter mais informações, consulte a seção [Preços e restrições do BYOK](plan-implement-tenant-key.md#BKMK_Pricing).|
Use as seções a seguir para ajudá-lo a escolher qual topologia de chave de locatário usar, entender o ciclo de vida da chave de locatário, como implementar a opção traga a sua própria chave (BYOK) e quais etapas executar em seguida:

-   [Escolha sua topologia de chave de locatário: Gerenciada pela Microsoft (o padrão) ou gerenciada por você (BYOK)](plan-implement-tenant-key.md#BKMK_ChooseTenantKey)

-   [Preços e restrições do BYOK](plan-implement-tenant-key.md#BKMK_Pricing)

-   [Implementando trazer a sua própria chave (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK)

-   [Próximas etapas](plan-implement-tenant-key.md#BKMK_NextSteps)

## <a name="BKMK_ChooseTenantKey"></a>Escolha sua topologia de chave de locatário: Gerenciada pela Microsoft (o padrão) ou gerenciada por você (BYOK)
Decida qual topologia de chave de locatário é melhor para sua organização. Por padrão, o Azure RMS gera sua chave de locatário e gerencia a maioria dos aspectos do ciclo de vida da chave de locatário. Esta é a opção mais simples com as menores despesas administrativas gerais. Na maioria dos casos, você não precisa nem saber que você tem uma chave de locatário. Basta se inscrever no Azure RMS e o resto do processo de gerenciamento de chave é feito pela Microsoft.

Como alternativa, você pode querer ter controle total sobre a sua chave de locatário, que envolve criá-la e manter a cópia mestra em suas instalações. Este cenário é, muitas vezes, mencionado como trazer a sua própria chave (BYOK). Com esta opção, acontece o seguinte:

1.  Você gera a chave de locatário em suas instalações, de acordo com suas políticas de TI.

2.  Transfira com segurança a chave de locatário de um HSM (Módulo de Segurança de Hardware) em sua posse para HSMs que são de propriedade e gerenciados pela Microsoft. Durante todo esse processo, a chave de locatário nunca sai do limite de proteção de hardware.

3.  Ao transferir a chave de locatário para a Microsoft, ela permanece protegida por HSMs da Thales. A Microsoft trabalhou com a Thales para garantir que a chave de locatário não possa ser extraída de HSMs da Microsoft.

Embora seja opcional, recomendamos o uso em logs de uso do Azure RMS e quase tempo real para ver exatamente como e quando a chave de locatário é usada.

> [!NOTE]
> Como medida de proteção adicional, o Azure RMS usa mundos de segurança separados para seus centros de dados na América do Norte, EMEA (Europa, Oriente Médio e África) e Ásia. Ao gerenciar a sua própria chave de locatário, ela é vinculada ao mundo de segurança da região em que o locatário do RMS está registrado. Por exemplo, uma chave de locatário de um cliente europeu não pode ser utilizada em centros de dados na América do Norte ou na Ásia.

## <a name="BKMK_OverviewLifecycle"></a>O ciclo de vida da chave de locatário
Se você decidir que a Microsoft deve gerenciar sua chave de locatário, a Microsoft lidará com a maioria das operações de chave do ciclo de vida. No entanto, se decidir gerenciar sua chave de locatário, você será responsável por muitas das operações do ciclo de vida da chave e por alguns procedimentos adicionais.

Os diagramas a seguir mostram e comparam essas duas opções. O primeiro diagrama mostra que há poucas sobrecargas de administrador para você na configuração padrão, quando a Microsoft gerencia a chave de locatário.

![](./media/RMS_BYOK_cloud.png)

O segundo diagrama mostra os passos adicionais necessários ao gerenciar a sua própria chave de locatário.

![](./media/RMS_BYOK_onprem.png)

Se decidir deixar a Microsoft gerenciar sua chave de locatário, não será necessária nenhuma ação adicional para gerar a chave e você pode ignorar as seções a seguir e ir direto para [Próximas etapas](plan-implement-tenant-key.md#BKMK_NextSteps).

Se optar por gerenciar sua chave de locatário por conta própria, leia as seguintes seções para obter mais informações.

### Mais informações sobre HSMs da Thales e adições da Microsoft
O Azure RMS usa HSMs da Thales para proteger suas chaves.

A Thales e-Security é uma fornecedora líder global de criptografia de dados e soluções de segurança cibernética para os setores de serviços financeiros, alta tecnologia, manufatura, governo e tecnologia. Com um histórico de 40 anos de proteção de informações corporativas e governamentais, as soluções Thales são usadas ​​por quatro das cinco maiores empresas de energia e aeroespacial, 22 países da OTAN, e oferece segurança a mais de 80% das operações de pagamento em todo o mundo.

A Microsoft tem colaborado com a Thales para melhorar o alto nível dos HSMs. Essas melhorias permitem obter os benefícios típicos de serviços hospedados sem abrir mão do controle sobre as chaves. Especificamente, essas melhorias permitem que a Microsoft gerencie os HSMs para que você não precise fazê-lo. Como um serviço de nuvem, o Azure RMS é dimensionado a curto prazo para atender aos picos de uso da organização. Ao mesmo tempo, sua chave está protegida dentro dos HSMs da Microsoft: Você mantém o controle sobre o ciclo de vida da chave porque gera a chave e a transfere para os HSMs da Microsoft.

Para obter mais informações, consulte [HSMs da Thales e Azure RMS](http://www.thales-esecurity.com/msrms/cloud) no site da Thales.

## <a name="BKMK_Pricing"></a>Preços e restrições do BYOK
A organização que tem uma assinatura gerenciada de TI Azure pode usar o BYOK e registrar o seu uso, sem custo extra. As organizações que usam o RMS para indivíduos não podem usar BYOK e log, porque elas não têm um administrador do locatário para configurar esses recursos.

> [!NOTE]
> Para obter mais informações sobre o RMS para pessoas físicas, consulte [RMS para pessoas físicas e Azure Rights Management](rms-for-individuals.md).

![](./media/RMS_BYOK_noExchange.png)

O BYOK e o log funcionam perfeitamente com todos os aplicativos que se integram com o Azure RMS. Isso inclui serviços de nuvem, como o SharePoint Online, servidores locais que executam o Exchange e servidores do SharePoint que trabalham com Azure RMS pelo uso do conector RMS e de aplicativos cliente, como o Office 2013. Você vai ter registros de uso de chave, independentemente de qual aplicativo faça solicitações de Azure RMS.

Há uma exceção: Atualmente, o **Azure RMS BYOK não é compatível com o Exchange Online**.  Se deseja usar o Exchange Online, recomendamos deixar o Azure RMS configurado no modo de gerenciamento de chave padrão, onde a Microsoft gera e gerencia a sua chave. Você tem a opção de mover para BYOK mais tarde, por exemplo, quando o Exchange Online oferece não oferece suporte ao BYOK do Azure RMS. No entanto, se você não puder esperar, outra opção é implantar o Azure RMS com BYOK agora, com funcionalidade reduzida do RMS para o Exchange Online (emails e anexos desprotegidos permanecerão totalmente funcionais):

-   Emails protegidos ou anexos protegidos no Outlook Web Access não poderão ser exibidos.

-   Emails protegidos em dispositivos móveis que usam o Exchange ActiveSync IRM não poderão ser exibidos.

-   Descriptografia de transporte (por exemplo, para verificar se há malware) e a descriptografia de diário não é possível, por isso emails e anexos protegidos serão ignorados.

-   Regras de proteção de transporte e prevenção de perda de dados (DLP) que impõem políticas de IRM não são possíveis, por isso a proteção RMS não pode ser aplicada usando esses métodos.

-   Pesquisa baseada em servidor para emails protegidos, portanto emails protegidos serão ignorados.

Quando você usa o Azure RMS BYOK com funcionalidade reduzida do RMS para o Exchange Online, o RMS funcionará com clientes de email no Outlook, Windows e Mac e outros clientes de email que não usam o Exchange ActiveSync IRM.

Se você estiver migrando para o Azure RMS do AD RMS, você pode importar a sua chave como um domínio de publicação confiável (TPD) para Exchange Online (também chamado BYOK na terminologia do Exchange, que é separada da terminologia do Azure RMS BYOK). Nesse cenário, você deve remover o TPD do Exchange Online para evitar modelos e diretivas em conflito. Para obter mais informações, consulte [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) da biblioteca de cmdlets do Exchange Online.

Às vezes, a exceção do BYOK do Azure RMS para o Exchange Online não é um problema na prática. Por exemplo, as organizações que precisam do BYOK e do log executam seus aplicativos de dados (Exchange, SharePoint, Office) no local e usam o Azure RMS para funcionalidades que não estão facilmente disponíveis com o AD RMS no local (por exemplo, a colaboração com outras empresas e acesso de clientes de telefonia móvel). O BYOK e o log operam bem neste cenário e permitem que a organização tenha controle total sobre a sua assinatura do Azure RMS.

## <a name="BKMK_ImplementBYOK"></a>Implementando trazer a sua própria chave (BYOK)
Use as informações e os procedimentos desta seção se você tiver decidido gerar e gerenciar sua chave de locatário; o cenário BYOK (trazer a sua própria chave):

-   [Pré-requisitos para o BYOK](plan-implement-tenant-key.md#BKMK_Preqs)

-   [Gerar e transferir a chave de locatário - pela Internet](plan-implement-tenant-key.md#BKMK_BYOK_Internet)

-   [Gerar e transferir sua chave de locatário pessoalmente](plan-implement-tenant-key.md#BKMK_BYOK_InPerson)

> [!IMPORTANT]
> Se você já tiver começado a usar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (o serviço está ativado) e tiver usuários que executam o Office 2010, entre em contato com o CSS (Microsoft Customer Support Services) antes de executar estes procedimentos. Dependendo do cenário e dos requisitos, talvez seja possível usar o BYOK, mas com algumas limitações ou passos adicionais.
> 
> Entre em contato com o CSS também se sua organização possui políticas específicas para a manipulação de chaves.

### <a name="BKMK_Preqs"></a>Pré-requisitos para o BYOK
Veja a tabela a seguir para obter uma lista de pré-requisitos para trazer sua própria chave (BYOK).

|Requisito|Mais informações|
|---------------|--------------------|
|Uma assinatura que dá suporte ao Azure RMS.|Para obter mais informações, consulte a seção [Assinaturas de nuvem que dão suporte ao Azure RMS](requirements-azure-rms.md#BKMK_SupportedSubscriptions) no tópico [Requisitos para o Azure Rights Management](requirements-azure-rms.md).|
|Você não pode usar o RMS para indivíduos ou Exchange Online. Ou, se você usar o Exchange Online, entenda e aceite as limitações do uso do BYOK com essa configuração.|Para obter mais informações sobre as atuais restrições e limitações do BYOK, consulte a seção [Preços e restrições do BYOK](plan-implement-tenant-key.md#BKMK_Pricing) neste tópico.<br /><br />**Importante**: atualmente, o BYOK não é compatível com o Exchange Online.|
|HSM da Thales, smartcards e software de suporte.<br /><br />**Observação**: se estiver migrando do AD RMS para o Azure RMS usando a chave de software para a chave de hardware, você deverá ter uma versão mínima de 11.62 para os drivers da Thales.|É necessário ter acesso a um Módulo de Segurança de Hardware da Thales e um conhecimento operacional básico dos HSMs da Thales. Consulte [Módulo de Segurança de Hardware da Thales](http://www.thales-esecurity.com/msrms/buy) para obter a lista de modelos compatíveis ou para comprar um HSM, se você não tiver um.|
|Se deseja transferir sua chave de locatário via Internet, em vez de estar fisicamente presente em Redmond, EUA, há 3 requisitos:<br /><br />Requisito 1: uma estação de trabalho x64 offline com um sistema operacional Windows mínimo do Windows 7 e software da Thales nShield que seja, pelo menos, da versão 11.62.<br /><br />Se esta estação de trabalho executa o Windows 7, você deve [instalar o Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br /><br />Requisito 2: uma estação de trabalho que esteja conectada à Internet e que tenha um sistema operacional Windows mínimo do Windows 7.<br /><br />Requisito 2: uma unidade USB ou outro dispositivo de armazenamento portátil que tenha, pelo menos, 16 MB de espaço livre.|Esses pré-requisitos não são necessários se você viajar para Redmond e transferir sua chave de locatário pessoalmente.<br /><br />Por razões de segurança, recomendamos que a primeira estação de trabalho não esteja conectada a uma rede. No entanto, isto não é programaticamente aplicado.<br /><br />Observação: nas instruções a seguir, essa estação de trabalho é mencionada como a **estação de trabalho desconectada**.<br /><br />Além disso, se a chave de locatário for para uma rede de produção, recomendamos o uso de uma segunda estação de trabalho separada para baixar o conjunto de ferramentas e fazer o upload da chave de locatário. Mas para fins de teste, é possível usar a mesma estação de trabalho como a primeira.<br /><br />Observação: nas instruções a seguir, essa segunda estação de trabalho é mencionada como a **estação de trabalho conectada à Internet**.|

Os procedimentos para gerar e utilizar a sua própria chave de locatário dependem se você deseja fazer isso pela Internet ou pessoalmente:

-   **Através da Internet:** Isso requer algumas etapas de configuração extras, como baixar e usar um conjunto de ferramentas e cmdlets do Windows PowerShell. No entanto, não é necessário estar fisicamente em uma instalação da Microsoft para transferir a chave de locatário. A segurança é mantida pelos seguintes métodos:

    -   Você gera a chave de locatário de uma estação de trabalho offline, o que reduz a superfície de ataque.

    -   A chave de locatário é criptografada com uma KEK (Key Exchange Key - Chave de Troca de Chave), que permanece criptografada até que seja transferida para os HSMs do Azure RMS. Apenas a versão criptografada da chave de locatário deixa a estação de trabalho de origem.

    -   Uma ferramenta define propriedades na sua chave de locatário que se vincula à sua chave de locatário para a segurança mundial do Azure RMS. Portanto, após os HSMs do Azure RMS receberem e descriptografarem a chave de locatário, somente esses HSMs poderão usá-la. Sua chave de locatário não pode ser exportada. Essa associação é exigida pelos HSMs da Thales.

    -   O KEK (Key Exchange Key) que é usado para criptografar a chave de locatário é gerado dentro dos HSMs do Azure RMS e não é exportável. Os HSMs exigem que não haja nenhuma versão clara do KEK fora dos HSMs. Além disso, o conjunto de ferramentas inclui atestado da Thales de que a KEK não é exportável e foi gerada dentro de um HSM original que foi fabricado pela Thales.

    -   O conjunto de ferramentas inclui atestado da Thales de que o mundo de segurança do Azure RMS também foi gerado em um HSM original fabricado pela Thales. Isso comprova que a Microsoft está usando hardware original.

    -   A Microsoft usa KEKs separadas, bem como mundos de segurança separados em cada região geográfica, o que garante que a sua chave de locatário só pode ser utilizada em centros de dados na região em que você a criptografou. Por exemplo, uma chave de locatário de um cliente europeu não pode ser utilizada em centros de dados na América do Norte ou na Ásia.

    > [!NOTE]
    > Sua chave de locatário pode se mover com segurança em computadores e redes não confiáveis​​, pois é criptografada e protegida com permissões de nível de controle de acesso, o que torna utilizável apenas dentro de seus HSMs e HSMs da Microsoft para o Azure RMS. Você pode usar os scripts que são fornecidos no conjunto de ferramentas para verificar as medidas de segurança e ler mais informações sobre como isso funciona a partir da Thales: [Gerenciamento de chaves de hardware na nuvem do RMS](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **Pessoalmente:** Isso requer que você entre em contato com os Serviços de Atendimento ao Cliente da Microsoft (CSS) para agendar uma consulta de transferência de chave para o Azure RMS. Será necessário viajar para um escritório da Microsoft em Redmond, Washington, nos Estados Unidos, para transferir a chave de locatário para o mundo de segurança do Azure RMS.

### <a name="BKMK_BYOK_Internet"></a>Gerar e transferir a chave de locatário - pela Internet
Use os seguintes procedimentos se quiser transferir a chave de locatário pela Internet, em vez de viajar para uma instalação da Microsoft para transferir a chave de locatário pessoalmente:

-   [Prepare a sua estação de trabalho conectada à Internet](plan-implement-tenant-key.md#BKMK_InternetPrepareWorkstation)

-   [Prepare a sua estação de trabalho desconectada](plan-implement-tenant-key.md#BKMK_DisconnectedPrepareWorkstation)

-   [Gerar sua chave de locatário](plan-implement-tenant-key.md#BKMK_InternetGenerate)

-   [Prepare sua chave de locatário para transferência](plan-implement-tenant-key.md#BKMK_InternetPrepareTransfer)

-   [Transfira sua chave de locatário para o Azure RMS](plan-implement-tenant-key.md#BKMK_InternetTransfer)

#### <a name="BKMK_InternetPrepareWorkstation"></a>Prepare a sua estação de trabalho conectada à Internet
Para preparar sua estação de trabalho que está conectada à Internet, siga estas 3 etapas:

-   [Etapa 1: Instale o Windows PowerShell para Azure Rights Management](plan-implement-tenant-key.md#BKMK_PrepareInternetConnectedWorkstation1)

-   [Etapa 2: Obtenha sua ID de locatário do Active Directory do Azure](plan-implement-tenant-key.md#BKMK_PrepareInternetConnectedWorkstation2)

-   [Etapa 3: Baixe o conjunto de ferramentas do BYOK](plan-implement-tenant-key.md#BKMK_PrepareInternetConnectedWorkstation3)

##### <a name="BKMK_PrepareInternetConnectedWorkstation1"></a>Etapa 1: Instale o Windows PowerShell para Azure Rights Management
Na estação de trabalho conectada à Internet, baixe e instale o módulo do Windows PowerShell para o Azure Rights Management.

> [!NOTE]
> Se você já baixou previamente este módulo do Windows PowerShell, execute o seguinte comando para verificar se o seu número de versão é, pelo menos, 2.1.0.0: `(Get-Module aadrm -ListAvailable).Version`

Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

##### <a name="BKMK_PrepareInternetConnectedWorkstation2"></a>Etapa 2: Obtenha sua ID de locatário do Active Directory do Azure
Inicie o Windows PowerShell com a opção **Executar como administrador** e, em seguida, execute os seguintes comandos:

-   Use o cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) para estabelecer conexão com o serviço do Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando solicitado, insira suas credenciais de administrador de locatário [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, você usará uma conta que seja um administrador global do Azure Active Directory ou do Office 365).

-   Use o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para exibir a configuração do seu locatário:

    ```
    Get-AadrmConfiguration
    ```
    Da saída, salve o GUID da primeira linha (BPOSId). Essa é sua ID de locatário do Active Directory do Azure, que mais tarde será necessária ao preparar sua chave de locatário para carregar.

-   Use o cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para sair do serviço do Azure RMS até que você esteja pronto para fazer upload da sua chave:

    ```
    Disconnect-AadrmService
    ```

Não feche a janela do Windows PowerShell.

##### <a name="BKMK_PrepareInternetConnectedWorkstation3"></a>Etapa 3: Baixe o conjunto de ferramentas do BYOK
Vá para o Centro de Download da Microsoft e [baixe o conjunto de ferramentas do BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) para a sua região:

|Região|Nome do pacote|
|----------|----------------|
|América do Norte|AzureRMS-BYOK-tools-UnitedStates.zip|
|Ocidental|AzureRMS-BYOK-tools-Europe.zip|
|Ásia|AzureRMS-BYOK-tools-AsiaPacific.zip|
O conjunto de ferramentas inclui o seguinte:

-   Um pacote de KEK (Chave de Troca de Chaves) que tem um nome que começa com **BYOK-KEK-pkg-**.

-   Um pacote do Security World que tem um nome que começa com **BYOK-SecurityWorld-pkg-**.

-   Um script python chamado **verifykeypackage.py**.

-   Um arquivo executável de linha de comando chamado **KeyTransferRemote.exe**, um arquivo de metadados chamado **KeyTransferRemote.exe.config** e as DLLs associadas.

-   Um pacote redistribuível do Visual C++, chamado **vcredist_x64.exe**.

Copie o pacote para uma unidade USB ou outro armazenamento portátil.

#### <a name="BKMK_DisconnectedPrepareWorkstation"></a>Prepare a sua estação de trabalho desconectada
Para preparar sua estação de trabalho que não está conectada a uma rede (Internet ou sua rede interna), siga estas 2 etapas:

-   [Etapa 1: Prepare a estação de trabalho desconectada com o HSM da Thales](plan-implement-tenant-key.md#BKMK_PrepareDisconnectedWorkstation1)

-   [Etapa 2: Instale o conjunto de ferramentas BYOK na estação de trabalho desconectada](plan-implement-tenant-key.md#BKMK_PrepareDisconnectedWorkstation2)

##### <a name="BKMK_PrepareDisconnectedWorkstation1"></a>Etapa 1: Prepare a estação de trabalho desconectada com o HSM da Thales
Na estação de trabalho desconectada, instale o software de suporte nCipher (Thales) em um computador com Windows e anexe um HSM da Thales a esse computador.

Certifique-se de que as ferramentas Thales estão no caminho **(%nfast_home%\bin** e **%nfast_home%\python\bin**). Por exemplo, digite o seguinte:

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Para obter mais informações, consulte o guia do usuário fornecido com o HSM da Thales ou visite o site da Thales para Azure RMS em [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

##### <a name="BKMK_PrepareDisconnectedWorkstation2"></a>Etapa 2: Instale o conjunto de ferramentas BYOK na estação de trabalho desconectada
Copie o pacote de conjunto de ferramentas BYOK da unidade USB ou de outros portáteis de armazenamento e faça o seguinte:

1.  Extraia os arquivos do pacote baixado em qualquer pasta.

2.  Nessa pasta, execute o vcredist_x64.exe.

3.  Siga as instruções para instalar os componentes de tempo de execução do Visual C++ para o Visual Studio 2012.

#### <a name="BKMK_InternetGenerate"></a>Gerar sua chave de locatário
Na estação de trabalho desconectada, siga estas três etapas para gerar sua própria chave de locatário:

-   [Etapa 1: Crie um mundo de segurança](plan-implement-tenant-key.md#BKMK_InternetGenerate1)

-   [Etapa 2: Valide o pacote baixado](plan-implement-tenant-key.md#BKMK_InternetGenerate2)

-   [Etapa 3: Crie uma nova chave](plan-implement-tenant-key.md#BKMK_InternetGenerate3)

##### <a name="BKMK_InternetGenerate1"></a>Etapa 1: Crie um mundo de segurança
Inicie um prompt de comando e execute o programa do novo mundo Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa cria um arquivo **Security World** em %NFAST_KMDATA%\local\world, que corresponde à pasta C:\ProgramData\nCipher\Key Management Data\local. É possível usar valores diferentes para o quorum, mas no nosso exemplo, você será solicitado a digitar três cartões e pins em branco para cada um. Em seguida, os dois cartões deverão ter acesso administrativo ao mundo de segurança (o quorum especificado).  Esses cartões se tornam o **Conjunto de Cartões do Administrador** para o novo mundo de segurança. Neste estágio, você pode especificar a senha ou PIN para cada cartão ACS ou adicioná-la mais tarde com um comando.

> [!TIP]
> Você pode verificar o status da configuração atual de seu HSM usando o comando `nkminfo` .

Em seguida, faça o seguinte:

1.  Instale o provedor de Thales GNV como descrito na documentação da Thales e configure-o para usar o novo mundo de segurança.

2.  Faça backup do arquivo world em **%nfast_kmdata%\local**. Assegure e proteja o arquivo de mundo, os Cartões de administrador e seus pins, e certifique-se de que ninguém mais tenha acesso a mais de um cartão.

##### <a name="BKMK_InternetGenerate2"></a>Etapa 2: Valide o pacote baixado
Esta etapa é opcional, mas recomendada para que você possa validar o seguinte:

-   A chave de troca de chave que está incluída no conjunto de ferramentas foi gerada a partir de um HSM da Thales original.

-   O hash para o Azure RMS Security World que está incluído no conjunto de ferramentas foi gerado em um Thales HSM genuíno.

-   A chave de troca de chave é não exportável.

> [!NOTE]
> Para validar o pacote baixado, o HSM deve estar conectado, ligado e deve ter um mundo de segurança nele (como o que você acabou de criar).

###### Para validar o pacote baixado

1.  Execute o script verifykeypackage.py digitando uma das seguintes opções, dependendo da sua região:

    -   Para a América do Norte:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Para a Europa:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Para a Ásia:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > O software Thales inclui um intérprete Python em %NFAST_HOME%\python\bin

2.  Confirme que você vê o seguinte, que indica a validação bem-sucedida: **Resultado:  ÊXITO**

Este script valida a cadeia do assinante em relação à chave raiz Thales. O hash dessa chave raiz está inserido no script e seu valor deve ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Você também pode confirmar esse valor separadamente visitando o [site da Thales](http://www.thalesesec.com/).

Agora você está pronto para criar uma nova chave que será a sua chave de locatário do RMS.

##### <a name="BKMK_InternetGenerate3"></a>Etapa 3: Crie uma nova chave
Gere uma chave CNG usando os programas **generatekey** e **cngimport** da Thales.

Execute o seguinte comando para gerar a chave:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Ao executar este comando, use estas instruções:

-   O parâmetro **protect** deve ser definido para o valor **module**, conforme mostrado. Isso cria uma chave protegida por módulo. O conjunto de ferramentas BYOK não dá suporte a chaves protegidas por OCS.

-   Para tamanho de chave, recomendamos 2048, mas também suporta chaves RSA de 1024 bits para clientes AD RMS existentes que tenham essas chaves e estejam migrando para o Azure RMS.

-   Substitua o valor de *contosokey* pelo **ident** e **plainname** com qualquer valor de cadeia de caracteres. Para minimizar custos administrativos e reduzir o risco de erros, recomendamos o uso do mesmo valor para os dois e o uso de todos os caracteres minúsculos.

-   O pubexp é deixado em branco (padrão) neste exemplo, mas você pode especificar valores específicos. Para obter mais informações, consulte a documentação da Thales.

Em seguida, execute o seguinte comando para importar a chave para CNG:

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
Ao executar este comando, use estas instruções:

-   Substitua *contosokey* pelo mesmo valor especificado na [Etapa 1: Criar um mundo de segurança](plan-implement-tenant-key.md#BKMK_InternetGenerate1) da seção *Gerar sua chave de locatário*.

-   Use a opção **-M** para que a chave seja adequada para esse cenário. Sem isso, a chave resultante será uma chave específica do usuário para o usuário atual.

-   A opção **appname** é o nome do aplicativo relatado no arquivo de chave. Se você usou essas instruções para criar uma nova chave, usamos o valor de simples, conforme mostrado no comando. No entanto, se você estiver migrando uma chave protegida por HSM para uma migração do AD RMS para o Azure RMS, especifique seu nome existente nesse comando e nos comandos a seguir quando eles também usarem a opção appname.

Este comando cria um arquivo de chave de token na pasta %NFAST_KMDATA%\local com um nome iniciado por **key_caping_** seguido de um SID. Por exemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este arquivo contém uma chave criptografada.

> [!TIP]
> Você pode ver o status da configuração atual de suas chaves usando o comando `nkminfo –k` .

Faça backup deste arquivo de chave de token em um local seguro.

> [!IMPORTANT]
> Quando transferir a chave para o Azure RMS posteriormente, a Microsoft não poderá exportar esta chave de volta para você, por isso é muito importante que seja feito o backup de sua chave e do mundo de segurança de forma segura. Entre em contato com a Thales para obter orientações e as melhores práticas para fazer backup da sua chave.

Agora você está pronto para transferir a chave de locatário do Azure RMS.

#### <a name="BKMK_InternetPrepareTransfer"></a>Prepare sua chave de locatário para transferência
Na estação de trabalho desconectada, siga estas quatro etapas para preparar sua própria chave de locatário:

-   [Etapa 1: Crie uma cópia de sua chave com permissões reduzidas](plan-implement-tenant-key.md#BKMK_InternetPrepareTransfer1)

-   [Etapa 2: Inspecione a nova cópia da chave](plan-implement-tenant-key.md#BKMK_InternetPrepareTransfer2)

-   [Etapa 3: Criptografe sua chave usando o Key Exchange Key da Microsoft](plan-implement-tenant-key.md#BKMK_InternetPrepareTransfer3)

-   [Etapa 4: Copie o pacote de transferência de chave para a estação de trabalho conectada à Internet](plan-implement-tenant-key.md#BKMK_InternetPrepareTransfer4)

##### <a name="BKMK_InternetPrepareTransfer1"></a>Etapa 1: Crie uma cópia de sua chave com permissões reduzidas
Para reduzir as permissões em sua chave de locatário, faça o seguinte:

-   Em um prompt de comando, execute uma das seguintes opções, dependendo da sua região:

    -   Para a América do Norte:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Para a Europa:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Para a Ásia:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

Ao executar este comando, substitua *contosokey* pelo mesmo valor especificado na [Etapa 1: Crie um mundo de segurança](plan-implement-tenant-key.md#BKMK_InternetGenerate1) da seção *Gerar sua chave de locatário*.

Você será solicitado a conectar seus cartões de ACS do mundo de segurança e, se for especificado, sua senha ou PIN.

Ao concluir o comando, você verá **Resultado: SUCCESSO** e a cópia da sua chave de locatário com permissões reduzidas estará no arquivo chamado key_xferacId_*&lt;contosokey&gt;*.

##### <a name="BKMK_InternetPrepareTransfer2"></a>Etapa 2: Inspecione a nova cópia da chave
Opcionalmente, execute os utilitários da Thales para confirmar as permissões mínimas na nova chave de locatário:

-   aclprint.py:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Ao executar este comando, substitua *contosokey* pelo mesmo valor especificado na [Etapa 1: Crie um mundo de segurança](plan-implement-tenant-key.md#BKMK_InternetGenerate1) da seção *Gerar sua chave de locatário*.

##### <a name="BKMK_InternetPrepareTransfer3"></a>Etapa 3: Criptografe sua chave usando o Key Exchange Key da Microsoft
Execute um dos seguintes comandos, dependendo da sua região:

-   Para a América do Norte:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Para a Europa:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Para a Ásia:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

Ao executar este comando, use estas instruções:

-   Substitua *contosokey* pelo identificador usado para gerar a chave na [Etapa 1: Criar um mundo de segurança](plan-implement-tenant-key.md#BKMK_InternetGenerate1) da seção *Gerar sua chave de locatário*.

-   Substitua *GUID* pela ID do locatário do Azure Active Directory recuperada na [Etapa 2: Obter sua ID de locatário do Azure Active Directory](plan-implement-tenant-key.md#BKMK_PrepareInternetConnectedWorkstation2) da seção *Preparar sua estação de trabalho conectada à Internet*.

-   Substitua *ContosoFirstKey* por um rótulo que será usado para o nome do arquivo de saída.

Quando isso for concluído com êxito, a mensagem **Resultado: SUCESSO** será exibida e haverá um novo arquivo na pasta atual com o seguinte nome: TransferPackage-*ContosoFirstkey*.byok

##### <a name="BKMK_InternetPrepareTransfer4"></a>Etapa 4: Copie o pacote de transferência de chave para a estação de trabalho conectada à Internet
Use uma unidade USB ou outro armazenamento portátil para copiar o arquivo de saída da etapa anterior (KeyTransferPackage-*ContosoFirstkey*.byok) para sua estação de trabalho conectada à Internet.

> [!NOTE]
> Use as práticas de segurança para proteger o arquivo, porque ele inclui sua chave privada.

#### <a name="BKMK_InternetTransfer"></a>Transfira sua chave de locatário para o Azure RMS
Na estação de trabalho conectada à Internet, siga estas 3 etapas para transferir sua nova chave de locatário para o Azure RMS:

-   [Etapa 1: Conectar ao Azure RMS](plan-implement-tenant-key.md#BKMK_InternetTransfer1)

-   [Etapa 2: Faça upload do pacote da chave](plan-implement-tenant-key.md#BKMK_InternetTransfer2)

-   [Etapa 3: Enumere suas chaves de locatário, se necessário](plan-implement-tenant-key.md#BKMK_InternetTransfer3)

##### <a name="BKMK_InternetTransfer1"></a>Etapa 1: Conectar ao Azure RMS
Volte para a janela do Windows PowerShell e digite o seguinte:

1.  Reconecte ao serviço do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]:

    ```
    Connect-AadrmService
    ```

2.  Use o cmdlet [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) para ver sua configuração atual da chave de locatário:

    ```
    Get-AadrmKeys
    ```

##### <a name="BKMK_InternetTransfer2"></a>Etapa 2: Faça upload do pacote da chave
Use o cmdlet [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) para fazer upload do pacote de transferência da chave que você copiou da estação de trabalho desconectada:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Você será solicitado a confirmar essa ação. É importante entender que essa ação não poderá ser desfeita. Ao fazer o carregamento de uma chave de locatário, ela automaticamente se torna a chave de locatário principal da sua organização e os usuários começarão a usar essa chave de locatário quando protegerem documentos e arquivos.

Se o upload for bem-sucedido, a seguinte mensagem será exibida: **O serviço do Rights Management adicionou a chave com sucesso.**

Espere por um atraso de replicação para que a alteração se propague para todos os centros de dados do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

##### <a name="BKMK_InternetTransfer3"></a>Etapa 3: Enumere suas chaves de locatário, se necessário
Use o cmdlet Get-AadrmKeys novamente para ver a alteração em sua chave de locatário e sempre que quiser ver uma lista de suas chaves de locatário. As chaves de locatário exibidas incluem a chave de locatário inicial que a Microsoft gerou para você e todas as chaves de locatário que você adicionou:

```
Get-AadrmKeys
```
A chave de locatário que está marcada como **Ativa** é a que a sua organização está usando atualmente para proteger documentos e arquivos.

Agora você concluiu todas as etapas necessárias para trazer sua própria chave pela Internet e pode ir para as [Próximas etapas](plan-implement-tenant-key.md#BKMK_NextSteps).

### <a name="BKMK_BYOK_InPerson"></a>Gerar e transferir sua chave de locatário pessoalmente
Utilize os procedimentos a seguir se não quiser transferir sua chave de locatário pela Internet, mas em vez disso, quiser transferir sua chave de locatário pessoalmente.

-   [Gerar sua chave de locatário](plan-implement-tenant-key.md#BKMK_GenerateKey)

-   [Transfira sua chave de locatário para o Azure RMS](plan-implement-tenant-key.md#BKMK_Transfer)

#### <a name="BKMK_GenerateKey"></a>Gerar sua chave de locatário
Para gerar sua chave de locatário, siga estas 3 etapas:

-   [Etapa 1: Prepare uma estação de trabalho com HSM da Thales](plan-implement-tenant-key.md#BKMK_GenerateYourKey1)

-   [Etapa 2: Crie um mundo de segurança](plan-implement-tenant-key.md#BKMK_GenerateYourKey2)

-   [Etapa 3: Crie uma nova chave](plan-implement-tenant-key.md#BKMK_GenerateYourKey3)

##### <a name="BKMK_GenerateYourKey1"></a>Etapa 1: Prepare uma estação de trabalho com HSM da Thales
Instale o software de suporte nCipher (Thales) em um computador com Windows. Anexe um HSM da Thales a esse computador. Certifique-se de que as ferramentas Thales estejam em seu caminho. Para obter mais informações, consulte o guia do usuário fornecido com o HSM da Thales ou visite o site da Thales para Azure RMS em [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

##### <a name="BKMK_GenerateYourKey2"></a>Etapa 2: Crie um mundo de segurança
Inicie um prompt de comando e execute o programa do novo mundo Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa cria um arquivo **Security World** em %NFAST_KMDATA%\local\world, que corresponde à pasta C:\ProgramData\nCipher\Key Management Data\local. É possível usar valores diferentes para o quorum, mas no nosso exemplo, você será solicitado a digitar três cartões e pins em branco para cada um. Então, os dois cartões darão acesso completo ao mundo de segurança.  Esses cartões se tornam o **Conjunto de Cartões do Administrador** para o novo mundo de segurança.

Em seguida, faça o seguinte:

1.  Instale o provedor de Thales GNV como descrito na documentação da Thales e configure-o para usar o novo mundo de segurança.

2.  Faça backup do arquivo do mundo. Assegure e proteja o arquivo de mundo, os Cartões de administrador e seus pins, e certifique-se de que ninguém mais tenha acesso a mais de um cartão.

Agora você está pronto para criar uma nova chave que será a sua chave de locatário do RMS.

##### <a name="BKMK_GenerateYourKey3"></a>Etapa 3: Crie uma nova chave
Gere uma chave CNG usando os programas **generatekey** e **cngimport** da Thales.

Execute o seguinte comando para gerar a chave:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Ao executar este comando, use estas instruções:

-   O parâmetro **protect** deve ser definido para o valor **module**, conforme mostrado. Isso cria uma chave protegida por módulo. O conjunto de ferramentas BYOK não dá suporte a chaves protegidas por OCS.

-   Para tamanho de chave, recomendamos 2048, mas também suporta chaves RSA de 1024 bits para clientes AD RMS existentes que tenham essas chaves e estejam migrando para o Azure RMS.

-   Substitua o valor de *contosokey* pelo **ident** e **plainname** com qualquer valor de cadeia de caracteres. Para minimizar custos administrativos e reduzir o risco de erros, recomendamos o uso do mesmo valor para os dois e o uso de todos os caracteres minúsculos.

-   O pubexp é deixado em branco (padrão) neste exemplo, mas você pode especificar valores específicos. Para obter mais informações, consulte a documentação da Thales.

Em seguida, execute o seguinte comando para importar a chave para CNG:

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Ao executar este comando, use estas instruções:

-   Substitua *contosokey* pelo mesmo valor especificado na Etapa 1.

-   Use a opção **-M** para que a chave seja adequada para esse cenário. Sem isso, a chave resultante será uma chave específica do usuário para o usuário atual.

Este comando cria um arquivo de chave de token na pasta %NFAST_KMDATA%\local com um nome iniciado por **key_caping_** seguido de um SID. Por exemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este arquivo contém uma chave criptografada.

Faça backup deste arquivo de chave de token em um local seguro.

> [!IMPORTANT]
> Mais tarde, ao transferir sua chave para o Azure RMS, a Microsoft terá uma cópia não recuperável de sua chave. Isso significa que ninguém poderá recuperar sua chave dos HSMs na Microsoft. Isso permite que você mantenha o controle exclusivo sobre sua chave de locatário. Por isso, é extremamente importante que seja feito o backup de sua chave e do mundo da segurança de forma segura. Entre em contato com a Thales para obter orientações e as melhores práticas para fazer backup da sua chave.

Agora você está pronto para transferir a sua chave de locatário do Azure RMS.

#### <a name="BKMK_Transfer"></a>Transfira sua chave de locatário para o Azure RMS
Após gerar sua própria chave, será necessário transferi-la para o Azure RMS antes de usá-la. Para o mais alto nível de segurança, esta transferência é um processo manual que exige que você vá ao escritório da Microsoft em Redmond, em Washington, nos Estados Unidos. Para concluir esse processo, siga estas 3 etapas:

-   [Etapa 1: Traga sua chave para a Microsoft](plan-implement-tenant-key.md#BKMK_TransferYourKey1)

-   [Etapa 2: Transfira sua chave para o mundo de segurança do Windows Azure RMS](plan-implement-tenant-key.md#BKMK_TransferYourKey2)

-   [Etapa 3: Procedimentos de encerramento](plan-implement-tenant-key.md#BKMK_TransferYourKey3)

###### Etapa 1: Traga sua chave para a Microsoft

-   Entre em contato com os Serviços de Atendimento ao Cliente da Microsoft (CSS) para agendar uma consulta de transferência de chave para o Azure RMS. Traga o seguinte para a Microsoft em Redmond:

    -   O quórum de seus cartões administrativos. Se você seguiu as instruções anteriores em [Etapa 2: Criar um mundo de segurança](plan-implement-tenant-key.md#BKMK_GenerateYourKey2), esses são dois dos seus três cartões.

    -   Pessoal autorizado a levar seus cartões e pins administrativos, geralmente dois (um para cada cartão).

    -   Seu arquivo do Security World (%NFAST_KMDATA%\local\world) em uma unidade USB.

    -   Seu arquivo de chave de token em uma unidade USB.

###### Etapa 2: Transfira sua chave para o mundo de segurança do Windows Azure RMS

1.  Ao chegar na Microsoft para transferir sua chave, acontece o seguinte:

    -   A Microsoft fornece uma estação de trabalho offline que tem um HSM da Thales anexo, um software Thales instalado e um arquivo Azure RMS World Security pré-carregado na pasta C:\Temp\Destination.

    -   Nessa estação de trabalho, você carrega seu arquivo do Security World e o arquivo de chave de token da sua unidade USB para a pasta C:\Temp\Source.

    -   Os operadores do Azure RMS transferem de forma segura sua chave para o mundo da segurança do Azure RMS com utilitários Thales.

    Este processo será semelhante ao seguinte, onde o último parâmetro de key-xfer-im, neste exemplo, é substituído pelo nome do seu arquivo de chave de token:

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  O Mk-reprogram pedirá a você e aos operadores do Azure RMS que conectem seus respectivos cartões de administrador e pins. Isso comanda a saída de um arquivo de chave de símbolo no C:\Temp\Destination que contém sua chave protegida pelo mundo de segurança Azure RMS.

###### Etapa 3: Procedimentos de encerramento

-   Em sua presença, os operadores do Azure RMS fazem o seguinte:

    -   Executam uma ferramenta que a Microsoft desenvolveu em colaboração com a Thales que remove duas permissões: A permissão para recuperar a chave e a permissão para alterar as permissões. Após ter feito isso, esta cópia de sua chave será bloqueada para o mundo de segurança do Azure RMS. Os HSMs da Thales não permitirão que os operadores do Azure RMS com seus cartões de administrador recuperem a cópia de texto sem formatação de sua chave.

    -   Copie o arquivo de chave resultante para uma unidade USB para posteriormente fazer upload para o serviço do Azure RMS.

    -   Redefina o HSM para as configurações de fábrica e limpe a estação de trabalho.

Agora você concluiu todas as etapas necessárias para trazer sua própria chave pessoalmente e pode voltar para sua organização para as próximas etapas.

## <a name="BKMK_NextSteps"></a>Próximas etapas

1.  Comece a usar sua chave de locatário:

    -   Se ainda não tiver feito isso, será necessário agora ativar o Rights Management de modo que sua organização possa começar a usar o RMS. Os usuários começam imediatamente a utilizar a chave de locatário (gerenciada pela Microsoft ou por você).

        Para obter mais informações sobre uma ativação, consulte [Ativando o Microsoft Azure Rights Management](activate-service.md).

    -   Se já tiver ativado o Rights Management e decidir gerenciar sua própria chave de locatário, os usuários farão a transição gradual da chave de locatário antiga para a nova chave de locatário, e essa transição escalonada pode levar algumas semanas para ser concluída. Os documentos e arquivos que foram protegidos com a chave de locatário antiga, permanecem acessíveis para usuários autorizados.

2.  Considere habilitar o log de uso, que registra todas as transações que o RMS executa.

    Se você decidiu gerenciar sua própria chave de locatário, o log inclui informações sobre como usar sua chave de locatário. Consulte o exemplo a seguir de um arquivo de log exibido no Excel, onde os Tipos de solicitação **Descriptografar** e **SignDigest** mostram que a chave de locatário está sendo usada.

    ![](./media/RMS_Logging.gif)

    Para obter mais informações sobre registro em log de uso, consulte [Registrando em log e analisando o uso do Azure Rights Management](log-analyze-usage.md).

3.  Mantenha sua chave de locatário.

    Para obter mais informações, consulte [Operações para Sua chave de locatário do Azure Rights Management](operations-tenant-key.md).

## Consulte também
[Configurando o Azure Rights Management](configuring-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


