---
title: TESTAR a configuração dos direitos de uso do Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# ANTES DE: configurar os direitos de uso do Azure Rights Management
Quando você define a proteção em arquivos ou emails usando o Azure Rights Management (Azure RMS) e não usa um modelo, você deve configurar os direitos de uso por conta própria. Além disso, ao configurar modelos personalizados para o Azure RMS, selecione os direitos de uso que serão aplicados automaticamente quando o modelo é selecionado por usuários, administradores, ou serviços configurados. Por exemplo, no portal clássico do Azure, você pode selecionar funções que configuram um agrupamento lógico de direitos de uso ou pode configurar os direitos individuais.

Use este artigo para ajudá-lo a configurar os direitos de uso que você deseja para o aplicativo que está usando e compreender como esses direitos são interpretados pelos aplicativos.

## Direitos de uso e descrições
As seções a seguir listam e descrevem os direitos de uso aos quais o Rights Management dá suporte e como eles são usados e interpretados. Nessas seções, o **Nome comum** normalmente é como você pode ver o direito de uso exibido ou referenciado, como uma versão mais amigável do valor de palavra única que é usada no código (o valor de **Codificação na política**). **Constante ou Valor de API** é o nome do SDK para uma chamada à API da MSIPC usada quando você grava um aplicativo habilitado para RMS que verifica um direito de uso ou adiciona um direito de uso a uma política.

### Nome comum: Editar conteúdo, Editar

**Codificação na política:**

- DOCEDIT

**Descrição:**

- Permite que usuário modifique, reorganize, formate ou filtre o conteúdo dentro do aplicativo. Ele não concede o direito para salvar a cópia editada.

**Implementação de direitos personalizados do Office:**

- Como parte das opções **Alterar** e **Controle total** .

**Nome no portal clássico do Azure:**

- **Editar conteúdo**

**Nome em modelos do AD RMS:**

- **Editar**

**Constante ou valor de API:**

- Não aplicável

**Informação adicional:**

- Em aplicativos do Office, esse direito também permite que o usuário salve o documento.

---

### Nome comum: Salvar

**Codificação na política:**

- EDITAR

**Descrição:**

- Permite ao usuário salvar o documento em seu local atual.

**Implementação de direitos personalizados do Office:**

- Como parte das opções **Alterar** e **Controle total** .

**Nome no portal clássico do Azure:**

- **Salvar arquivo**

**Nome em modelos do AD RMS:**

- Salvar

**Constante ou valor de API:**

- IPC_GENERIC_WRITEL"EDIT"

**Informação adicional:**

- Em aplicativos do Office, esse direito também permite que o usuário modifique o documento.

---

### Nome comum: Comentar

**Codificação na política:**

- COMENTAR

**Descrição:**

- Habilita a opção para adicionar anotações ou comentários ao conteúdo.

**Implementação de direitos personalizados do Office:**

- Não foi implementado.

**Nome no portal clássico do Azure:**

- Não foi implementado.

**Nome em modelos do AD RMS:**

- Não foi implementado.

**Constante ou valor de API:**

- IPC_GENERIC_COMMENTL"COMMENT

**Informação adicional:**

- Esse direito está disponível no SDK, está disponível como uma política ad hoc no módulo de proteção por RMS para Windows PowerShell e foi implementado em alguns aplicativos de fornecedores de software. No entanto, ele não é amplamente usado e não é suportado atualmente por aplicativos do Office.

---

### Nome comum: Salvar como, Exportar

**Codificação na política:**

- EXPORTAR

**Descrição:**

- Habilita a opção para salvar o conteúdo com um nome de arquivo diferente (Salvar como). Dependendo do aplicativo, o arquivo pode ser salvo sem proteção.

**Implementação de direitos personalizados do Office:**

- Como parte das opções **Alterar** e **Controle total** .

**Nome no portal clássico do Azure:**

- **Exportar o conteúdo (Salvar como)**

**Nome em modelos do AD RMS:**

- **Exportar (Salvar como)**

**Constante ou valor de API:**

- IPC_GENERIC_EXPORTL"EXPORT"

**Informação adicional:**

- Esse direito também permite que o usuário execute outras opções de exportação em aplicativos, como **Enviar para o OneNote**.

---

### Nome comum: Encaminhar

**Codificação na política:**

- ENCAMINHAR

**Descrição:**

- Habilita a opção para encaminhar uma mensagem de email e adicionar destinatários nas linhas **Para** e **Cc** .

**Implementação de direitos personalizados do Office:**

- Negado ao usar a política padrão **não encaminhar** .

**Nome no portal clássico do Azure:**

