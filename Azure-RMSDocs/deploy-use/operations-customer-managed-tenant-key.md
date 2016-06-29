---
# required metadata

title: Operações de ciclo de vida das chaves de inquilino – geridas pelo cliente | Azure RMS
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


# Operações de ciclo de vida das chaves de inquilino: geridas pelo cliente

*Aplica-se a: Azure Rights Management, Office 365*

Se gerir a sua chave de inquilino para o Azure Rights Management (o cenário traga a sua própria chave ou BYOK), utilize as secções seguintes para obter mais informações sobre as operações de ciclo de vida que são relevantes para esta topologia.

## Revogar a chave de inquilino
Quando anular a subscrição do Azure RMS, o Azure RMS deixa de utilizar a chave de inquilino e não é necessária qualquer ação por parte do utilizador.

## Efetuar o rechaveamento da chave de inquilino
O rechaveamento também é conhecido como implementar a chave. Não efetue o rechaveamento da chave de inquilino, a menos que seja realmente necessário. Os clientes antigos, tal como o Office 2010, não foram concebidos para processar alterações de chave corretamente. Neste cenário, tem de limpar o estado do RMS nos computadores utilizando a Política de Grupo ou um mecanismo equivalente. No entanto, existem alguns eventos legítimos que poderão forçá-lo a efetuar o rechaveamento da chave de inquilino. Por exemplo:

-   A sua empresa foi dividida em duas ou mais empresas. Quando efetua o rechaveamento da chave de inquilino, a nova empresa não terá acesso ao conteúdo novo que os seus funcionários publicam. Estes podem aceder ao conteúdo antigo se tiverem uma cópia da chave de inquilino antiga.

-   Considera que a cópia principal da sua chave de inquilino (a cópia na sua posse) foi comprometida.

Quando efetua o rechaveamento da chave de inquilino, o novo conteúdo é protegido através da utilização da nova chave de inquilino. Isto acontece de forma faseada, pelo que, durante um período de tempo, algum conteúdo novo irá continuar a ser protegido com a chave de inquilino antiga. O conteúdo previamente protegido permanece protegido para a sua chave de inquilino antiga. Para suportar este cenário, o Azure RMS retém a chave de inquilino antiga para poder emitir licenças para o conteúdo antigo.

Para efetuar o rechaveamento da chave de inquilino, gere e crie uma nova chave através da Internet ou pessoalmente, utilizando os procedimentos na secção [Implementar BYOK (traga a sua própria chave)](..\plan-design\plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) do tópico [Planear e Implementar a Chave de Inquilino do Azure Rights Management](..\plan-design\plan-implement-tenant-key.md).

## Efetuar cópia de segurança e recuperar a chave de inquilino
É responsável pela cópia de segurança da sua chave de inquilino. Se gerou a chave de inquilino num HSM da Thales, para efetuar a cópia de segurança da chave, basta efetuar uma cópia de segurança do Ficheiro de Chave com Token, do ficheiro de Universo e dos Cartões de Administrador.

Se transferiu a chave ao seguir os procedimentos na secção [Implementar BYOK (traga a sua própria chave)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) do artigo [Planear e implementar a chave de inquilino do Azure Rights Management](../plan-design/plan-implement-tenant-key.md), o Azure RMS irá manter o Ficheiro de Chave com Token, para proteção contra falhas de quaisquer nós do Azure RMS. No entanto, não considere que esta seja uma cópia de segurança completa. Por exemplo, se alguma vez precisar de uma cópia de texto simples da sua chave para utilizar fora de um HSM da Thales, o Azure RMS não conseguirá recuperá-la porque apenas tem uma cópia não recuperável.

## Exportar a chave de inquilino
Se utilizar o BYOK, não é possível exportar a chave de inquilino do Azure RMS. A cópia no Azure RMS não é recuperável. Se pretender eliminar esta chave para deixar de poder ser utilizada, contacte o Suporte ao Cliente da Microsoft (CSS).

## Responder a uma violação
Nenhum sistema de segurança, por mais forte que seja, está completo sem um processo de resposta a violações. A sua chave de inquilino pode estar comprometida ou ter sido roubada. Mesmo quando está bem protegida, podem existir vulnerabilidades na tecnologia HSM da geração atual ou nos algoritmos e comprimentos de chaves atuais.

A Microsoft tem uma equipa dedicada para responder a incidentes de segurança nos seus produtos e serviços. Assim que existir um relatório credível de um incidente, esta equipa investiga o âmbito, a causa raiz e as resoluções. Se este incidente afetar os recursos, a Microsoft irá notificar os administradores de inquilinos do Azure RMS por e-mail utilizando o endereço que especificou aquando da subscrição.

Se ocorrer uma violação, a melhor ação que o utilizador ou a Microsoft pode efetuar depende do âmbito da violação; a Microsoft irá trabalhar consigo ao longo deste processo. A tabela seguinte mostra algumas situações típicas e a resposta provável, embora a resposta exata dependa de todas as informações que são reveladas durante a investigação.

|Descrição do incidente|Resposta provável|
|------------------------|-------------------|
|Ocorreu uma fuga da chave de inquilino.|Efetue o rechaveamento da chave de inquilino. Consulte [Efetuar o rechaveamento da chave de inquilino](#re-key-your-tenant-key).|
|Um indivíduo não autorizado ou um software maligno obteve direitos para utilizar a sua chave de inquilino, mas não houve uma fuga da própria chave.|Efetuar o rechaveamento da chave de inquilino não ajuda neste caso e requer a análise da causa raiz. Se um erro no processo ou software tiver sido responsável pelo acesso que o indivíduo não autorizado obteve, essa situação tem de ser resolvida.|
|Vulnerabilidade detetada na tecnologia HSM de geração atual.|A Microsoft tem de atualizar os HSMs. Se existir razão para considerar que a vulnerabilidade expôs chaves, a Microsoft instruirá todos os clientes a renovarem as respetivas chaves de inquilino.|
|Foi detetada uma vulnerabilidade no algoritmo RSA, ou no comprimento da chave, ou ataques de força bruta tornaram-se exequíveis a nível informático.|A Microsoft tem de atualizar o Azure RMS para suportar os novos algoritmos e maiores comprimentos de chaves para serem resilientes e instruir todos os clientes a renovarem as respetivas chaves de inquilino.|




<!--HONumber=Apr16_HO4-->


