---
title: "Configuração dos direitos de uso do Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 60f25cdcdabbfbb61072a95e39f84fed79cad871
ms.openlocfilehash: e656729fa9ea926681e560f40c4f43ce320a0d5e


---

# Configuração dos direitos de uso do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Quando você define a proteção em arquivos ou emails usando o Azure Rights Management (Azure RMS) e não usa um modelo, você deve configurar os direitos de uso por conta própria. Além disso, ao configurar modelos personalizados para o Azure RMS, selecione os direitos de uso que serão aplicados automaticamente quando o modelo é selecionado por usuários, administradores, ou serviços configurados. Por exemplo, no portal clássico do Azure, você pode selecionar funções que configuram um agrupamento lógico de direitos de uso ou pode configurar os direitos individuais.

Use este artigo para ajudá-lo a configurar os direitos de uso que você deseja para o aplicativo que está usando e compreender como esses direitos são interpretados pelos aplicativos.

## Direitos de uso e descrições
A tabela a seguir lista e descreve os direitos de uso compatíveis com o Rights Management e como eles são usados e interpretados. Eles estão listados pelo **Nome comum**, que normalmente é como você pode ver o direito de uso exibido ou referenciado, como uma versão mais amigável do valor de palavra única que é usada no código (o valor de **Codificação na política**). **Constante ou Valor de API** é o nome do SDK para uma chamada à API da MSIPC usada quando você grava um aplicativo habilitado para RMS que verifica um direito de uso ou adiciona um direito de uso a uma política.