- **Encaminhar**

**Nome em modelos do AD RMS:**

- **Encaminhar**

**Constante ou valor de API:**

- IPC_EMAIL_FORWARDL"FORWARD"

**Informação adicional:**

- Não permite que o encaminhador conceda direitos a outros usuários como parte da ação de encaminhamento.

---

### Nome comum: Controle total

**Codificação na política:**

- PROPRIETÁRIO

**Descrição:**

- Concede todos os direitos ao documento e todas as ações disponíveis podem ser executadas.

**Implementação de direitos personalizados do Office:**

- Como a opção personalizada **Controle total** .

**Nome no portal clássico do Azure:**

- **Controle total**

**Nome em modelos do AD RMS:**

- **Controle total**

**Constante ou valor de API:**

- IPC_GENERIC_ALLL"OWNER"

**Informação adicional:**

- Inclui a capacidade de remover a proteção.

---

### Nome comum: Imprimir

**Codificação na política:**

- PRINT

**Descrição:**

- Habilita as opções para imprimir o conteúdo.

**Implementação de direitos personalizados do Office:**

- Como a opção **Imprimir conteúdo** nas permissões personalizadas. Não é uma configuração por destinatário.

**Nome no portal clássico do Azure:**

- **Imprimir**

**Nome em modelos do AD RMS:**

- **Imprimir**

**Constante ou valor de API:**

- IPC_GENERIC_PRINTL"PRINT

---

### Nome comum: Responder

**Codificação na política:**

- RESPONDER

**Descrição:**

- Habilita a opção Responder em um cliente de email, sem permitir alterações nas linhas **Para** ou **Cc** .

**Implementação de direitos personalizados do Office:**

- Não aplicável

**Nome no portal clássico do Azure:**

- **Responder**

**Nome em modelos do AD RMS:**

- **Responder**

**Constante ou valor de API:**

- IPC_EMAIL_REPLY

---

### Nome comum: Responder a todos

**Codificação na política:**

- REPLYALL

**Descrição:**

- Habilita a opção **Responder a todos** em um cliente de email, mas não permite que o usuário adicione destinatários nas linhas **Para** ou **Cc** .

**Implementação de direitos personalizados do Office:**

- Não aplicável

**Nome no portal clássico do Azure:**

- **Responder a todos**

**Nome em modelos do AD RMS:**

- **Responder a todos**

**Constante ou valor de API:**

- IPC_EMAIL_REPLYALLL"REPLYALL"

---

### Nome comum: Exibir, Abrir, Ler

**Codificação na política:**

- EXIBIR

**Descrição:**

- Permite que o usuário abra o documento e visualize o conteúdo.

**Implementação de direitos personalizados do Office:**

- Como a política personalizada **Leitura** , opção **Exibição** .

**Nome no portal clássico do Azure:**

- **Exibir Conteúdo**

**Nome em modelos do AD RMS:**

- **Exibir**

**Constante ou valor de API:**

- IPC_GENERIC_READL"VIEW"

---

### Nome comum: direitos de exibição

**Codificação na política:**

- EXIBIRRIGHTSDATA

**Descrição:**

- Permite que o usuário veja a política aplicada ao documento.

**Implementação de direitos personalizados do Office:**

- Não foi implementado.

**Nome no portal clássico do Azure:**

- **Exibir direitos atribuídos**

**Nome em modelos do AD RMS:**

- **Direitos de exibição**

**Constante ou valor de API:**

- IPC_READ_RIGHTSL"VIEWRIGHTSDATA"

---

### Nome comum: direitos de exibição

**Codificação na política:**

- EXIBIRRIGHTSDATA

**Descrição:**

- Permite que o usuário veja a política aplicada ao documento.

**Implementação de direitos personalizados do Office:**

- Não foi implementado.

**Nome no portal clássico do Azure:**

- **Exibir direitos atribuídos**

**Nome em modelos do AD RMS:**

- **Direitos de exibição**

**Constante ou valor de API:**

- IPC_READ_RIGHTSL"VIEWRIGHTSDATA"

**Informação adicional:**

- Ignorado por alguns aplicativos.

---

### Nome comum: Direitos de alteração

**Codificação na política:**

- EDITRIGHTSDATA

**Descrição:**

- Permite que o usuário altere a política que é aplicada ao documento. Inclui a remoção da proteção.

**Implementação de direitos personalizados do Office:**

- Não foi implementado.

**Nome no portal clássico do Azure:**

- **Direitos de alteração**

**Nome em modelos do AD RMS:**

- **Editar direitos**

**Constante ou valor de API:**

