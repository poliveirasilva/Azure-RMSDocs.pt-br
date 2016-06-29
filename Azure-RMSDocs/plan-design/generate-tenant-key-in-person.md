---
# required metadata

title: Gerar e transferir a chave de inquilino – pessoalmente | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Gerar e transferir a chave de inquilino – pessoalmente

*Aplica-se a: Azure Rights Management, Office 365*


Utilize os procedimentos seguintes se decidiu [gerir a sua própria chave de inquilino](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) e não a pretende transferir através da Internet, mas pretende transferir a chave de inquilino pessoalmente.

## Gerar a chave de inquilino
Para gerar a sua própria chave de inquilino, siga estes 3 passos:

-   [Passo 1: preparar uma estação de trabalho com o HSM da Thales](#step-1-prepare-a-workstation-with-thales-hsm)

-   [Passo 2: criar um universo de segurança](#step-2-create-a-security-world)

-   [Passo 3: criar uma nova chave](#step-3-create-a-new-key)

### Passo 1: preparar uma estação de trabalho com o HSM da Thales
Instale o software de suporte nCipher (Thales) num computador Windows. Anexe um HSM da Thales a esse computador. Certifique-se de que as ferramentas da Thales estão no seu caminho. Para mais informações, consulte o guia de utilizador incluído no HSM da Thales ou visite o Web site da Thales para o Azure RMS em [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Passo 2: criar um universo de segurança
Inicie uma linha de comandos e execute o programa de novo universo da Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa cria um ficheiro **Universo de Segurança** em %NFAST_KMDATA%\local\world, que corresponde à pasta C:\ProgramData\nCipher\Key Management Data\local. Pode utilizar valores diferentes para o quórum, mas no nosso exemplo, é-lhe pedido que introduza três cartões em branco e PINs para cada um deles. Em seguida, pode usar dois dos cartões e obterá acesso total ao universo de segurança.  Estes cartões tornam-se o **Conjunto de Cartões do Administrador** para o novo universo de segurança.

Depois, efetue o seguinte:

1.  Instale o fornecedor CNG da Thales conforme descrito na documentação da Thales e configure-o para utilizar o novo universo de segurança.

2.  Efetue uma cópia de segurança do ficheiro do universo. Proteja o ficheiro do universo, os Cartões de Administrador e os respetivos PINs e certifique-se de que nenhuma pessoa tem acesso a mais do que um cartão.

Agora, está pronto para criar uma nova chave que será a sua chave de inquilino do RMS.

### Passo 3: criar uma nova chave
Gere uma chave CNG utilizando os programas **generatekey** e **cngimport** da Thales.

Execute o seguinte comando para criar a chave:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Quando executar este comando, utilize estas instruções:

-   O parâmetro **protect** tem de ser definido para o valor **module**, conforme mostrado. Esta ação cria uma chave protegida por um módulo. O conjunto de ferramentas BYOK não suporta chaves protegidas por OCS.

-   Para o tamanho da chave, recomendamos chaves RSA de 2048 bits, mas também suportamos chaves de 1024 bits para clientes de AD RMS existentes que tenham essas chaves e estejam a migrar para o Azure RMS.

-   Substitua o valor de *contosokey* por **ident** e **plainname** por qualquer valor da cadeia. Para minimizar as sobrecargas administrativas e reduzir o risco de erros, recomendamos que utilize o mesmo valor para ambos e utilize todos os carateres minúsculos.

-   O pubexp fica em branco (predefinição) neste exemplo, mas pode especificar valores específicos. Para obter mais informações, consulte a documentação da Thales.

Em seguida, execute o seguinte comando para importar a chave para a CNG:

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Quando executar este comando, utilize estas instruções:

-   Substitua *contosokey* pelo mesmo valor que especificou no Passo 1.

-   Utilize a opção **-M** para que a chave seja adequada para este cenário. Sem esta ação, a chave resultante será uma chave específica para o utilizador atual.

Este comando cria um ficheiro de Chave com Token na pasta %NFAST_KMDATA%\local com um nome começado por **key_caping`_`** seguido de um SID. Por exemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este ficheiro contém uma chave encriptada.

Efetue uma cópia de segurança deste Ficheiro de Chave com Token numa localização segura.

> [!IMPORTANT]
> Ao transferir a chave para o Azure RMS mais tarde, a Microsoft terá uma cópia não recuperável da sua chave. Isto significa que ninguém pode obter a sua chave dos HSMs na Microsoft. Isto permite-lhe manter um controlo exclusivo sobre a sua chave de inquilino. Como tal, torna-se muito importante que efetue uma cópia de segurança da chave e do universo de segurança. Contacte a Thales para obter orientações e as melhores práticas para efetuar a cópia de segurança da sua chave.

Agora, está pronto para transferir a chave de inquilino para o Azure RMS.

## Transferir a chave de inquilino para o Azure RMS
Depois de ter gerado a sua própria chave, tem de a transferir para o Azure RMS antes de a utilizar. Para o nível mais elevado de segurança, esta transferência é um processo manual que requer que viaje até ao escritório da Microsoft em Redmond, Washington, nos EUA. Para concluir este processo, siga estes 3 passos:

-   [Passo 1: levar a chave até à Microsoft](#step-1-bring-your-key-to-microsoft)

-   [Passo 2: transferir a chave para o universo de segurança do Azure RMS](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [Passo 3: procedimentos de encerramento](#step-3-closing-procedures)

### Passo 1: levar a chave até à Microsoft

-   Contacte o Suporte ao Cliente da Microsoft (CSS) para agendar uma sessão de transferência da chave para o Azure RMS. Leve o seguinte para a Microsoft em Redmond:

    -   Um quórum dos seus Cartões Administrativos. Se seguiu as instruções anteriores no [Passo 2: criar um universo de segurança](#step-2-create-a-security-world), estes são dois dos seus três cartões.

    -   Pessoal autorizado a transportar os seus Cartões Administrativos e PINs, normalmente, dois (um para cada cartão).

    -   O ficheiro de Universo de Segurança (%NFAST_KMDATA%\local\world) numa unidade USB.

    -   O ficheiro de Chave com Token numa unidade USB.

### Passo 2: transferir a chave para o universo de segurança do Azure RMS

1.  Quando chegar à Microsoft para transferir a chave, ocorrerá o seguinte:

    -   A Microsoft fornece-lhe uma estação de trabalho offline com um HSM da Thales anexado, o software da Thales instalado e um ficheiro de Universo de Segurança do Azure RMS previamente carregado na pasta C:\Temp\Destination.

    -   Nesta estação de trabalho, carregue o ficheiro de Universo de Segurança e o Ficheiro de Chave com Token da sua unidade USB para a pasta C:\Temp\Source.

    -   Os operadores do Azure RMS transferem em segurança a chave para o universo de segurança do Azure RMS utilizando utilitários da Thales.

    Este processo será semelhante ao seguinte, em que o último parâmetro de key-xfer-im neste exemplo é substituído pelo nome do Ficheiro de Chave com Token:

    **C:\&gt; mk-reprogram.exe – proprietário c:\Temp\Destination adicione c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination – módulo c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  O mk-reprogram pede-lhe a si e aos operadores do Azure RMS para ligarem os respetivos Cartões de administrador e PINs. Estes comandos geram um Ficheiro de Chave com Token em C:\Temp\Destination que contém a sua chave protegida pelo universo de segurança do Azure RMS.

### Passo 3: procedimentos de encerramento

-   Na sua presença, os operadores do Azure RMS efetuam o seguinte:

    -   Executam uma ferramenta desenvolvida pela Microsoft em colaboração com a Thales que remove duas permissões: a permissão para recuperar a chave e a permissão para alterar as permissões. Depois de concluída a ação, esta cópia da sua chave fica bloqueada para o universo de segurança do Azure RMS. Os HSMs da Thales não irão permitir que os operadores do Azure RMs com os respetivos Cartões de administrador recuperem a cópia de texto simples da sua chave.

    -   Copie o ficheiro da chave resultante para uma unidade USB para mais tarde carregar para o serviço do Azure RMS.

    -   Efetue uma reposição de fábrica no HSM e apague a estação de trabalho.

Concluiu as instruções necessárias para levar a sua chave pessoalmente e pode regressar à sua organização para obter os passos seguintes para o planeamento e a implementação da sua chave de inquilino.

> [!div class="botão"]
[Passos Seguintes >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Apr16_HO4-->


