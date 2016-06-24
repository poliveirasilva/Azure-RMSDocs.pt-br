---
# required metadata

title: Gerenciado pelo cliente - operações de ciclo de vida da chave de locatário | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Gerenciado pelo cliente: operações de ciclo de vida da chave de locatário

*Aplica-se a: Azure Rights Management, Office 365*

Se você gerencia sua chave de locatário para o Azure Rights Management (traga sua própria chave, ou BYOK), use as seções a seguir para obter mais informações sobre as operações do ciclo de vida que são relevantes para esta topologia.

## Revogue sua chave de locatário
Ao cancelar a assinatura do Azure RMS, o Azure RMS para de usar sua chave de locatário e não precisa realizar nenhuma ação.

## Crie novamente sua chave de locatário
A Criação repetida de chaves também é conhecida como geração repetida de sua chave. Não crie novamente sua chave de locatário a menos que seja realmente necessário. Clientes antigos, tais como Office 2010, não foram projetados para manipular normalmente as alterações de chave. Neste cenário, você deve limpar o estado do RMS nos computadores usando uma Política de grupo ou um mecanismo equivalente. Entretanto, há alguns eventos legítimos que podem lhe forçar a criar novamente sua chave de locatário. Por exemplo:

-   Sua empresa se dividiu em duas ou mais empresas. Ao criar novamente sua chave de locatário, a nova empresa não terá acesso ao novo conteúdo que seus empregados publiquem. Eles podem acessar o conteúdo antigo se tiverem uma cópia da chave de locatário antiga.

-   Você acredita que a cópia mestre da sua chave de locatário (a cópia em sua posse) foi comprometida.

Ao criar novamente sua chave de locatário, o novo conteúdo é protegido usando a nova chave de locatário. Isto acontece em uma maneira em fases, para que em um período de tempo, algum conteúdo novo continuará sendo protegido com a chave de locatário antiga. O conteúdo previamente protegido permanece protegido com sua chave de locatário antiga. Para oferecer suportes a este cenário, o Azure RMS retém sua chave de locatário antiga de modo que possa emitir licenças para conteúdo antigo.

Para criar novamente sua chave de locatário e criar uma nova chave na Internet ou pessoalmente, use os procedimentos na seção [Implementando sua própria chave (BYOK)](..\plan-design\plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) do tópico [Planejamento e implementação sua chave de locatário do Azure Rights Management](..\plan-design\plan-implement-tenant-key.md).

## Faça backup e recupere sua chave de locatário
Você é responsável por fazer o backup da sua chave de locatário. Se você gerou sua chave de locatário em um Thales HSM, para fazer o backup da chave, simplesmente faça o backup do arquivo de Chave de token, o arquivo World e os Cartões de administrador.

Se você transferiu sua chave seguindo os procedimentos da seção [Implementando o BYOK (traga sua própria chave)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) do artigo [Planejamento e implementação da sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md), o Azure RMS persistirá o arquivo de chave indexado para proteger contra a falha de todos os nós do Azure RMS. No entanto, não considere isto como um backup completo. Por exemplo, se você alguma vez precisar uma cópia em texto não formatado da sua chave para usar fora de um Thales HSM, o Azure RMS não será capaz de recuperá-la para você porque somente tem uma cópia não recuperável.

## Exportar sua chave de locatário
Se você usa o BYOK, você não pode exportar sua chave de locatário do Azure RMS. A cópia no Azure RMS não é recuperável. Se desejar excluir essa chave para que ela não possa mais ser usada, entre em contato com o suporte de serviço de cliente da Microsoft (CSS).

## Responder a uma violação
Nenhum sistema de segurança, sem importar o forte que seja, está completo sem um processo de resposta de violação. Sua chave de locatário pode estar comprometida ou roubada. Ainda quando estiver bem protegido, as vulnerabilidades podem ser encontradas na tecnologia HSM da geração atual ou em comprimentos e algoritmos da chave atual.

A Microsoft tem uma equipe dedicada para responder a incidentes de segurança nos seus produtos e serviços. Assim que houver um relatório confiável de um incidente, esta equipe se ocupa de investigar o escopo, a causa raiz e as atenuações. Se este incidente afeta seus ativos, então a Microsoft notificará seus administradores de locatário do Azure RMS por e-mail usando o endereço que você forneceu quando assinou.

Se você tem uma violação, a melhor ação que você ou a Microsoft podem tomar depende do escopo da violação; a Microsoft trabalhará com você ao longo deste processo. A seguinte tabela mostra algumas situações típicas e a resposta provável, embora a resposta exata dependerá de todas as informações que sejam reveladas durante a investigação.

|Descrição do incidente|Resposta provável|
|------------------------|-------------------|
|Sua chave de locatário vazou.|Crie novamente sua chave de locatário. Consulte [Criar novamente sua chave de locatário](#re-key-your-tenant-key).|
|Um indivíduo não autorizado ou malware obteve direitos para usar sua chave de locatário mas a chave em si não vazou.|Criar novamente sua chave de locatário não ajuda aqui e necessita um análises da causa raiz. Se um processo ou bug do software foi responsável para que o indivíduo não autorizado obtenha acesso, aquela situação deve ser resolvida.|
|A vulnerabilidade descoberta na tecnologia HSM da geração atual.|A Microsoft deve atualizar os HSMs. Se há um motivo para acreditar que a vulnerabilidade expus as chaves, então a Microsoft instruirá a todos os clientes para renovar suas chaves de locatário.|
|Vulnerabilidade descoberta no algoritmo RSA, ou comprimento da chave, ou ataques de força bruta se tornam possíveis em termos computacionais.|A Microsoft deve atualizar o Azure RMS para oferecer suporte de novos algoritmos e comprimentos de chave maiores que sejam resilientes, e instruir a todos os usuários a renovar suas chaves de locatário.|




<!--HONumber=Apr16_HO4-->