- IPC_WRITE_RIGHTSL"EDITRIGHTSDATA"

---

### Nome comum: Permitir macros

**Codificação na política:**

- OBJMODEL

**Descrição:**

- Habilita a opção para executar macros ou realizar outro acesso remoto ou por programação ao conteúdo em um documento.

**Implementação de direitos personalizados do Office:**

- Como a opção de política personalizada **Permitir acesso programático** . Não é uma configuração por destinatário.

**Nome no portal clássico do Azure:**

- **Permitir Macros**

**Nome em modelos do AD RMS:**

- **Permitir Macros**

**Constante ou valor de API:**

- Não aplicável

---


|Nome comum|Codificação na política|Descrição|Implementação de direitos personalizados do Office|Nome no portal clássico do Azure|Nome em modelos do AD RMS|API constant ou value|Informações adicionais|
|---------------|----------------------|---------------|------------------------------------------|-------------------------------------|----------------------------|-------------------------|--------------------------|
|Editar conteúdo, editar|DOCEDIT|Permite que usuário modifique, reorganize, formate ou filtre o conteúdo dentro do aplicativo. Ele não concede o direito para salvar a cópia editada.|Como parte das opções **Alterar** e **Controle total** .|**Editar conteúdo**|**Editar**|Não aplicável|Em aplicativos do Office, esse direito também permite que o usuário salve o documento.|
|Salvar|EDITAR|Permite ao usuário salvar o documento em seu local atual.|Como parte das opções **Alterar** e **Controle total** .|**Salvar arquivo**|**Salvar**|IPC_GENERIC_WRITEL"EDIT"|Em aplicativos do Office, esse direito também permite que o usuário modifique o documento.|
|Comentário|COMENTAR|Habilita a opção para adicionar anotações ou comentários ao conteúdo.|Não implementado|Não implementado|Não implementado|IPC_GENERIC_COMMENTL"COMMENT"|Esse direito está disponível no SDK, está disponível como uma política ad hoc no módulo de proteção por RMS para Windows PowerShell e foi implementado em alguns aplicativos de fornecedores de software. No entanto, ele não é amplamente usado e não é suportado atualmente por aplicativos do Office.|
|Salvar como, Exportar|EXPORTAR|Habilita a opção para salvar o conteúdo com um nome de arquivo diferente (Salvar como). Dependendo do aplicativo, o arquivo pode ser salvo sem proteção.|Como parte das opções **Alterar** e **Controle total** .|**Exportar o conteúdo (Salvar como)**|**Exportar (Salvar como)**|IPC_GENERIC_EXPORTL"EXPORT"|Esse direito também permite que o usuário execute outras opções de exportação em aplicativos, como **Enviar para o OneNote**.|
|Encaminhar|ENCAMINHAR|Habilita a opção para encaminhar uma mensagem de email e adicionar destinatários nas linhas **Para** e **Cc** .|Negado ao usar a política padrão **não encaminhar** .|**Encaminhar**|**Encaminhar**|IPC_EMAIL_FORWARDL"FORWARD"|Não permite que o encaminhador conceda direitos a outros usuários como parte da ação de encaminhamento.|
|Controle total|PROPRIETÁRIO|Concede todos os direitos ao documento e todas as ações disponíveis podem ser executadas.|Como a opção personalizada **Controle total** .|**Controle total**|**Controle total**|IPC_GENERIC_ALLL"OWNER"|Inclui a capacidade de remover a proteção.|
|Imprimir|PRINT|Habilita as opções para imprimir o conteúdo.|Como a opção **Imprimir conteúdo** nas permissões personalizadas. Não é uma configuração por destinatário.|**Imprimir**|**Imprimir**|IPC_GENERIC_PRINTL"PRINT|Nenhuma informação adicional|
|Responder|RESPONDER|Habilita a opção Responder em um cliente de email, sem permitir alterações nas linhas **Para** ou **Cc** .|Não aplicável|**Responder**|**Responder**|IPC_EMAIL_REPLY|Nenhuma informação adicional|
|Responder a todos|REPLYALL|Habilita a opção **Responder a todos** em um cliente de email, mas não permite que o usuário adicione destinatários nas linhas **Para** ou **Cc** .|Não aplicável|**Responder a todos**|**Responder a todos**|IPC_EMAIL_REPLYALLL"REPLYALL"|Nenhuma informação adicional|
|Modo de exibição, Abrir, Ler|EXIBIR|Permite que o usuário abra o documento e visualize o conteúdo.|Como a política personalizada **Leitura** , opção **Exibição** .|**Exibir Conteúdo**|**Exibição**|IPC_GENERIC_READL"VIEW"|Nenhuma informação adicional|
|Copiar|EXTRAIR|Habilita opções para copiar dados (incluindo capturas de tela) do documento para o mesmo documento ou outro.|Como a opção de política personalizada **Permitir que usuários com acesso de leitura copiem conteúdo** .|**Copiar e extrair conteúdo**|**Extrair**|IPC_GENERIC_EXTRACTL"EXTRACT"|Em alguns aplicativos, ele também permite que todo o documento seja salvo no formato não protegido.|
|Direitos de exibição|EXIBIRRIGHTSDATA|Permite que o usuário veja a política aplicada ao documento.|Não implementado|**Exibir direitos atribuídos**|**Direitos de exibição**|IPC_READ_RIGHTSL"VIEWRIGHTSDATA"|Ignorado por alguns aplicativos.|
|Direitos de alteração|EDITRIGHTSDATA|Permite que o usuário altere a política que é aplicada ao documento. Inclui a remoção da proteção.|Não implementado|**Direitos de alteração**|**Editar direitos**|IPC_WRITE_RIGHTSL"EDITRIGHTSDATA"|Nenhuma informação adicional|
|Permitir Macros|OBJMODEL|Habilita a opção para executar macros ou realizar outro acesso remoto ou por programação ao conteúdo em um documento.|Como a opção de política personalizada **Permitir acesso programático** . Não é uma configuração por destinatário.|**Permitir Macros**|**Permitir Macros**|Não aplicável|Nenhuma informação adicional|

