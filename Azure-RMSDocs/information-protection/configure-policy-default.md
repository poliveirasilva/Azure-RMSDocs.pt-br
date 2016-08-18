---
title: "A política padrão do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 0e02a3f78f1c5986d61f73e57265b944e9d03552
ms.openlocfilehash: 4abce96c4e1215f92211a231a187bd2de4ad3845


---

# A política padrão do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Use as seguintes informações para entender como a política padrão do Azure Information Protection é configurada. Se você modificar a política padrão, poderá consultar estes valores para retornar a política aos padrões.

## Barra do Information Protection

|Setting|Valor|
|-------------------------------|---------------------------|
|Título|Sensibilidade|
|Dica de ferramenta|A Confidencialidade de Informações consiste em quatro níveis distintos (Público, Interno, Confidencial e Secreto), permitindo que o usuário identifique o risco de expor as informações a usuários não autorizados dentro ou fora da empresa.|

## Rótulos

|Rótulo|Dica de ferramenta|Configurações|
|-------------------------------|---------------------------|-----------------|
|Pessoal|Apenas para uso pessoal. Esses dados não serão monitorados pela organização. As informações pessoais não devem incluir dados relacionados à empresa.|**Habilitado**: sim <br /><br />**Cor**: verde-claro<br /><br />**Marcações visuais**: nenhuma <br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|
|Público|Essas informações são internas e podem ser usadas por todas as pessoas dentro ou fora da empresa.|**Habilitado**: sim <br /><br />**Cor**: verde<br /><br />**Marcações visuais**: nenhuma<br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|
|Interno|Essas informações incluem uma ampla variedade de dados corporativos internos que podem ser usados por todos os funcionários e compartilhados com parceiros de negócios e clientes autorizados. Exemplos de informações internas são as políticas da empresa e a maioria das comunicações internas.|**Habilitado**: sim <br /><br />**Cor**: azul <br /><br />**Marcações visuais**: rodapé (documento e email)<br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|
|Confidencial|Esses dados incluem informações comerciais confidenciais. Expor esses dados a usuários não autorizados pode prejudicar a organização. Exemplos de informações Confidenciais são informações de funcionários, projetos ou contratos de clientes individuais e dados de contas de vendas.|**Habilitado**: sim <br /><br />**Cor**: laranja<br /><br />**Marcações visuais**: rodapé (documento e email)<br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|
|Segredo|Esses dados incluem informações altamente confidenciais da empresa que precisam ser protegidas. Expor dados secretos a usuários não autorizados pode prejudicar seriamente a organização. Exemplos de informações Secretas são informações de identificação pessoal, registros de clientes, código-fonte e relatórios financeiros pré-anunciados.|**Habilitado**: sim <br /><br />**Cor**: vermelho<br /><br />**Marcações visuais**: rodapé (documento e email)<br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|

## Sub-rótulos

|Rótulo|Dica de ferramenta|Configurações|
|-------------------------------|---------------------------|-----------------|
|*Segredo* > Toda a Empresa|Esses dados incluem informações comerciais confidenciais – permitidas para todos os funcionários da empresa.|**Habilitado**: sim <br /><br />**Marcações visuais**: nenhuma<br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|
|*Segredo* > Meu Grupo|Esses dados incluem informações comerciais confidenciais – permitidas apenas para grupos de funcionários.|**Habilitado**: sim <br /><br />**Marcações visuais**: nenhuma<br /><br />**Condições**: nenhuma<br /><br />**Proteção**: não|

## Configurações globais

|Setting|Valor|
|-------------------------------|---------------------------|
|Todos os documentos e emails devem ter um rótulo (aplicado automaticamente ou por usuários)|Desativado|
|Selecionar o rótulo padrão|Nenhum|
|Os usuários devem fornecer uma justificativa ao diminuir o nível de confidencialidade (por exemplo, de Confidencial para Público)|Desativado|


## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização). 



<!--HONumber=Aug16_HO2-->


