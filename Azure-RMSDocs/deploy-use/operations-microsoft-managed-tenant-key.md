---
# required metadata

title: Gerenciado pela Microsoft - operações de ciclo de vida da chave de locatário | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Gerenciado pela Microsoft: operações de ciclo de vida da chave de locatário

*Aplica-se a: Azure Rights Management, Office 365*

Se a Microsoft gerencia sua chave de locatário para o Azure Rights Management (o padrão), use as seções a seguir para obter mais informações sobre as operações do ciclo de vida que são relevantes para esta topologia.

## Revogue sua chave de locatário
Ao cancelar a assinatura do Azure RMS, o Azure RMS para de usar sua chave de locatário e não precisa realizar nenhuma ação.

## Crie novamente sua chave de locatário
A Criação repetida de chaves também é conhecida como geração repetida de sua chave. Não crie novamente sua chave de locatário a menos que seja realmente necessário. Clientes antigos, tais como Office 2010, não foram projetados para manipular normalmente as alterações de chave. Neste cenário, você deve limpar o estado do RMS nos computadores usando uma Política de grupo ou um mecanismo equivalente. Entretanto, há alguns eventos legítimos que podem lhe forçar a criar novamente sua chave de locatário. Por exemplo:

-   Sua empresa se dividiu em duas ou mais empresas. Ao criar novamente sua chave de locatário, a nova empresa não terá acesso ao novo conteúdo que seus empregados publiquem. Eles podem acessar o conteúdo antigo se tiverem uma cópia da chave de locatário antiga.

-   Você acredita que a cópia mestre da sua chave de locatário (a cópia em sua posse) foi comprometida.

Você pode criar novamente sua chave de locatário chamando ao CSS (Serviços de Atendimento ao Cliente) da Microsoft e provando que você é o administrador de locatário.

Ao criar novamente sua chave de locatário, o novo conteúdo é protegido usando a nova chave de locatário. Isto acontece em uma maneira em fases, para que em um período de tempo, algum conteúdo novo continuará sendo protegido com a chave de locatário antiga. O conteúdo previamente protegido permanece protegido com sua chave de locatário antiga. Para oferecer suportes a este cenário, o Azure RMS retém sua chave de locatário antiga de modo que possa emitir licenças para conteúdo antigo.

## Faça backup e recupere sua chave de locatário
A Microsoft é responsável por fazer o backup da sua chave de locatário e nenhuma ação sua é requerida.

## Exportar sua chave de locatário
Você pode exportar sua configuração do Azure RMS e a chave do locatário seguindo as instruções nestas três etapas:

### Etapa 1: Iniciar exportação

-   Para fazer isso, contate o Serviço de Atendimento ao Cliente da Microsoft (CSS). Você deve provar que é um administrador para seu locatário do Azure RMS.

### Etapa 2: Espere a verificação

-   A Microsoft verifica se sua solicitação de liberação da chave de locatário do RMS é legítima. Esse processo pode levar até três semanas.

### Etapa 3: Receber instruções de chave do CSS

-   Os Serviços de Atendimento ao Cliente da Microsoft (CSS) lhe enviarão sua configuração do Azure RMS e a chave de locatário criptografada em um arquivo protegido por senha que tem a extensão de nome de arquivo .tpd. Para fazer isto, o CSS primeiro lhe envia (como a pessoa que inicia a exportação) uma ferramenta por e-mail. Você deve executar a ferramenta desde um prompt de comando da seguinte forma:

    ```
    AadrmTpd.exe -createkey
    ```
    Isso gera um par de chaves do RSA e salva as metades pública e privada como arquivos na pasta atual. Por exemplo: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** e **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Responda a este email do CSS, anexando o arquivo que tem um nome que começa com **PublicKey**. O CSS enviará um arquivo TPD como um arquivo .xml que é criptografado com sua chave RSA. Copie esse arquivo na mesma pasta em que você executou a ferramenta AadrmTpd originalmente e execute-a novamente, usando o arquivo que começa com **PrivateKey** e o arquivo de CSS. Por exemplo:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    A saída desse comando deve ser dois arquivos: um contém a senha em texto sem formatação para o TDP protegido por senha e o outro é o TPD protegido por senha próprio. Para propósitos de referências cruzadas, ambos devem ter o mesmo GUID que os arquivos de chave públicos e privados no momento em que você executou o comando AadrmTpd.exe -createkey:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Faça backup destes arquivos e armazene-os com segurança para garantir que você possa continuar descriptografando conteúdo protegido com esta chave de locatário. Além disso, se você estiver migrando para o AD RMS, poderá importar esse arquivo TPD (o arquivo que começa com **ExportedTDP**) para seu servidor do AD RMS.

### Etapa 4: Contínua: proteger sua chave de locatário

-   Após receber sua chave de locatário, guarde-a em local seguro, pois se alguém tiver acesso a ela será possível descriptografar todos os documentos protegidos usando essa chave.

    Caso queira exportar sua chave de locatário porque não deseja mais usar o Azure RMS, a prática recomendada é desativar seu locatário do RMS. Não demore para fazer isso após receber sua chave de locatário, pois isso o ajudará a minimizar as consequências se sua chave for acessada por alguém que não deveria ter acesso a ela. Para instruções, consulte [Descomissionando e desativando o Azure Rights Management](decommission-deactivate.md).

## Responder a uma violação
Nenhum sistema de segurança, sem importar o forte que seja, está completo sem um processo de resposta de violação. Sua chave de locatário pode estar comprometida ou roubada. Ainda quando estiver bem protegido, as vulnerabilidades podem ser encontradas na tecnologia HSM da geração atual ou em comprimentos e algoritmos da chave atual.

A Microsoft tem uma equipe dedicada para responder a incidentes de segurança nos seus produtos e serviços. Assim que houver um relatório confiável de um incidente, esta equipe se ocupa de investigar o escopo, a causa raiz e as atenuações. Se este incidente afeta seus ativos, então a Microsoft notificará seus administradores de locatário do Azure RMS por e-mail usando o endereço que você forneceu quando assinou.

Se você detectar uma violação, a melhor ação que você ou a Microsoft pode efetuar depende do escopo da violação; a Microsoft trabalhará com você ao longo deste processo. A seguinte tabela mostra algumas situações típicas e a resposta provável, embora a resposta exata dependerá de todas as informações que sejam reveladas durante a investigação.

|Descrição do incidente|Resposta provável|
|------------------------|-------------------|
|Sua chave de locatário vazou.|Crie novamente sua chave de locatário. Consulte a seção [Crie novamente sua chave de locatário](operations-tenant-key.md#re-key-your-tenant-key) nesse artigo.|
|Um indivíduo não autorizado ou malware obteve direitos para usar sua chave de locatário mas a chave em si não vazou.|Criar novamente sua chave de locatário não ajuda aqui e necessita um análises da causa raiz. Se um processo ou bug do software foi responsável para que o indivíduo não autorizado obtenha acesso, aquela situação deve ser resolvida.|
|Vulnerabilidade descoberta no algoritmo RSA, ou comprimento da chave, ou ataques de força bruta se tornam possíveis em termos computacionais.|A Microsoft deve atualizar o Azure RMS para oferecer suporte de novos algoritmos e comprimentos de chave maiores que sejam resilientes, e instruir a todos os usuários a renovar suas chaves de locatário.|




<!--HONumber=Apr16_HO4-->


