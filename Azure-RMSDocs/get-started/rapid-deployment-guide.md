---
title: "Guia de implementação rápida para o Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c994d616-cff6-4930-9228-a7f7d198a160
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 01c2436218e0d7fd80a31cdc037d9dc8933e42f2


---

# Guia de implementação rápida para o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Utilize este guia, além das informações de configuração na secção **Implementar e Utilizar**, para o ajudar a implementar e utilizar mais rapidamente o Azure Rights Management (Azure RMS) ao selecionar a numa lista dos cenários específicos a implementar.

Estes cenários contêm as instruções do administrador e a documentação do utilizador final associada. Antes de dar a documentação (instruções ou anúncios) aos seus utilizadores finais, terá primeiro de personalizá-la para os seus requisitos empresariais e fluxos de trabalho existentes. Um conjunto de instruções de exemplo ou um anúncio mostram o possível aspeto da documentação do utilizador final.

Cada cenário tem uma lista dos requisitos com ligações para mais informações, se necessário, para que possa implementar estas soluções de forma independente e por qualquer ordem.

Os cenários aqui listados são uma amostra daqueles mais populares. Uma vez que o Azure RMS pode ser utilizado para proteger as informações num grande número de cenários numa organização e entre organizações, pode definir os seus próprios cenários e implementá-los para o seu ambiente e os seus utilizadores com este mesmo modelo. Ao concentrar-se em cenários específicos, a implementação do Azure RMS estará mais alinhada com os seus objetivos empresariais. Além disso, a nossa experiência é que os utilizadores tendem a seguir instruções de cenários específicos muito mais atentamente e sistematicamente do que as orientações gerais, tais como “proteger documentos confidenciais”.

Antes de implementar estas soluções, deve enviar um anúncio abrangente para os utilizadores finais, permitindo-lhes saber que algumas alterações serão feitas para ajudar a proteger os dados da empresa e que podem ser necessárias algumas alterações por parte desses indivíduos. Uma comunicação de exemplo está incluída depois da tabela seguinte.

> [!NOTE]
> Se tiver perguntas e comentários acerca deste guia, utilize os mecanismos de comentários nesta página ou envie uma mensagem de e-mail para [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback).

## Cenários para o Azure RMS
Para o ajudar a implementar mais rapidamente o Azure RMS para resolver problemas empresariais específicos, escolha os cenários que melhor correspondem aos seus objetivos empresariais e adapte-os sempre que necessário.



**Envie um ficheiro do Office por e-mail para utilizadores noutra organização com a capacidade para controlar os acessos resultantes (colaboração de empresa-empresa)**

Exemplos:

- Enviar uma lista de preços, informações gerais ou planos de lançamento para um cliente

- Enviar uma ordem de trabalho ou uma especificação de marketing a um fornecedor

- Enviar uma proposta ou pedido de orçamento (RFQ) a um parceiro

Consulte: [Cenário – partilhar um ficheiro do Office com os utilizadores noutra organização](scenario-share-office-file-externally.md)

**Certificar-se de que os documentos armazenados numa biblioteca do SharePoint permanecem no seu controlo**

Exemplos:

- Folhas de cálculo departamentais e relatórios

- Colaboração entre equipas para criar documentos ou outros materiais a entregar

Consulte: [Cenário – manter o controlo de documentos armazenados no SharePoint](scenario-sharepoint.md)

**Os executivos podem trocar informações privilegiadas em segurança por e-mail**

Exemplos:

- Partilhar planos de aquisição

- Debater ou divulgar problemas legais

- Informações sobre potenciais despedimentos ou outros assuntos confidenciais

Consulte: [Cenário – os executivos trocam informações privilegiadas em segurança](scenario-executives-email.md)

**Proteger automaticamente todos os ficheiros num servidor de ficheiros**

Exemplos:

- Documentos CAD que têm de ser mantidos internamente para impedir uma perda de propriedade intelectual

- As datas e os planos de promoção de marketing têm de ser mantidos em segredo para evitar a divulgação pública e para manter uma vantagem competitiva

