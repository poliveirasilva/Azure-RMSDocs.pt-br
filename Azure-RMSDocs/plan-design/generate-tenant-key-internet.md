---
title: "Gerar e transferir sua chave de locatário - pela Internet | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 20cfa722f7008c52f4fbc219a4de04c50ee3548d


---


# Gerar e transferir a chave de locatário - pela Internet

*Aplica-se a: Azure Rights Management, Office 365*

Use os seguintes procedimentos se decidir [gerenciar sua própria chave de locatário](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) e quiser transferi-la pela Internet, em vez de viajar para uma instalação da Microsoft para transferir a chave de locatário pessoalmente:


## Prepare a sua estação de trabalho conectada à Internet
Para preparar sua estação de trabalho que está conectada à Internet, siga estas 3 etapas:

-   [Etapa 1: Instale o Windows PowerShell para Azure Rights Management](#step-1-install-windows-powershell-for-azure-rights-management)

-   [Etapa 2: Obtenha sua ID de locatário do Active Directory do Azure](#step-2-get-your-azure-active-directory-tenant-id)

-   [Etapa 3: Baixe o conjunto de ferramentas do BYOK](#step-3-download-the-byok-toolset)

### Etapa 1: Instale o Windows PowerShell para Azure Rights Management
Na estação de trabalho conectada à Internet, baixe e instale o módulo do Windows PowerShell para o Azure Rights Management.

> [!NOTE]
> Se você já baixou previamente este módulo do Windows PowerShell, execute o seguinte comando para verificar se o seu número de versão é, pelo menos, 2.1.0.0: `(Get-Module aadrm -ListAvailable).Version`

Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

### Etapa 2: Obtenha sua ID de locatário do Active Directory do Azure
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

### Etapa 3: Baixe o conjunto de ferramentas do BYOK
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

## Prepare a sua estação de trabalho desconectada
Para preparar sua estação de trabalho que não está conectada a uma rede (Internet ou sua rede interna), siga estas 2 etapas:

-   [Etapa 1: Prepare a estação de trabalho desconectada com o HSM da Thales](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [Etapa 2: Instale o conjunto de ferramentas BYOK na estação de trabalho desconectada](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### Etapa 1: Prepare a estação de trabalho desconectada com o HSM da Thales
Na estação de trabalho desconectada, instale o software de suporte nCipher (Thales) em um computador com Windows e anexe um HSM da Thales a esse computador.

Certifique-se de que as ferramentas Thales estão no caminho **(%nfast_home%\bin** e **%nfast_home%\python\bin**). Por exemplo, digite o seguinte:

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Para obter mais informações, consulte o guia do usuário fornecido com o HSM da Thales ou visite o site da Thales para Azure RMS em [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Etapa 2: Instale o conjunto de ferramentas BYOK na estação de trabalho desconectada
Copie o pacote de conjunto de ferramentas BYOK da unidade USB ou de outros portáteis de armazenamento e faça o seguinte:

1.  Extraia os arquivos do pacote baixado em qualquer pasta.

2.  Nessa pasta, execute o vcredist_x64.exe.

3.  Siga as instruções para instalar os componentes de tempo de execução do Visual C++ para o Visual Studio 2012.

## Gerar sua chave de locatário
Na estação de trabalho desconectada, siga estas três etapas para gerar sua própria chave de locatário:

-   [Etapa 1: Crie um mundo de segurança](#step-1-create-a-security-world)

-   [Etapa 2: Valide o pacote baixado](#step-2-validate-the-downloaded-package)

-   [Etapa 3: Crie uma nova chave](#step-3-create-a-new-key)

### Etapa 1: Crie um mundo de segurança
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

### Etapa 2: Valide o pacote baixado
Esta etapa é opcional, mas recomendada para que você possa validar o seguinte:

-   A chave de troca de chave que está incluída no conjunto de ferramentas foi gerada a partir de um HSM da Thales original.

-   O hash para o Azure RMS Security World que está incluído no conjunto de ferramentas foi gerado em um Thales HSM genuíno.

-   A chave de troca de chave é não exportável.

> [!NOTE]
> Para validar o pacote baixado, o HSM deve estar conectado, ligado e deve ter um mundo de segurança nele (como o que você acabou de criar).

#### Para validar o pacote baixado

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

### Etapa 3: Crie uma nova chave
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

-   Substitua *contosokey* pelo mesmo valor especificado na [Etapa 1: Criar um mundo de segurança](#step-1-create-a-security-world) da seção *Gerar sua chave de locatário*.

-   Use a opção **-M** para que a chave seja adequada para esse cenário. Sem isso, a chave resultante será uma chave específica do usuário para o usuário atual.

-   A opção **appname** é o nome do aplicativo relatado no arquivo de chave. Se você usou essas instruções para criar uma nova chave, usamos o valor de simples, conforme mostrado no comando. No entanto, se você estiver migrando uma chave protegida por HSM para uma migração do AD RMS para o Azure RMS, especifique seu nome existente nesse comando e nos comandos a seguir quando eles também usarem a opção appname.

Esse comando cria um arquivo de chave de token na pasta %NFAST_KMDATA%\local com um nome iniciado por **key_caping`_`** seguido de um SID. Por exemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este arquivo contém uma chave criptografada.

> [!TIP]
> Você pode ver o status da configuração atual de suas chaves usando o comando `nkminfo –k` .

Faça backup deste arquivo de chave de token em um local seguro.

> [!IMPORTANT]
> Quando transferir a chave para o Azure RMS posteriormente, a Microsoft não poderá exportar esta chave de volta para você, por isso é muito importante que seja feito o backup de sua chave e do mundo de segurança de forma segura. Entre em contato com a Thales para obter orientações e as melhores práticas para fazer backup da sua chave.

Agora você está pronto para transferir a chave de locatário do Azure RMS.

## Prepare sua chave de locatário para transferência
Na estação de trabalho desconectada, siga estas quatro etapas para preparar sua própria chave de locatário:

-   [Etapa 1: Crie uma cópia de sua chave com permissões reduzidas](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [Etapa 2: Inspecione a nova cópia da chave](#step-2-inspect-the-new-copy-of-the-key)

-   [Etapa 3: Criptografe sua chave usando o Key Exchange Key da Microsoft](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [Etapa 4: Copie o pacote de transferência de chave para a estação de trabalho conectada à Internet](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### Etapa 1: Crie uma cópia de sua chave com permissões reduzidas
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

Ao executar este comando, substitua *contosokey* pelo mesmo valor especificado na [Etapa 1: Crie um mundo de segurança](#step-1-create-a-security-world) da seção *Gerar sua chave de locatário*.

Você será solicitado a conectar seus cartões de ACS do mundo de segurança e, se for especificado, sua senha ou PIN.

Ao concluir o comando, você verá **Resultado: ÊXITO** e a cópia da sua chave de locatário com permissões reduzidas estará no arquivo nomeado key_xferacId_*&lt;contosokey&gt;*.

### Etapa 2: Inspecione a nova cópia da chave
Opcionalmente, execute os utilitários da Thales para confirmar as permissões mínimas na nova chave de locatário:

-   aclprint.py:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Ao executar este comando, substitua *contosokey* pelo mesmo valor especificado na [Etapa 1: Crie um mundo de segurança](#step-1-create-a-security-world) da seção *Gerar sua chave de locatário*.

### Etapa 3: Criptografe sua chave usando o Key Exchange Key da Microsoft
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

-   Substitua *contosokey* pelo identificador usado para gerar a chave na [Etapa 1: Criar um mundo de segurança](#step-1-create-a-security-world) da seção *Gerar sua chave de locatário*.

-   Substitua *GUID* pela ID do locatário do Azure Active Directory recuperada na [Etapa 2: Obter sua ID de locatário do Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id) da seção *Preparar sua estação de trabalho conectada à Internet*.

-   Substitua *ContosoFirstKey* por um rótulo que será usado para o nome do arquivo de saída.

Quando isso for concluído com êxito, a mensagem **Resultado: SUCESSO** será exibida e haverá um novo arquivo na pasta atual com o seguinte nome: TransferPackage-*ContosoFirstkey*.byok

### Etapa 4: Copie o pacote de transferência de chave para a estação de trabalho conectada à Internet
Use uma unidade USB ou outro armazenamento portátil para copiar o arquivo de saída da etapa anterior (KeyTransferPackage-*ContosoFirstkey*.byok) para sua estação de trabalho conectada à Internet.

> [!NOTE]
> Use as práticas de segurança para proteger o arquivo, porque ele inclui sua chave privada.

## Transfira sua chave de locatário para o Azure RMS
Na estação de trabalho conectada à Internet, siga estas 3 etapas para transferir sua nova chave de locatário para o Azure RMS:

-   [Etapa 1: Conectar ao Azure RMS](#step-1-connect-to-azure-rms)

-   [Etapa 2: Faça upload do pacote da chave](#step-2-upload-the-key-package)

-   [Etapa 3: Enumere suas chaves de locatário, se necessário](#step-3-enumerate-your-tenant-keys-as-needed)

### Etapa 1: Conectar ao Azure RMS
Volte para a janela do Windows PowerShell e digite o seguinte:

1.  Reconecte ao serviço do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]:

    ```
    Connect-AadrmService
    ```

2.  Use o cmdlet [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) para ver sua configuração atual da chave de locatário:

    ```
    Get-AadrmKeys
    ```

### Etapa 2: Faça upload do pacote da chave
Use o cmdlet [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) para fazer upload do pacote de transferência da chave que você copiou da estação de trabalho desconectada:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Você será solicitado a confirmar essa ação. É importante entender que essa ação não poderá ser desfeita. Ao fazer o carregamento de uma chave de locatário, ela automaticamente se torna a chave de locatário principal da sua organização e os usuários começarão a usar essa chave de locatário quando protegerem documentos e arquivos.

Se o upload for bem-sucedido, a seguinte mensagem será exibida: **O serviço do Rights Management adicionou a chave com sucesso.**

Espere por um atraso de replicação para que a alteração se propague para todos os centros de dados do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

### Etapa 3: Enumere suas chaves de locatário, se necessário
Use o cmdlet Get-AadrmKeys novamente para ver a alteração em sua chave de locatário e sempre que quiser ver uma lista de suas chaves de locatário. As chaves de locatário exibidas incluem a chave de locatário inicial que a Microsoft gerou para você e todas as chaves de locatário que você adicionou:

```
Get-AadrmKeys
```
A chave de locatário que está marcada como **Ativa** é a que a sua organização está usando atualmente para proteger documentos e arquivos.

Agora você concluiu todas as etapas necessárias para obter sua própria chave pela Internet e pode ir para as próximas etapas para planejar e implementar sua chave de locatário.


> [!div class="button"]
[Próximas etapas >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Jun16_HO4-->


