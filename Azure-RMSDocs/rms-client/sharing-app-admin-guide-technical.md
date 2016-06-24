---
# required metadata

title: Visão geral técnica do aplicativo de compartilhamento Microsoft Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Visão geral técnica do aplicativo de compartilhamento Microsoft Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*


O aplicativo de compartilhamento Microsoft Rights Management é um aplicativo para download opcional do Microsoft Windows e outras plataformas que oferece os seguintes recursos:

-   Proteção de um único arquivo, ou múltiplos arquivos em massa, ou ainda todos os arquivos em uma pasta selecionada.

-   Suporte completo para a proteção de qualquer tipo de arquivo e um visualizador nativo para os tipos de arquivos de texto e imagem mais comuns.

-   Proteção genérica para arquivos que não dão suporte à proteção de RMS.

-   Total interoperabilidade com arquivos protegidos usando o Office Information Rights Management (IRM).

-   Total interoperabilidade com arquivos PDF protegidos usando a FCI (Infraestrutura de Classificação de Arquivos) e as ferramentas de criação de PDF com suporte.

O aplicativo de compartilhamento Microsoft Rights Management usa o novo [AD RMS 2.1 runtime](http://www.microsoft.com/download/details.aspx?id=38396). Usando a funcionalidade do AD RMS 2.1, o aplicativo de compartilhamento Microsoft Rights Management fornece aos usuários finais uma experiência simples de proteção e de consumo.

Com o lançamento de outubro de 2013 do RMS, você pode nativamente proteger documentos usando o Office 2010 e enviá-los para pessoas de outra empresa, que pode, em seguida, consumi-los usando o Azure RMS. Além disso, com esta versão, se você usar o AD RMS em Modo Criptográfico 2, você pode usar o RMS para indivíduos e consumir conteúdo de pessoas de outra empresa que usam o Azure RMS. Para obter mais informações sobre o modo criptográfico 2, consulte [Modos de criptografia do AD RMS](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

Para obter informações de implantação, consulte [Implantação automática para o aplicativo de compartilhamento Microsoft Rights Management](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)

## Níveis de proteção - nativo e genérico
Aplicativo de compartilhamento Microsoft Rights Management oferece suporte a proteção em dois níveis diferentes, conforme descrito na tabela a seguir.

|Tipo de proteção|Nativo|Genérico|
|----------------------|----------|-----------|
|Descrição|Para arquivos de texto, imagem, do Microsoft Office (Word, Excel, PowerPoint), .pdf e para tipos de arquivo de outros aplicativos que suportam o AD RMS, a proteção nativa fornece um alto nível de proteção que inclui criptografia e aplicação de direitos (permissões).|Para todos os outros aplicativos e tipos de arquivo, a proteção genérica oferece um nível de proteção que inclui tanto o encapsulamento de arquivos o tipo de arquivo .pfile e autenticação para verificar se um usuário está autorizado a abrir o arquivo.|
|Proteção|Os arquivos estão completamente criptografados e a proteção é imposta das seguintes maneiras:<br /><br />- Para que conteúdo protegido seja processado, autenticação bem-sucedida deve ocorrer para aqueles que recebem o arquivo por email ou recebem acesso a ele por meio de permissões de arquivo ou compartilhamento.<br /><br />- Além disso, direitos de uso e a política definida pelo proprietário do conteúdo quando os arquivos são protegidos são totalmente aplicadas quando o conteúdo é renderizado no Visualizador de IP (para arquivos de texto e imagem protegidos) ou o aplicativo associado (para todos os outros tipos de arquivo com suporte).|A proteção de arquivos é imposta das seguintes maneiras:<br /><br />- Para que conteúdo protegido seja processado, autenticação bem-sucedida deve ocorrer para aqueles que estão autorizados a abrir o arquivo e recebem acesso a ele. Se a autorização falhar, o arquivo não abre.<br /><br />- Direitos de uso e a política definida pelo proprietário do conteúdo são exibidos para informar aos usuários autorizados a política de uso pretendido.<br /><br />- Log de auditoria de usuários autorizados a abrir e acessar arquivos ocorre, no entanto, nenhum direito de uso é aplicado por aplicativos sem suporte.|
|Padrão para tipos de arquivo|Isso é o nível de proteção padrão para os seguintes tipos de arquivo:<br /><br />- Arquivos de texto e imagem<br /><br />- Arquivos do Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato de documento portátil (.pdf)<br /><br />Para obter mais informações, consulte a seção a seguir, [Tipos de arquivo com suporte e extensões de nome de arquivo](#supported-file-types-and-file-name-extensions).|Isso é a proteção padrão para todos os outros tipos de arquivo (como .vsdx, .rtf e assim por diante) que não têm suporte pela proteção completa.|
Você pode alterar o nível de proteção padrão que o aplicativo de RMS sharing aplica. Você pode alterar o nível padrão de nativo para genérico, de genérico para nativo e até mesmo impedir que o aplicativo de aplicar proteção de compartilhamento do RMS. Para obter mais informações, consulte a seção [Alterando o nível de proteção padrão de arquivos](#changing-the-default-protection-level-of-files) neste artigo.

## Tipos de arquivo com suporte e extensões de nome de arquivo
A tabela a seguir lista os tipos de arquivos que são suportados nativamente pelo aplicativo de compartilhamento Microsoft Rights Management. Para esses tipos de arquivo, a extensão de nome de arquivo original é alterada quando a proteção nativa é aplicada, e esses arquivos se tornam somente leitura.

Além disso, quando o aplicativo RMS sharing nativamente protege um arquivo do Word, Excel ou PowerPoint cujos usuários protegem compartilhando, essa ação cria automaticamente um segundo arquivo que é uma cópia do original com o mesmo nome, mas com **.ppdf** de extensão de nome de arquivo¹. Esta versão do arquivo garante que os destinatários que instalem o aplicativo de RMS sharing sempre possam abrir o arquivo que tenha proteção nativa aplicada.

Para arquivos protegidos genericamente, a extensão de nome de arquivo original sempre é alterada para. pfile.

> [!WARNING] Se você tiver firewalls, proxies da web ou software de segurança que inspecionem e atuem de acordo com as extensões de nome de arquivo, talvez seja necessário reconfigurá-los para dar suporte a essas novas extensões de nome de arquivo.

|Extensão de nome de arquivo original|Extensão protegida por RMS|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|
¹ Renderização de PDF fornecida pela Foxit. Copyright © 2003–2014 by Foxit Coupouation.

A tabela a seguir lista os tipos de arquivo para os quais o aplicativo de compartilhamento Microsoft Rights Management oferece suporte nativo em Microsoft Office 2016, Office 2013 e Office 2010. Para esses arquivos, a extensão de nome de arquivo permanece o mesmo depois que o arquivo está protegido pelo RMS.

|Tipos de arquivo compatíveis com o Office|Tipos de arquivo compatíveis com o Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### Alterando o nível de proteção padrão de arquivos
Você pode alterar como o aplicativo de compartilhamento RMS protege arquivos editando o registro. Por exemplo, você pode forçar os arquivos que oferecem suporte a proteção nativa a serem genericamente protegidos pelo aplicativo de RMS sharing.

Razões para que você talvez queira fazer isso.

-   Para garantir que todos os usuários possam abri-lo em seus dispositivos móveis.

-   Para garantir que todos os usuários possam abrir o arquivo que não tenha um aplicativo que oferece suporte à proteção nativa.

-   Para acomodar sistemas de segurança que atuam em arquivos por sua extensão de nome de arquivo e podem ser reconfigurados para acomodar a extensão de nome de arquivo. pfile, mas não podem ser reconfigurados para acomodar várias extensões de nome de arquivo para proteção nativa.

Igualmente, você pode forçar o aplicativo RMS sharing a aplicar a proteção nativa a arquivos como padrão, que teriam a proteção genérica aplicada. Isso pode ser apropriado se você tiver um aplicativo que oferece suporte a RMS APIs – por exemplo, um aplicativo de linha de negócios escrito por seus desenvolvedores internos ou um aplicativo comprado de um fornecedor de software independente (ISV).

Você também pode forçar o aplicativo RMS sharing a bloquear a proteção de arquivos (não aplicar proteção nativa ou proteção genérica). Por exemplo, isso pode ser necessário se você tiver um aplicativo automatizado ou serviço que deve ser capaz de abrir um arquivo específico para processar seu conteúdo. Quando você bloqueia a proteção para um tipo de arquivo, os usuários não podem usar o aplicativo de compartilhamento RMS para proteger um arquivo com esse tipo de arquivo. Quando eles tentam, eles veem uma mensagem informando que o administrador impediu a proteção e precisam cancelar suas ações para proteger o arquivo.

Para configurar o aplicativo RMS sharing a aplicar a proteção genérica a todos os arquivos como padrão, que teriam a proteção nativa aplicada, faça as seguintes edições no registro:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: crie uma nova chave nomeada *.

    Essa configuração denota arquivos com qualquer extensão de nome de arquivo.

2.  Na chave recém adicionada de HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\\\*, crie um novo valor de cadeia (REG_SZ) nomeada **Criptografia** que possua o valor de dados de **Pfile**.

    Essa configuração resulta no aplicativo RMS sharing aplicando proteção genérica.

Essas duas configurações resultam no aplicativo RMS sharing aplicando proteção genérica para todos os arquivos que têm uma extensão de nome de arquivo. Se esse for o seu objetivo, nenhuma configuração adicional será necessária. No entanto, você pode definir exceções para tipos de arquivo específicos, para que eles ainda sejam protegidos nativamente. Para fazer isso, você deve fazer três edições adicionais do registro para cada tipo de arquivo:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: adicionar uma nova chave com o nome da extensão de nome de arquivo (sem o ponto anterior).

    Por exemplo, para arquivos que têm uma extensão .docx de nome de arquivo, crie uma chave chamada **DOCX**.

2.  Na chave de tipo de arquivo recém adicionada (por exemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), crie um novo valor DWORD chamado **AllowPFILEEncryption**, com o valor **0**.

3.  Na chave de tipo de arquivo recém adicionada (por exemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), crie um novo valor de cadeia de caracteres chamado **Criptografia**, com o valor **Nativo**.

Como resultado dessas configurações, todos os arquivos são genericamente protegidos exceto os arquivos que têm uma extensão de nome de arquivo. docx, que são protegidos nativamente pelo aplicativo RMS sharing.

Repita estes três passos para outros tipos de arquivos que você queira definir como exceções porque eles suportam proteção nativa e você não quer que eles sejam genericamente protegidos pelo aplicativo RMS sharing.

Você pode fazer edições de registro semelhantes para outros cenários, alterando o valor da cadeia **criptografia** que aceita os seguintes valores:

-   **Pfile**: Proteção genérica

-   **Nativo**: Proteção nativa

-   **Desativado**: Bloquear proteção

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)



<!--HONumber=May16_HO3-->