## Direitos incluídos nos níveis de permissões
Alguns aplicativos agrupam os direitos de uso em níveis de permissões, para facilitar a seleção dos direitos de uso que normalmente são usados juntos. Estes níveis de permissões ajudam a abstrair um nível de complexidade dos usuários, então eles podem escolher as opções baseadas em funções.  Por exemplo, **Revisor** e **Coautor**. Embora essas opções muitas vezes mostram aos usuários um resumo dos direitos, elas podem não incluir todos os direitos listados na tabela anterior.

Use a tabela a seguir para obter uma lista desses níveis de permissões e uma lista completa dos direitos que eles contêm.

|Nível de Permissões|Aplicativos|Direitos incluídos (nome comum)|
|---------------------|----------------|---------------------------------|
|Visualizador|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Modo de exibição, Abrir, Ler<br /><br />Responder<br /><br />Responder a todos|
|Revisor|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Modo de exibição, Abrir, Ler<br /><br />Salvar<br /><br />Editar conteúdo, editar<br /><br />Responder [nota de rodapé 1]<br /><br />Responder a todos [nota de rodapé 1]<br /><br />Encaminhar [nota de rodapé 1]|
|Coautor|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Modo de exibição, Abrir, Ler<br /><br />Salvar<br /><br />Editar conteúdo, editar<br /><br />Copiar<br /><br />Direitos de exibição<br /><br />Direitos de alteração<br /><br />Permitir Macros<br /><br />Salvar como, Exportar<br /><br />Imprimir<br /><br />Responder [nota de rodapé 1]<br /><br />Responder a todos [nota de rodapé 1]<br /><br />Encaminhar [nota de rodapé 1]|
|Coproprietário|Portal clássico do Azure<br /><br />Aplicativo e compartilhamento Rights Management para Windows|Modo de exibição, Abrir, Ler<br /><br />Salvar<br /><br />Editar conteúdo, editar<br /><br />Copiar<br /><br />Direitos de exibição<br /><br />Direitos de alteração<br /><br />Permitir Macros<br /><br />Salvar como, Exportar<br /><br />Imprimir<br /><br />Responder [nota de rodapé 1]<br /><br />Responder a todos [nota de rodapé 1]<br /><br />Encaminhar [nota de rodapé 1]<br /><br />Controle total|
Nota de rodapé 1: não se aplica ao aplicativo de compartilhamento Rights Management para Windows

## Direitos incluídos nos modelos padrão
Os direitos que estão incluídos com os modelos padrão são as seguintes:

|Nome para Exibição|Direitos incluídos (nome comum)|
|----------------|---------------------------------|
|&lt;nome da organização&gt; - somente exibição confidencial|Modo de exibição, Abrir, Ler|
|&lt;nome da organização&gt; - confidencial|Modo de exibição, Abrir, Ler<br /><br />Salvar<br /><br />Editar conteúdo, editar<br /><br />Direitos de exibição<br /><br />Permitir Macros<br /><br />Encaminhar<br /><br />Responder<br /><br />Responder a todos|

## Consulte também
[Configurando o Azure Rights Management](configuring-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


