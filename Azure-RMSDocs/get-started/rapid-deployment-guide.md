---
# required metadata

title: Guia de implantação rápida do Azure Rights Management | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guia de implantação rápida do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use este guia junto com as informações de configuração na seção **Implantar e usar** para obter ajuda com uma implantação e uso mais ágil do Azure RMS (Azure Rights Management) escolhendo em uma lista de cenários específicos de implementação.

Esses cenários contêm as instruções do administrador e a documentação de acompanhamento para o usuário final. Antes de fornecer a documentação (instruções ou anúncios) para os usuários finais, você precisará personalizá-la de acordo com suas necessidades de negócio e fluxos de trabalho existentes. Um exemplo de conjunto de instruções ou um aviso mostra a aparência final da documentação para o usuário final.

Cada cenário tem uma lista de requisitos com links para obter mais informações, se necessário, para que você pode implantar essas soluções de forma independente e em qualquer ordem.

Os cenários listados aqui são um exemplo dos mais populares. Como o Azure RMS pode ser usado para proteger as informações em uma grande quantidade de cenários, tanto dentro de uma organização quanto entre organizações, você pode definir seus próprios cenários e implantá-los em seu ambiente e para seus usuários usando esse mesmo modelo. Ao concentrar-se em cenários específicos, sua implantação do Azure RMS ficará mais alinhada aos objetivos comerciais. Além disso, nossa experiência diz que os usuários tendem a seguir instruções específicas ao cenário de forma mais rígida e sistemática do que uma orientação geral, por exemplo, "proteger documentos confidenciais".

Antes de implementar essas soluções, convém enviar um anúncio amplo aos usuários finais, avisando sobre algumas alterações que serão feitas para ajudar a proteger os dados da empresa, e que isso pode exigir algumas alterações da parte deles. Veja um exemplo de comunicação logo após a tabela a seguir.

> [!NOTE] Se você tiver dúvidas e comentários sobre este guia, use os mecanismos de comentários nesta página ou envie uma mensagem de email para [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback).

## Cenários para o Azure RMS
Para ajudar você a implantar o Azure RMS mais rapidamente a fim de resolver problemas comerciais específicos, escolha os cenários mais próximos de suas metas comerciais e adapte-os quando for necessário.



**Envie um arquivo do Office por email com segurança para usuários em outra organização, com a capacidade de acompanhar os acessos resultantes (colaboração entre empresas).**

Exemplos:

- Enviar uma lista de preços, roteiro ou planos de lançamentos a um cliente

- Enviar um pedido de trabalho ou a especificação de marketing para um fornecedor

- Enviar uma proposta ou solicitação de cotação (RFQ) a um parceiro.

Consulte: [Cenário - Compartilhar um arquivo do Office com usuários em outra organização](scenario-share-office-file-externally.md)

**Verifique se os documentos armazenados na biblioteca do SharePoint permanecem sob seu controle**

Exemplos:

- Relatórios e planilhas departamentais

- Colaboração entre equipes para documentos de design ou outros produtos.

Consulte: [Cenário - Mantenha o controle dos documentos armazenados no SharePoint](scenario-sharepoint.md)

**Os executivos podem trocar informações privilegiadas com segurança por email**

Exemplos:

- Compartilhamento de planos de aquisição

- Discussão ou disseminação de questões legais

- Informações sobre possíveis demissões ou outros assuntos sensíveis

Consulte: [Cenário - Executivos trocam informações privilegiadas de maneira segura](scenario-executives-email.md)

**Proteja automaticamente todos os arquivos em um servidor de arquivos**

Exemplos:

- Documentos de CAD que devem ser mantidos internamente para evitar a perda de propriedade intelectual

- Planos de promoção de marketing e datas que devem ser mantidos em segredo, sem divulgação pública, a fim de manter uma vantagem competitiva

Consulte: [Cenário - Proteger arquivos em um compartilhamento de servidor de arquivos](scenario-fci.md)

**Proteja de forma rígida seus documentos de alto impacto comercial e mais confidenciais**

Exemplos:

- Informações de receitas ou fórmulas exclusivas de sua empresa

- Planos de controle ou fusão altamente confidenciais

- Dados de exploração de recursos naturais

Consulte: [Cenário - Proteger seus &#40;poucos&#41; arquivos mais valiosos](scenario-secure-most-valuable-files.md)

**Envie com segurança anexos e emails confidenciais da empresa**

Exemplos:

- Declaração de visão da empresa

- Organogramas, notícias de reorganização ou anúncios de promoção

- Informações sobre políticas da empresa

Consulte: [Cenário - Enviar um email confidencial da empresa](scenario-company-confidential-email.md)

**Aplique proteção persistente para arquivos do Office em pastas de trabalho**

Exemplos:

- Documentos do Word editados localmente para um projeto confidencial da empresa

- Planilhas criadas localmente contendo dados confidenciais ou dados de alto impacto comercial

- Apresentações do PowerPoint ainda em produção e armazenadas localmente que não devem ser vazadas ou compartilhadas acidentalmente com pessoas fora da organização, até que as apresentações sejam concluídas

Consulte: [Cenário - Configurar pastas de trabalho para proteção persistente](scenario-work-folders.md)




## Anúncio para os usuários antes da implementação
Você pode usar o seguinte exemplo de mensagem de comunicação para avisar os usuários de que a implantação do Azure RMS exigirá algumas mudanças. Copie e cole o seguinte texto, que será enviado por email para todos os usuários por alguém da equipe de liderança de sua organização, preferencialmente pelo diretor executivo. Considere a possibilidade de fazer alterações no texto que tornem a mensagem mais relevante para os usuários e para sua organização.

![Faixa de documentação de usuário de exemplo para implantação rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

### Mudanças que estamos fazendo para proteger nossos dados
Você já quis bloquear o acesso àquele documento enviado por engano para seus parceiros? Você já pensou se há uma maneira de saber quais clientes leram as notícias mais recentes sobre o produto enviadas por você? Você tem a necessidade de compartilhar informações confidenciais sobre o produto sem a preocupação de que elas podem ser enviadas a pessoas que não deveriam vê-las?

Você poderá fazer essas coisas em breve, pois o departamento de TI está implantando algumas alterações que implementam o Azure RMS (Microsoft Azure Rights Management) como uma solução de proteção de dados corporativos. Muitas dessas soluções aplicarão automaticamente a proteção necessária, sem precisar fazer algo diferente. Porém, algumas mudanças podem exigir que você faça algumas coisas de forma diferente e, quando esse for o caso, o departamento de TI enviará informações e instruções, com o apoio do suporte técnico se você tiver dúvidas ou problemas.

Por exemplo, para rastrear (e, se necessário, revogar) os documentos compartilhados, você usará o site de rastreamento de documentos:

![Capturas de tela de acompanhamento de documento do Azure RMS](../media/AzRMS_Tutorial_5_Screenshots.png)

Para obter uma prévia de como isso funciona, confira este vídeo de dois minutos: [Azure RMS Document Tracking and Revocation](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)(Rastreamento e revogação de documento do Azure RMS)

Um dos ativos mais valiosos da organização são os dados; os dados que geramos, armazenamos e usamos diariamente. Eles nos proporcionam nossa vantagem competitiva e nos ajudam a ter sucesso. É por isso que é tão importante permanecer no controle de nossos dados e garantir que as pessoas que não devem acessá-los, não o façam.

As soluções que estamos implementando nos ajudarão a proteger nossos dados valiosos e fornecerão as ferramentas para manter o controle dos dados. Obrigado por sua cooperação durante a implementação dessas alterações.



<!--HONumber=May16_HO2-->


