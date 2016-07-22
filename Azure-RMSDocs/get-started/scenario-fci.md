---
title: "Cenário – Proteger ficheiros numa partilha de servidor de ficheiros | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: c16098a2d0fe41748280704716a2eeef8921a6fa


---

# Cenário – Proteger ficheiros numa partilha de servidor de ficheiros

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação do utilizador associada utilizam o Azure Rights Management para a proteção em volume de todos os ficheiros que pretende proteger num servidor de ficheiros, de modo a garantir que apenas os funcionários da sua organização podem aceder aos mesmos, mesmo que sejam copiados e guardados num armazenamento que não está sob o controlo do seu departamento de TI ou enviados por e-mail para outras pessoas.

Estas instruções utilizam um dos modelos predefinidos, que restringe o acesso a todos os funcionários com todos os direitos de utilização. Contudo, se for necessário, pode restringir mais os direitos de acesso e de utilização ao configurar um modelo personalizado em vez de utilizar um modelo predefinido.

As instruções aplicam-se às seguintes circunstâncias:

-   É necessário proteger todos os tipos de ficheiro e não apenas os ficheiros do Office. Os ficheiros que não podem ser protegidos nativamente pelo Azure RMS serão protegidos genericamente.

-   Serão protegidos todos os ficheiros no caminho especificado (incluindo as subpastas).

-   A proteção é reaplicada a todos os ficheiros de acordo com uma agenda, para garantir que as alterações aos modelos de política de direitos são aplicadas aos ficheiros protegidos.

