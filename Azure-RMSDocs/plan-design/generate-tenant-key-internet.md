---
title: "Gerar e transferir a chave de inquilino – através da Internet | Azure RMS"
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


# Gerar e transferir a chave de inquilino – através da Internet

*Aplica-se a: Azure Rights Management, Office 365*

Utilize os procedimentos seguintes se decidiu [gerir a sua própria chave de inquilino](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) e pretender transferi-la através da Internet em vez de a levar a uma instalação da Microsoft para transferir a chave de inquilino em pessoa:


## Preparar a estação de trabalho ligada à Internet
Para preparar a estação de trabalho que está ligada à Internet, siga estes 3 passos:

-   [Passo 1: instalar o Windows PowerShell para o Azure Rights Management](#step-1-install-windows-powershell-for-azure-rights-management)

-   [Passo 2: obter o ID de inquilino do Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id)

-   [Passo 3: transferir o conjunto de ferramentas BYOK](#step-3-download-the-byok-toolset)

### Passo 1: instalar o Windows PowerShell para o Azure Rights Management
Na estação de trabalho ligada à Internet, transfira e instale o módulo do Windows PowerShell para o Azure Rights Management.

> [!NOTE]
> Caso já tenha transferido este módulo do Windows PowerShell anteriormente, execute o seguinte comando para verificar se o seu número de versão é 2.1.0.0 ou posterior: `(Get-Module aadrm -ListAvailable).Version`

Para obter instruções de instalação, consulte [Instalar o Windows PowerShell para o Azure Rights Management](../deploy-use/install-powershell.md).

### Passo 2: obter o seu ID de inquilino do Azure Active Directory
Inicie o Windows PowerShell com a opção **Executar como administrador** e execute os seguintes comandos:

-   Utilize o cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) para efetuar uma ligação ao serviço Azure RMS:

    ```
    Connect-AadrmService
    ```
    Quando for solicitado, introduza as credenciais de administrador de inquilinos do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, utilizará uma conta de um administrador global do Azure Active Directory ou do Office 365).

-   Utilize o cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para ver a configuração do seu inquilino:

    ```
    Get-AadrmConfiguration
    ```
    A partir da saída, guarde o GUID da primeira linha (BPOSId). Este é o ID de inquilino do Azure Active Directory, que irá precisar mais tarde quando preparar a chave de inquilino para o carregamento.