|Right|Descrição|Implementação|
|-------------------------------|---------------------------|-----------------|
|Nome comum: **Editar Conteúdo, Editar** <br /><br />Codificação na política: **DOCEDIT**|Permite que usuário modifique, reorganize, formate ou filtre o conteúdo dentro do aplicativo. Ele não concede o direito para salvar a cópia editada.|Direitos personalizados do Office: como parte das opções **Alterar** e **Controle Total**. <br /><br />Nome no portal clássico do Azure: **Editar Conteúdo**<br /><br />Nome em modelos do AD RMS: **Editar** <br /><br />Constante de API ou valor: não aplicável.|
|Nome comum: **Salvar** <br /><br />Codificação na política: **EDIT**|Permite ao usuário salvar o documento em seu local atual.<br /><br />Em aplicativos do Office, esse direito também permite que o usuário modifique o documento.|Direitos personalizados do Office: como parte das opções **Alterar** e **Controle Total**. <br /><br />Nome no portal clássico do Azure: **Salvar Arquivo**<br /><br />Nome em modelos do AD RMS: **Salvar** <br /><br />Constante ou valor de API: `IPC_GENERIC_WRITE L"EDIT"`|
|Nome comum: **Comentar** <br /><br />Codificação na política: **COMMENT**|Habilita a opção para adicionar anotações ou comentários ao conteúdo.<br /><br />Esse direito está disponível no SDK, está disponível como uma política ad hoc no módulo de proteção por RMS para Windows PowerShell e foi implementado em alguns aplicativos de fornecedores de software. No entanto, ele não é amplamente usado e não é suportado atualmente por aplicativos do Office.|Direitos personalizados do Office: não implementado. <br /><br />Nome no portal clássico do Azure: não implementado.<br /><br />Nome em modelos do AD RMS: não implementado. <br /><br />Constante ou valor de API: `IPC_GENERIC_COMMENT L"COMMENT`|
|Nome comum: **Salvar Como, Exportar** <br /><br />Codificação na política: **EXPORT**|Habilita a opção para salvar o conteúdo com um nome de arquivo diferente (Salvar como). Para documentos do Office, o arquivo pode ser salvo sem proteção.<br /><br />Esse direito também permite que o usuário execute outras opções de exportação em aplicativos, como **Enviar para o OneNote**.|Direitos personalizados do Office: como parte das opções **Alterar** e **Controle Total**. <br /><br />Nome no portal clássico do Azure: **Exportar Conteúdo (Salvar Como)**<br /><br />Nome em modelos do AD RMS: **Exportar (Salvar Como)** <br /><br />Constante ou valor de API: `IPC_GENERIC_EXPORT L"EXPORT"`|
|Nome comum: **Encaminhar** <br /><br />Codificação na política: **FORWARD**|Habilita a opção para encaminhar uma mensagem de email e adicionar destinatários nas linhas **Para** e **Cc** . Esse direito não se aplica a documentos; apenas mensagens de email.<br /><br />Não permite que o encaminhador conceda direitos a outros usuários como parte da ação de encaminhamento.|Direitos personalizados do Office: negados ao usar a política padrão **Não Encaminhar**.<br /><br />Nome no portal clássico do Azure: **Encaminhar**<br /><br />Nome em modelos do AD RMS: **Encaminhar** <br /><br />Constante ou valor de API: `IPC_EMAIL_FORWARD L"FORWARD"`|
|Nome comum: **Controle Total** <br /><br />Codificação na política: **OWNER**|Concede todos os direitos ao documento e todas as ações disponíveis podem ser executadas.<br /><br />Inclui a capacidade de remover a proteção e proteger novamente um documento.|Direitos personalizados do Office: como a opção personalizada **Controle Total**.<br /><br />Nome no portal clássico do Azure: **Controle Total**<br /><br />Nome em modelos do AD RMS: **Controle Total** <br /><br />Constante ou valor de API: `IPC_GENERIC_ALL L"OWNER"`|
|Nome comum: **Imprimir** <br /><br />Codificação na política: **PRINT**|Habilita as opções para imprimir o conteúdo.|Direitos personalizados do Office: como a opção **Imprimir Conteúdo** nas permissões personalizadas. Não é uma configuração por destinatário.<br /><br />Nome no portal clássico do Azure: **Imprimir**<br /><br />Nome em modelos do AD RMS: **Imprimir** <br /><br />Constante ou valor de API: `IPC_GENERIC_PRINT L"PRINT"`|
|Nome comum: **Responder** <br /><br />Codificação na política: **PRINT**|Habilita a opção **Responder** em um cliente de email, sem permitir alterações nas linhas **Para** ou **Cc**.|Direitos personalizados do Office: não aplicável.<br /><br />Nome no portal clássico do Azure: **Responder**<br /><br />Nome em modelos do AD RMS: **Responder** <br /><br />Constante ou valor de API: `IPC_EMAIL_REPLY`|
|Nome comum: **Responder a Todos** <br /><br />Codificação na política: **REPLYALL**|Habilita a opção **Responder a todos** em um cliente de email, mas não permite que o usuário adicione destinatários nas linhas **Para** ou **Cc** .|Direitos personalizados do Office: não aplicável.<br /><br />Nome no portal clássico do Azure: **Responder a Todos**<br /><br />Nome em modelos do AD RMS: **Responder a Todos** <br /><br />Constante ou valor de API: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|Nome comum: **Exibir, Abrir, Ler** <br /><br />Codificação na política: **EXIBIR**|Permite que o usuário abra o documento e visualize o conteúdo.|Direitos personalizados do Office: como a política personalizada **Ler**, opção **Exibir**.<br /><br />Nome no portal clássico do Azure: **Exibir**<br /><br />Nome em modelos do AD RMS: **Responder a Todos** <br /><br />Constante ou valor de API: `IPC_GENERIC_READ L"VIEW"`|
|Nome comum: **Copiar** <br /><br />Codificação na política: **EXTRACT**|Habilita opções para copiar dados (incluindo capturas de tela) do documento para o mesmo documento ou outro.<br /><br />Em alguns aplicativos, ele também permite que todo o documento seja salvo no formato não protegido.|Direitos personalizados do Office: como a opção de política personalizada **Permitir que usuários com Acesso de leitura copiem conteúdo**.<br /><br />Nome no portal clássico do Azure: **Copiar e Extrair Conteúdo**<br /><br />Nome em modelos do AD RMS: **Extrair** <br /><br />Constante ou valor de API: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|Nome comum: **Permitir Macros** <br /><br />Codificação na política: **OBJMODEL**|Habilita a opção para executar macros ou realizar outro acesso remoto ou por programação ao conteúdo em um documento.|Direitos personalizados do Office: como a opção de política personalizada **Permitir o Acesso de Programação**. Não é uma configuração por destinatário.<br /><br />Nome no portal clássico do Azure: **Permitir Macros**<br /><br />Nome em modelos do AD RMS: **Permitir Macros** <br /><br />Constante de API ou valor: não implementado.|



## Direitos incluídos nos níveis de permissões

Alguns aplicativos agrupam os direitos de uso em níveis de permissões, para facilitar a seleção dos direitos de uso que normalmente são usados juntos. Estes níveis de permissões ajudam a abstrair um nível de complexidade dos usuários, então eles podem escolher as opções baseadas em funções.  Por exemplo, **Revisor** e **Coautor**. Embora essas opções muitas vezes mostram aos usuários um resumo dos direitos, elas podem não incluir todos os direitos listados na tabela anterior.

Use a tabela a seguir para obter uma lista desses níveis de permissões e uma lista completa dos direitos que eles contêm.