Consulte: [Cenário – proteger ficheiros numa partilha de servidor de ficheiros](scenario-fci.md)

**Proteger cuidadosamente os seus documentos empresariais mais confidenciais e de elevado impacto**

Exemplos:

- Informações de receitas ou fórmulas que são exclusivas da sua empresa

- Planos de aquisições ou fusões altamente confidenciais

- Dados de exploração de recursos naturais

Consulte: [Cenário – proteger os seus ficheiros mais importantes](scenario-secure-most-valuable-files.md)

**Enviar anexos e e-mails da empresa confidenciais**

Exemplos:

- Declaração de visão da empresa

- Organogramas, notícias de reorganização ou anúncios de promoção

- Informações sobre a política da empresa

Consulte: [Cenário – enviar um e-mail confidencial da empresa](scenario-company-confidential-email.md)

**Aplicar proteção persistente a ficheiros do Office nas Pastas de Trabalho**

Exemplos:

- Documentos editados localmente do Word para um projeto confidencial da empresa

- Folhas de cálculo criadas localmente que contêm dados confidenciais ou dados de elevado impacto para a empresa

- Apresentações do PowerPoint em curso armazenadas localmente que não podem ser divulgadas ou acidentalmente partilhadas com pessoas fora da organização, até que as apresentações estejam concluídas

Consulte: [Cenário – configurar pastas de trabalho para proteção persistente](scenario-work-folders.md)




## Anúncio para utilizadores antes da implementação
Pode utilizar a seguinte mensagem de comunicação de exemplo para que os utilizadores saibam que implementar o Azure RMS significa que algumas alterações estão a caminho. Copie e cole o seguinte texto para ser enviado por e-mail para todos os utilizadores de alguém na equipa de liderança da sua organização, de preferência, o Diretor Executivo. Considere efetuar alterações a este texto para tornar a mensagem mais relevante para os utilizadores e a sua organização.

![Exemplo de faixa de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

### As alterações que estamos a efetuar para salvaguardar os nossos dados
Alguma vez quis bloquear o acesso a um documento enviado para os parceiros por engano? Já pensou se existe uma forma de saber qual dos seus clientes leu as notícias mais recentes do produto que enviou? Tem necessidade de partilhar informações confidenciais do produto sem preocupações de que poderão ser enviadas a pessoas que não as deveriam ver?

Em breve, poderá fazer tudo isto, porque o Departamento de TI está a implementar algumas alterações que implementam o Microsoft Azure Rights Management (Azure RMS) como uma solução de proteção de dados da empresa. Muitas destas soluções aplicarão automaticamente a proteção de que precisamos, sem precisar de fazer algo diferente. Algumas alterações podem exigir efetuar algo de forma diferente e, quando for este o caso, o Departamento de TI enviar-lhe-á informações e instruções, com o apoio do suporte técnico se tiver questões ou problemas.

Por exemplo, para controlar (e, se for necessário, revogar) os documentos que partilha, irá utilizar o site de controlo de documentos:

![Capturas de Ecrã do Controlo de Documentos do Azure RMS](../media/AzRMS_Tutorial_5_Screenshots.png)

Para uma antevisão de como isto funciona, veja este vídeo de 2 minutos: [Revogação e Controlo de Documentos do Azure RMS](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

Um dos recursos mais importantes desta organização são os seus dados — os dados que geramos, armazenamos e utilizamos numa base diária. Dá-nos a uma vantagem competitiva e ajuda-nos a ter êxito. É por esse motivo que é tão importante mantermos o controlo dos nossos dados e certificarmo-nos de que as pessoas que não devem aceder aos mesmos não o conseguem fazer.

As soluções que estamos a implementar ajudam-nos a proteger os nossos dados valiosos e dão-lhe as ferramentas necessárias para manter o controlo desses dados. Obrigado pela sua cooperação enquanto implementamos estas alterações.




<!--HONumber=Jun16_HO4-->


