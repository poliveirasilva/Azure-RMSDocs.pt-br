---
# required metadata

title: Gerar e transferir sua chave de locatário pessoalmente | Azure RMS
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

# Gerar e transferir sua chave de locatário pessoalmente

Utilize os procedimentos a seguir se decidiu [gerenciar sua própria chave de locatário](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) e não quiser transferi-la pela Internet, mas em vez disso, quiser transferir sua chave de locatário pessoalmente.

## Gerar sua chave de locatário
Para gerar sua chave de locatário, siga estas 3 etapas:

-   [Etapa 1: Prepare uma estação de trabalho com HSM da Thales](#step-1-prepare-a-workstation-with-thales-hsm)

-   [Etapa 2: Crie um mundo de segurança](#step-2-create-a-security-world)

-   [Etapa 3: Crie uma nova chave](#step-3-create-a-new-key)

### Etapa 1: Prepare uma estação de trabalho com HSM da Thales
Instale o software de suporte nCipher (Thales) em um computador com Windows. Anexe um HSM da Thales a esse computador. Certifique-se de que as ferramentas Thales estejam em seu caminho. Para obter mais informações, consulte o guia do usuário fornecido com o HSM da Thales ou visite o site da Thales para Azure RMS em [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Etapa 2: Crie um mundo de segurança
Inicie um prompt de comando e execute o programa do novo mundo Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa cria um arquivo **Security World** em %NFAST_KMDATA%\local\world, que corresponde à pasta C:\ProgramData\nCipher\Key Management Data\local. É possível usar valores diferentes para o quorum, mas no nosso exemplo, você será solicitado a digitar três cartões e pins em branco para cada um. Então, os dois cartões darão acesso completo ao mundo de segurança.  Esses cartões se tornam o **Conjunto de Cartões do Administrador** para o novo mundo de segurança.

Em seguida, faça o seguinte:

1.  Instale o provedor de Thales GNV como descrito na documentação da Thales e configure-o para usar o novo mundo de segurança.

2.  Faça backup do arquivo do mundo. Assegure e proteja o arquivo de mundo, os Cartões de administrador e seus pins, e certifique-se de que ninguém mais tenha acesso a mais de um cartão.

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
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Ao executar este comando, use estas instruções:

-   Substitua *contosokey* pelo mesmo valor especificado na Etapa 1.

-   Use a opção **-M** para que a chave seja adequada para esse cenário. Sem isso, a chave resultante será uma chave específica do usuário para o usuário atual.

Esse comando cria um arquivo de chave de token na pasta %NFAST_KMDATA%\local com um nome iniciado por **key_caping`_`** seguido de um SID. Por exemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este arquivo contém uma chave criptografada.

Faça backup deste arquivo de chave de token em um local seguro.

> [!IMPORTANT]
> Mais tarde, ao transferir sua chave para o Azure RMS, a Microsoft terá uma cópia não recuperável de sua chave. Isso significa que ninguém poderá recuperar sua chave dos HSMs na Microsoft. Isso permite que você mantenha o controle exclusivo sobre sua chave de locatário. Por isso, é extremamente importante que seja feito o backup de sua chave e do mundo da segurança de forma segura. Entre em contato com a Thales para obter orientações e as melhores práticas para fazer backup da sua chave.

Agora você está pronto para transferir a sua chave de locatário do Azure RMS.

## Transfira sua chave de locatário para o Azure RMS
Após gerar sua própria chave, será necessário transferi-la para o Azure RMS antes de usá-la. Para o mais alto nível de segurança, esta transferência é um processo manual que exige que você vá ao escritório da Microsoft em Redmond, em Washington, nos Estados Unidos. Para concluir esse processo, siga estas 3 etapas:

-   [Etapa 1: Traga sua chave para a Microsoft](#step-1-bring-your-key-to-microsoft)

-   [Etapa 2: transfira sua chave para o mundo de segurança do Azure RMS](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [Etapa 3: Procedimentos de encerramento](#step-3-closing-procedures)

### Etapa 1: Traga sua chave para a Microsoft

-   Entre em contato com os Serviços de Atendimento ao Cliente da Microsoft (CSS) para agendar uma consulta de transferência de chave para o Azure RMS. Traga o seguinte para a Microsoft em Redmond:

    -   O quórum de seus cartões administrativos. Se você seguiu as instruções anteriores em [Etapa 2: Criar um mundo de segurança](#step-2-create-a-security-world), esses são dois dos seus três cartões.

    -   Pessoal autorizado a levar seus cartões e pins administrativos, geralmente dois (um para cada cartão).

    -   Seu arquivo do Security World (%NFAST_KMDATA%\local\world) em uma unidade USB.

    -   Seu arquivo de chave de token em uma unidade USB.

### Etapa 2: transfira sua chave para o mundo de segurança do Azure RMS

1.  Ao chegar na Microsoft para transferir sua chave, acontece o seguinte:

    -   A Microsoft fornece uma estação de trabalho offline que tem um HSM da Thales anexo, um software Thales instalado e um arquivo Azure RMS World Security pré-carregado na pasta C:\Temp\Destination.

    -   Nessa estação de trabalho, você carrega seu arquivo do Security World e o arquivo de chave de token da sua unidade USB para a pasta C:\Temp\Source.

    -   Os operadores do Azure RMS transferem de forma segura sua chave para o mundo da segurança do Azure RMS com utilitários Thales.

    Este processo será semelhante ao seguinte, onde o último parâmetro de key-xfer-im, neste exemplo, é substituído pelo nome do seu arquivo de chave de token:

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  O Mk-reprogram pedirá a você e aos operadores do Azure RMS que conectem seus respectivos cartões de administrador e pins. Isso comanda a saída de um arquivo de chave de símbolo no C:\Temp\Destination que contém sua chave protegida pelo mundo de segurança Azure RMS.

### Etapa 3: Procedimentos de encerramento

-   Em sua presença, os operadores do Azure RMS fazem o seguinte:

    -   Executam uma ferramenta que a Microsoft desenvolveu em colaboração com a Thales que remove duas permissões: A permissão para recuperar a chave e a permissão para alterar as permissões. Após ter feito isso, esta cópia de sua chave será bloqueada para o mundo de segurança do Azure RMS. Os HSMs da Thales não permitirão que os operadores do Azure RMS com seus cartões de administrador recuperem a cópia de texto sem formatação de sua chave.

    -   Copie o arquivo de chave resultante para uma unidade USB para posteriormente fazer upload para o serviço do Azure RMS.

    -   Redefina o HSM para as configurações de fábrica e limpe a estação de trabalho.

Agora você concluiu as instruções necessárias para trazer sua própria chave pessoalmente e pode voltar para sua organização para as próximas etapas do planejamento e implementação da sua chave de locatário.

> [!div class="button"]
[Próximas etapas >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Apr16_HO3-->