## Instruções de implementação
![Instruções do administrador para a Implementação Rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Certifique-se de que os seguintes requisitos são cumpridos e, em seguida, siga as instruções dos procedimentos de suporte antes de avançar para a documentação do utilizador.

## Requisitos para este cenário
Para que as instruções para este cenário funcionem, é necessário o seguinte:

|Requisito|Se precisar de mais informações|
|---------------|--------------------------------|
|O Azure Rights Management está ativado|[Activating Azure Rights Management (Ativar o Azure Rights Management – em inglês)](https://technet.microsoft.com/library/jj658941.aspx)|
|Sincronizou as suas contas de utilizador do Active Directory no local com o Azure Active Directory ou o Office 365, incluindo o respetivo endereço de e-mail. Isto é necessário para todos os utilizadores que possam necessitar de aceder a ficheiros depois de estarem protegidos pela FCI e pelo Azure Rights Management.|[Preparar para o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Um dos seguintes:<br /><br />- Para utilizar um modelo predefinido para todos os utilizadores: o modelo predefinido não está arquivado, &lt;nome da organização&gt; – Confidencial<br /><br />- Para utilizar um modelo personalizado para utilizadores específicos: criou e publicou este modelo personalizado|[Configurar modelos personalizados para o Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|A aplicação de partilha Rights Management está implementada nos computadores dos utilizadores que executam o Windows|[Implementação automática da aplicação de partilha Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|Transferiu a ferramenta de Proteção RMS e configurou os pré-requisitos do Azure RMS|Para obter instruções para transferir a ferramenta e os pré-requisitos: [Cmdlets de Proteção RMS](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />Para configurar os pré-requisitos adicionais do Azure RMS, tal como a conta do principal de serviço: [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### Configurar um servidor de ficheiros para proteger todos os ficheiros ao utilizar o Azure RMS e o Gestor de Recursos do Servidor de Ficheiros com Infraestrutura de Classificação de Ficheiros

1.  Inicie uma sessão do Windows PowerShell. Não é necessário executar esta sessão como administrador.

2.  Efetue a autenticação no Azure RMS:

    ```
    Set-RMSServerAuthentication
    ```
    Quando lhe for pedido, forneça os valores da conta do principal de serviço que criou como pré-requisito dos cmdlets de Proteção RMS.

3.  Execute o seguinte para identificar o ID do modelo que será utilizado para proteger os ficheiros:

    ```
    Get-RMSTemplate
    ```
    Para utilizar o modelo predefinido que restringe o acesso a todos os funcionários com todos os direitos de utilização, procure o nome do modelo da **&lt;nome da organização&gt; – Confidencial**. Por exemplo, **VanArsdel, Ltd – Confidencial**.

4.  Siga as instruções passo a passo disponíveis em [Proteção RMS com Infraestrutura de Classificação de Ficheiros (FCI) do Windows Server](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx).

    Estas instruções incluem um script do Windows PowerShell que deve especificar para ser executado como um executável personalizado no Gestor de Recursos do Servidor de Ficheiros. As instruções também incluem como verificar se os ficheiros estão protegidos pelo Azure Rights Management.

## Instruções da documentação do utilizador
Se os ficheiros que está a proteger forem apenas ficheiros do Office, poderá não ter de fornecer aos utilizadores quaisquer instruções sobre os ficheiros protegidos. Quando os utilizadores autorizados abrem estes documentos, estes abrem no Office como habitualmente. A única diferença é que poderá ser solicitado aos utilizadores que se autentiquem e, provavelmente, estes verão uma barra de informações na parte superior do documento que os informa de que o documento está protegido.

Se os ficheiros protegidos tiverem uma extensão de nome de ficheiro **.ppdf** ou forem um ficheiro de texto ou de imagem protegido (por exemplo, se tiverem uma extensão de nome de ficheiro **.ptxt** ou **.pjpg**), esses ficheiros são agora só de leitura e não podem ser editados. Os utilizadores podem visualizá-los ao utilizar o visualizador da aplicação de partilha RMS, que é carregado automaticamente para estes tipos de ficheiro. Estes ficheiros estão protegidos nativamente pelo Azure RMS e aplicam todas as definições de política do modelo que aplicou, à exceção dos direitos de utilização, porque o próprio ficheiro é só de leitura. A menos que saiba que irá proteger estes tipos de ficheiro, é pouco provável que sejam necessárias instruções de utilizador para este cenário. No entanto, avise o suporte técnico de que poderá ser necessário explicar aos utilizadores por que razão não é possível editar estes ficheiros.

Se os ficheiros protegidos tiverem uma extensão **.pfile**, os utilizadores podem ver os ficheiros, mas têm de os guardar com o respetivo nome do ficheiro original (remova a extensão de nome de ficheiro .pfile) se pretenderem editá-los e guardar as alterações. Estes ficheiros estão protegidos genericamente pelo Azure RMS e não podem impor os direitos de utilização do modelo que aplicou, o que significa que a proteção deixa de existir se o ficheiro for guardado com um novo nome. Este cenário requer instruções para os utilizadores.

Utilizando o modelo seguinte, copie e cole as instruções para os utilizadores finais para que estes saibam como editar ficheiros protegidos genericamente. Efetue estas alterações para refletir o seu ambiente:

-   Substitua *&lt;tipo de ficheiro&gt;* e *&lt;partilha de servidor de ficheiros&gt;* pelo tipo de ficheiro que será protegido genericamente e o nome da partilha de servidor de ficheiros.

-   Substitua *&lt;nome da organização&gt;* pelo nome da sua organização, conforme apresentado nos seus modelos predefinidos do Azure Rights Management.

-   Substitua *&lt;nome da organização&gt;* pelo nome da sua organização.

-   Substitua *&lt;Instruções para guardar o ficheiro e remover a extensão .pfile&gt;* por instruções específicas da aplicação para este tipo de ficheiro.

-   Substitua os detalhes de contacto por instruções sobre como os utilizadores podem contactar o suporte técnico, tais como uma ligação para um site, um endereço de e-mail ou um número de telefone.

-   Efetue quaisquer modificações adicionais que pretenda a este conjunto de instruções e, em seguida, envie-o aos utilizadores.

A documentação de exemplo mostra que aspeto estas instruções poderão ter para os utilizadores depois das personalizações.

![Modelo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_UsersBanner.png)

### Como editar &lt;tipo de ficheiro&gt; na &lt;partilha de servidor de ficheiros&gt;

1.  Faça duplo clique no ficheiro para o abrir. Poderão ser-lhe pedidas as credenciais.

2.  Será apresentada uma caixa de diálogo **ficheiro protegido** da aplicação de partilha Microsoft Rights Management, que indica que é esperado que respeite as permissões da **&lt;nome da organização&gt; – Confidencial**. Isto significa que não deve partilhar este documento com outras pessoas se estas não trabalharem para a &lt;nome da organização&gt;.

3.  Clique em **Abrir**.

4.  Para editar o ficheiro, guarde-o primeiro e remova a extensão .pfile:

    -   &lt;Instruções para guardar o ficheiro e remover a extensão .pfile&gt;

5.  Agora pode editar e guardar o ficheiro como habitualmente.

Os ficheiros serão protegidos novamente de forma periódica. Esta operação volta a adicionar a extensão de nome de ficheiro .pfile, pelo que terá de repetir estes passos.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Ver e utilizar ficheiros que foram protegidos](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contactar o suporte técnico:

    -   *&lt;detalhes de contacto&gt;*

### Exemplo de documentação do utilizador personalizada
![Exemplo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Como editar desenhos CAD a partir da partilha ProjectNextGen

1.  Faça duplo clique no ficheiro para o abrir. Poderão ser-lhe pedidas as credenciais.

2.  Será apresentada uma caixa de diálogo **ficheiro protegido** da aplicação de partilha Microsoft Rights Management, o que indica que é esperado que respeite as permissões de **VanArsdel, Ltd – Confidencial**. Isto significa que não deve partilhar este documento com outras pessoas se estas não trabalharem para a VanArsdel, Ltd.

3.  Clique em **Abrir**.

4.  Para editar o ficheiro, guarde-o primeiro e remova a extensão .pfile:

    -   **Ficheiro** &gt; **Guardar como**

    -   Elimine **.pfile** do fim do nome de ficheiro e clique em **OK**.

5.  Agora pode editar e guardar o ficheiro como habitualmente.

Os ficheiros serão protegidos novamente de forma periódica. Esta operação volta a adicionar a extensão de nome de ficheiro .pfile, pelo que terá de repetir estes passos.

**Precisa de ajuda?**

-   Para obter informações adicionais:

    -   [Ver e utilizar ficheiros que foram protegidos](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contacte o suporte técnico: helpdesk@vanarsdelltd.com




<!--HONumber=Jun16_HO4-->