-   Utilize o cmdlet [Desligar AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desligar do serviço Azure RMS até estar pronto para carregar a chave:

    ```
    Disconnect-AadrmService
    ```

Não feche a janela do Windows PowerShell.

### Passo 3: transferir o conjunto de ferramentas BYOK
Aceda ao Centro de Transferências da Microsoft e [transfira o conjunto de ferramentas BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) para sua região:

|Região|Nome do pacote|
|----------|----------------|
|América do Norte|AzureRMS-BYOK-tools-UnitedStates.zip|
|Europa|AzureRMS-BYOK-tools-Europe.zip|
|Ásia|AzureRMS-BYOK-tools-AsiaPacific.zip|
O conjunto de ferramentas inclui o seguinte:

-   Um pacote da Chave de Troca de Chaves (KEK) que tem um nome a começar com **BYOK-KEK-pkg-**.

-   Um pacote do Universo de Segurança que tem um nome que começa com **BYOK-SecurityWorld-pkg-**.

-   Um script de python com o nome **verifykeypackage.py**.

-   Um ficheiro executável da linha de comandos com o nome **KeyTransferRemote.exe**, um ficheiro de metadados com o nome **KeyTransferRemote.exe.config** e DLLs associados.

-   Um Visual C++ Redistributable Package, com o nome **vcredist_x64.exe**.

Copie o pacote para outro armazenamento portátil ou uma unidade USB.

## Preparar a estação de trabalho desligada
Para preparar a estação de trabalho que não está ligada a uma rede (Internet ou rede interna), siga estes 2 passos:

-   [Passo 1: preparar a estação de trabalho desligada com o HSM da Thales](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [Passo 2: instalar o conjunto de ferramentas BYOK na estação de trabalho desligada](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### Passo 1: preparar a estação de trabalho desligada com o HSM da Thales
Na estação de trabalho desligada, instale o software de suporte nCipher (Thales) num computador Windows e, em seguida, anexe um HSM da Thales a esse computador.

Certifique-se de que as ferramentas de Thales estão no seu caminho **(%nfast_home%\bin** e **%nfast_home%\python\bin**). Por exemplo, escreva o seguinte:

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Para mais informações, consulte o guia de utilizador incluído no HSM da Thales ou visite o Web site da Thales para o Azure RMS em [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Passo 2: instalar o conjunto de ferramentas BYOK na estação de trabalho desligada
Copie o conjunto de ferramentas BYOK da unidade USB ou de outro armazenamento portátil e, em seguida, faça o seguinte:

1.  Extraia os ficheiros do pacote transferido para qualquer pasta.

2.  Nessa pasta, execute o ficheiro vcredist_x64.exe.

3.  Siga as instruções para instalar os componentes do Visual C++ runtime para o Visual Studio 2012.

## Gerar a chave de inquilino
Na estação de trabalho desligada, siga estes 3 passos para gerar a sua própria chave de inquilino:

-   [Passo 1: criar um universo de segurança](#step-1-create-a-security-world)

-   [Passo 2: validar o pacote transferido](#step-2-validate-the-downloaded-package)

-   [Passo 3: criar uma nova chave](#step-3-create-a-new-key)

### Passo 1: criar um universo de segurança
Inicie uma linha de comandos e execute o programa de novo universo da Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa cria um ficheiro **Universo de Segurança** em %NFAST_KMDATA%\local\world, que corresponde à pasta C:\ProgramData\nCipher\Key Management Data\local. Pode utilizar valores diferentes para o quórum, mas no nosso exemplo é-lhe pedido que introduza três cartões em branco e pins para cada um deles. Em seguida, qualquer conjunto de dois cartões terá de ter acesso administrativo ao universo de segurança (o quórum especificado).  Estes cartões tornam-se o **Conjunto de Cartões do Administrador** para o novo universo de segurança. Nesta fase, pode especificar a palavra-passe ou o PIN para cada cartão de ACS ou adicioná-lo mais tarde com um comando.

> [!TIP]
> Pode verificar o estado de configuração atual do HSM ao utilizar o comando `nkminfo`.

Em seguida, faça o seguinte:

1.  Instale o fornecedor CNG da Thales conforme descrito na documentação da Thales e configure-o para utilizar o novo universo de segurança.

2.  Crie uma cópia de segurança do ficheiro do universo em **%nfast_kmdata%\local**. Proteja o ficheiro do universo, os Cartões de Administrador e os respetivos pins e certifique-se de que ninguém tem acesso a mais do que um cartão.

### Passo 2: validar o pacote transferido
Este passo é opcional, mas recomendado para que possa validar o seguinte:

-   A Chave de Troca de Chaves que está incluída no conjunto de ferramentas foi gerada a partir de um HSM da Thales genuíno.

-   O hash do Universo de Segurança do Azure RMS que está incluído no conjunto de ferramentas foi gerado num HSM da Thales genuíno.

-   A Chave de Troca de Chaves não é exportável.

> [!NOTE]
> Para validar o pacote transferido, o HSM tem de estar ligado e tem de ter um universo de segurança no mesmo (tal como o que acabou de criar).

#### Para validar o pacote transferido

1.  Execute o script verifykeypackage.py ao escrever um dos seguintes, consoante a sua região:

    -   Para a América do Norte

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
    > O software da Thales inclui um interpretador Python em %NFAST_HOME%\python\bin

2.  Confirme se vê o seguinte, que indica uma validação com êxito: **Resultado: ÊXITO**

Este script valida a cadeia de signatário até à chave de raiz da Thales. O hash desta chave de raiz é incorporado no script e o respetivo valor deve ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Também pode confirmar este valor separadamente, ao aceder ao [Web site da Thales](http://www.thalesesec.com/).

Agora está pronto para criar uma nova chave que será a sua chave de inquilino do RMS.

### Passo 3: criar uma nova chave
Gere uma chave CNG com os programas **generatekey** e **cngimport** da Thales.

Execute o seguinte comando para criar a chave:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Quando executar este comando, utilize estas instruções:

-   O parâmetro **protect** tem de ser definido para o valor **module**, conforme mostrado. Esta ação cria uma chave protegida por um módulo. O conjunto de ferramentas BYOK não suporta chaves protegidas por OCS.

-   Para o tamanho da chave, recomendamos chaves RSA de 2048 bits, mas também suportamos chaves de 1024 bits para clientes de AD RMS existentes que tenham essas chaves e estejam a migrar para o Azure RMS.

-   Substitua o valor *contosokey* por **ident** e **plainname** por qualquer valor da cadeia. Para minimizar as tarefas administrativas adicionais e reduzir o risco de erros, recomendamos que utilize o mesmo valor para ambos e utilize todos os carateres em minúsculas.

-   O pubexp fica em branco (predefinição) neste exemplo, mas pode especificar valores. Para mais informações, consulte a documentação da Thales.

Em seguida, execute o seguinte comando para importar a chave para a CNG:

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
Quando executar este comando, utilize estas instruções:

-   Substitua *contosokey* pelo mesmo valor que especificou no [Passo 1: criar um universo de segurança](#step-1-create-a-security-world) na secção *Gerar a chave de inquilino*.

-   Utilize a opção **-M** para que a chave seja adequada para este cenário. Sem esta ação, a chave resultante será uma chave específica para o utilizador atual.

-   A opção **appname** é o Nome da Aplicação reportado no ficheiro de chave. Se utilizou estas instruções para criar uma nova chave, utilizamos o valor de simples, tal como apresentado no comando. No entanto, se está a migrar uma chave protegida por HSM existente para uma migração do AD RMS para o Azure RMS, especifique o nome existente neste comando e os comandos que se seguem quando também utilizam a opção de appname.

Este comando cria um ficheiro de Chave com Token na pasta %NFAST_KMDATA%\local com um nome começado por **key_caping`_`** seguido de um SID. Por exemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este ficheiro contém uma chave encriptada.

> [!TIP]
> Pode verificar o estado de configuração atual das suas chaves ao utilizar o comando `nkminfo –k`.

Crie uma cópia de segurança deste Ficheiro de Chave com Token numa localização segura.

> [!IMPORTANT]
> Quando transferir a chave para o Azure RMS posteriormente, a Microsoft não lhe poderá exportar esta chave novamente, pelo que é extremamente importante que crie uma cópia de segurança da chave e do universo de segurança. Contacte a Thales para obter orientações e melhores práticas para criar a cópia de segurança da sua chave.

Agora está pronto para transferir a chave de inquilino para o Azure RMS.

## Preparar a transferência da chave de inquilino
Na estação de trabalho desligada, siga estes 4 passos para preparar a sua própria chave de inquilino:

-   [Passo 1: criar uma cópia da chave com permissões reduzidas](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [Passo 2: inspecionar a nova cópia da chave](#step-2-inspect-the-new-copy-of-the-key)

-   [Passo 3: encriptar a chave ao utilizar a Chave da Troca de Chaves da Microsoft](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [Passo 4: copiar o pacote de transferência da chave para a estação de trabalho ligada à Internet](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### Passo 1: criar uma cópia da chave com permissões reduzidas
Para reduzir as permissões na sua chave de inquilino, faça o seguinte:

-   Numa linha de comandos, execute um dos seguintes procedimentos, consoante a sua região:

    -   Para a América do Norte

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

Quando executar este comando, substitua *contosokey* pelo mesmo valor que especificou no [Passo 1: criar um universo de segurança](#step-1-create-a-security-world) na secção *Gerar a chave de inquilino*.

Ser-lhe-á pedido que ligue os cartões de ACS do universo de segurança e, se for especificado, a respetiva palavra-passe ou PIN.

Quando o comando for concluído, verá **Resultado: ÊXITO** e a cópia da chave de inquilino com permissões reduzidas vai estar no ficheiro denominado key_xferacId_*&lt;contosokey&gt;*.

### Passo 2: inspecionar a nova cópia da chave
Opcionalmente, execute os utilitários da Thales para confirmar as permissões mínimas na nova chave de inquilino:

-   aclprint.py:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Quando executar este comando, substitua *contosokey* pelo mesmo valor que especificou no [Passo 1: criar um universo de segurança](#step-1-create-a-security-world) na secção *Gerar a chave de inquilino*.

### Passo 3: encriptar a chave ao utilizar a Chave da Troca de Chaves da Microsoft
Execute um dos seguintes comandos, dependendo da sua região:

-   Para a América do Norte

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

Quando executar este comando, utilize estas instruções:

-   Substitua *contosokey* pelo identificador utilizado para gerar a chave no [Passo 1: Criar um universo de segurança](#step-1-create-a-security-world) na secção *Gerar a chave de inquilino*.

-   Substitua *GUID* pelo ID de inquilino do Azure Active Directory que obteve no [Passo 2: obter o ID de inquilino do Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id) na secção *Preparar a estação de trabalho ligada à Internet*.

-   Substitua *ContosoFirstKey* por uma etiqueta que será utilizada para o nome do ficheiro de saída.

Quando esta ação for concluída com êxito, será apresentada a mensagem **Resultado: ÊXITO** e haverá um novo ficheiro na pasta atual, que tem o seguinte nome: TransferPackage-*ContosoFirstkey*.byok

### Passo 4: copiar o pacote de transferência da chave para a estação de trabalho ligada à Internet
Utilize uma pen USB ou outro armazenamento portátil para copiar o ficheiro de saída do passo anterior (KeyTransferPackage-*ContosoFirstkey*.byok) para a estação de trabalho ligada à Internet.

> [!NOTE]
> Utilize as práticas de segurança para proteger o ficheiro, pois inclui a sua chave privada.

## Transferir a chave de inquilino para o Azure RMS
Na estação de trabalho ligada à Internet, siga estes 3 passos para transferir a nova chave de inquilino para o Azure RMS:

-   [Passo 1: ligar ao Azure RMS](#step-1-connect-to-azure-rms)

-   [Passo 2: carregar o pacote de chave](#step-2-upload-the-key-package)

-   [Passo 3: enumerar as chaves de inquilino – conforme necessário](#step-3-enumerate-your-tenant-keys-as-needed)

### Passo 1: ligar ao Azure RMS
Regresse à janela do Windows PowerShell e escreva o seguinte:

1.  Restabeleça ligação ao serviço [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]:

    ```
    Connect-AadrmService
    ```

2.  Utilize o cmdlet [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) para ver a configuração da chave de inquilino atual:

    ```
    Get-AadrmKeys
    ```

### Passo 2: carregar o pacote de chave
Utilize o cmdlet [Adicionar AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) para carregar o pacote de transferência da chave que copiou da estação de trabalho desligada:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> É-lhe pedido que confirme esta ação. É importante compreender que não é possível anular esta ação. Ao carregar uma chave de inquilino, torna-se automaticamente a chave de inquilino principal da sua organização e os utilizadores irão começar a utilizar esta chave de inquilino para proteger documentos e ficheiros.

Se o carregamento for bem-sucedido, verá a seguinte mensagem: **O serviço de gestão de direitos adicionou a chave com êxito.**

Existirá um atraso na replicação para que a alteração seja propagada a todos os centros de dados do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

### Passo 3: enumerar as chaves de inquilino – conforme necessário
Utilize o cmdlet Get-AadrmKeys novamente para ver a alteração na sua chave de inquilino e sempre que pretender ver uma lista das chaves de inquilino. As chaves de inquilino apresentadas incluem a chave de inquilino inicial que a Microsoft gerou para si e todas as chaves de inquilino que adicionou:

```
Get-AadrmKeys
```
A chave de inquilino que está marcada como **Ativa** é a que a sua organização está atualmente a utilizar para proteger documentos e ficheiros.

Agora que concluiu todos os passos necessários para levar a sua própria chave através da Internet, pode avançar para os passos seguintes para planear e implementar a sua chave de inquilino.


> [!div class="button"]
[Passos Seguintes >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Jun16_HO4-->