|Nível de Permissões|Aplicativos|Direitos incluídos (nome comum)|
|---------------------|----------------|---------------------------------|
|Visualizador|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Exibir, Abrir, Ler; Responder; Responder a Todos|
|Revisor|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Exibir, Abrir, Ler; Salvar; Editar Conteúdo, Editar; Responder [[1]](#footnote-1); Responder a Todos [[1]](#footnote-1); Encaminhar [[1]](#footnote-1)|
|Coautor|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Exibir, Abrir, Ler; Salvar; Editar Conteúdo, Editar; Copiar; Exibir Direitos; Permitir Macros; Salvar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a Todos [[1]](#footnote-1); Encaminhar [[1]](#footnote-1)|
|Coproprietário|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Exibir, Abrir, Ler; Salvar; Editar Conteúdo, Editar; Copiar; Exibir Direitos; Permitir Macros; Salvar como, Exportar; Imprimir; Responder [[1]](#footnote-1); Responder a Todos [[1]](#footnote-1); Encaminhar [[1]](#footnote-1); Controle Total|

----

###### Nota de rodapé 1
Não se aplica ao aplicativo de compartilhamento Rights Management para Windows.

## Direitos incluídos nos modelos padrão
Os direitos que estão incluídos com os modelos padrão são as seguintes:

|Nome para Exibição|Direitos incluídos (nome comum)|
|----------------|---------------------------------|
|&lt;*nome da organização*&gt;*- Somente exibição confidencial*|Modo de exibição, Abrir, Ler|
|&lt;*nome da organização*&gt; *- Confidencial*|Exibir, Abrir, Ler; Salvar; Editar Conteúdo, Editar; Exibir Direitos Atribuídos; Permitir Macros; Encaminhar; Responder; Responder a Todos|

## Opções Não Encaminhar para emails

Os clientes e serviços do Exchange (por exemplo, o cliente do Outlook, o aplicativo Outlook Web Access e as regras de transporte do Exchange) têm uma opção adicional de proteção de direitos de informações para emails: **Não Encaminhar**. 

Embora essa opção apareça para os usuários (e os administradores do Exchange) como se fosse um modelo padrão do Rights Management que eles podem selecionar, **Não Encaminhar** não é um modelo. Isso explica por que você não a vê no portal clássico do Azure quando você exibe e gerencia modelos do Azure RMS. Em vez disso, a opção **Não Encaminhar** é um conjunto de direitos que é aplicado dinamicamente por usuários para seus destinatários de email.

Quando a opção **Não Encaminhar** é aplicada a um email, os destinatários não podem encaminhá-lo, imprimi-lo, copiá-lo, salvar anexos ou salvá-lo com um nome diferente. Por exemplo, no cliente do Outlook, o botão Encaminhar não fica disponível, as opções de menu **Salvar Como**, **Salvar Anexo** e **Imprimir** não estão disponíveis e você não pode adicionar ou alterar destinatários nas caixas **Para**, **Ccc** ou **Cco**.

Há uma distinção importante entre aplicar a opção **Não Encaminhar** e aplicar um modelo que não concede o direito de Encaminhar um email: a opção **Não Encaminhar** usa uma lista dinâmica de usuários autorizados baseada nos destinatários escolhidos pelo usuário do email original, enquanto os direitos no modelo têm uma lista estática de usuários autorizados que o administrador especificou anteriormente. Qual é a diferença? Vejamos um exemplo: 

Uma usuária deseja enviar algumas informações por email para pessoas específicas do departamento de marketing, e essas informações não devem ser compartilhadas com mais ninguém. Ela deve proteger o email com um modelo que restringe os direitos (exibir, responder e salvar) para o departamento de marketing?  Ou deve escolher a opção **Não Encaminhar**? Ambas as opções fariam com que os destinatários não pudessem encaminhar o email. 

- Se ela aplicasse o modelo, os destinatários ainda poderiam compartilhar as informações com outras pessoas no departamento de marketing. Por exemplo, um destinatário poderia usar o Explorer para arrastar e soltar o email para um local compartilhado ou uma unidade USB. Agora, qualquer pessoa do departamento de marketing (e o proprietário do email) com acesso a esse local poderia exibir as informações no email.
 
- Se ela aplicasse a opção **Não Encaminhar**, os destinatários não poderiam compartilhar as informações com nenhuma outra pessoa no departamento de marketing movendo o email para outro local. Nesse cenário, somente os destinatários originais (e o proprietário de email) poderiam exibir as informações no email.

> [!NOTE] 
> Use **Não Encaminhar** quando for importante que somente os destinatários que o remetente escolher possam ver as informações no email. Use um modelo para emails para restringir direitos a um grupo de pessoas que o administrador especifica antecipadamente, independentemente dos destinatários escolhidos pelo remetente.




## Consulte também
[Configurando modelos personalizados do Azure Rights Management](configure-custom-templates.md)




<!--HONumber=Aug16_HO2-->


