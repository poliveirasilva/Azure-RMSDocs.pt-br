---
title: "A política padrão do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 977cbf2f45cab75aaca9c2a16dd1564c2af2fe4a


---

# A política padrão do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Use as seguintes informações para entender como a política padrão do Azure Information Protection é configurada. Se você modificar a política padrão, poderá consultar estes valores para retornar a política aos padrões.

## Barra do Information Protection

Título: **Confidencialidade**

Dica de ferramenta: **a Confidencialidade de informações consiste em quatro níveis distintos (Público, Interno, Confidencial, Secreto), permitindo que o usuário identifique o risco de expor as informações a usuários não autorizados dentro ou fora da empresa.**


## Rótulos

Há cinco rótulos padrão com as seguintes configurações:

### **Pessoal**

Dica de ferramenta: **apenas para uso pessoal. Esses dados não serão monitorados pela organização. As informações pessoais não devem incluir nenhum dado relacionado à empresa.**

Cor: verde-claro

Marcações visuais: nenhuma

Condições: nenhuma

Proteção: nenhuma

----


### **Público**

Dica de ferramenta: **essas informações são internas e podem ser usadas por todos os usuários dentro ou fora da empresa.**

Cor: verde

Marcações visuais: nenhuma

Condições: nenhuma

Proteção: nenhuma

----

### **Interno**

Dica de ferramenta: **essas informações incluem uma ampla variedade de dados de negócios internos que podem ser usados por todos os funcionários e podem ser compartilhados com parceiros comerciais e clientes autorizados. Exemplos de informações internas são as políticas da empresa e a maioria das comunicações internas.**

Cor: azul

Marcações visuais: rodapé (documento e email)

Condições: nenhuma

Proteção: nenhuma

----

### **Confidencial**

Dica de ferramenta: **esses dados incluem informações confidenciais da empresa. Expor esses dados a usuários não autorizados pode prejudicar a organização. Exemplos de informações confidenciais são informações de funcionários, projetos ou contratos de clientes individuais e dados de contas de vendas.**

Cor: laranja

Marcações visuais: rodapé (documento e email)

Condições: nenhuma

Proteção: nenhuma

----

### **Segredo**

Dica de ferramenta: **esses dados incluem informações altamente confidenciais da empresa, que precisam ser protegidos. Expor dados secretos a usuários não autorizados pode prejudicar seriamente a organização. Exemplos de informações secretas são informações de identificação pessoal, registros de clientes, código-fonte e relatórios financeiros pré-anunciados.**

Cor: vermelha

Marcações visuais: rodapé (documento e email)

Condições: nenhuma

Proteção: nenhuma

----


## Sub-rótulos

Há dois sub-rótulos padrão com as seguintes configurações:

### Segredo > **Toda a empresa**

Dica de ferramenta: **esses dados incluem informações confidenciais da empresa, permitidas para todos os funcionários da empresa.**

Marcações visuais: nenhuma

Condições: nenhuma

Proteção: nenhuma

----

### Segredo > **Meu grupo**

Dica de ferramenta: **esses dados incluem informações confidenciais da empresa, permitidas apenas para grupos de funcionários.**

Marcações visuais: nenhuma

Condições: nenhuma

Proteção: nenhuma

## Configurações globais

**Todos os documentos e emails devem ter um rótulo (aplicado automaticamente ou por usuários)**: desativado

**Selecione o rótulo padrão**: nenhum

**Os usuários devem fornecer justificativa ao diminuir o nível de confidencialidade (por exemplo, de Confidencial para Público)**: desativado

## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização). 



<!--HONumber=Jul16_HO5-->


