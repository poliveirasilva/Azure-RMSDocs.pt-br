---
title: "Cenário – Configurar pastas de trabalho para proteção persistente | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1f189345-a69e-4bf5-8a45-eb0fe5bb542b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: 35ad445e229eac3feeca5522a41b9e3b25fd1180


---

# Cenário – Configurar pastas de trabalho para proteção persistente

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação de apoio do utilizador utilizam o Azure Rights Management para aplicar proteção persistente aos documentos do Office contidos em [Pastas de Trabalho](https://technet.microsoft.com/library/dn265974.aspx). As Pastas de Trabalho utilizam um serviço de função para servidores de ficheiros que utilizam o Windows Server que disponibiliza uma forma consistente de os utilizadores acederem aos seus ficheiros de trabalho a partir dos respetivos PCs e dispositivos. Apesar de as Pastas de Trabalho fornecerem a sua própria encriptação para proteger os ficheiros, esta proteção deixa de existir se os ficheiros forem movidos para fora do ambiente das Pastas de Trabalho. Por exemplo, os utilizadores copiam os ficheiros sincronizados e guardam-nos num local que não é controlado pelo seu departamento de TI ou os ficheiros são enviados para terceiros por e-mail.

A proteção adicional fornecida pelo Azure Rights Management ajuda a evitar a perda acidental de dados, evitando que os ficheiros sejam vistos por pessoas externas à sua organização. Para tal, pode utilizar um dos modelos de política de direitos predefinidos e incorporados. No entanto, antes de implementar este cenário, tenha em atenção que os utilizadores poderão precisar de partilhar legitimamente um destes ficheiros com pessoas externas à organização. Por exemplo, depois de trabalharem no rascunho de uma lista de preços, os utilizadores enviam e-mails com a versão final para os respetivos clientes noutras organizações. Se utilizassem o modelo de Gestão de Direitos predefinido para Pastas de Trabalho, os clientes das outras organizações não conseguiriam ler esse documento enviado por e-mail. Para cumprir este requisito, pode criar um modelo personalizado que permite que os utilizadores apliquem uma nova política de direitos ao ficheiro, a qual irá substituir a restrição original de todos os funcionários pelas pessoas especificadas no e-mail.

> [!NOTE]
> Quando utiliza o modelo personalizado indicado neste cenário, apesar de os utilizadores poderem partilhar intencionalmente ficheiros com pessoas que não definiu no modelo, a proteção adicional que está a aplicar com o Azure Rights Management proporciona diversos benefícios. Esta proteção adicional evita a perda acidental de dados, caso os conteúdos sejam movidos para fora do limite das Pastas de Trabalho, dado que os conteúdos permanecem protegidos contra utilizadores não autorizados, quer os conteúdos estejam inativos, quer tenham sido transmitidos. Por exemplo, um utilizador perde um dispositivo que está a utilizar as Pastas de Trabalho, este dispositivo é roubado ou os conteúdos sincronizados com e a partir deste dispositivo são transferidos através de uma infraestrutura insegura.
> 
> Se um utilizador partilhar os conteúdos com alguém de outra organização através da funcionalidade Partilhar Protegido da aplicação de partilha Rights Management, esse utilizador substitui a proteção original pela sua própria política de proteção. Por conseguinte, os conteúdos continuam a estar protegidos contra acessos não autorizados e apenas as pessoas especificadas pelo utilizador poderão aceder aos conteúdos.

Pode aplicar esta proteção persistente a todos os documentos do Office nas Pastas de Trabalho dos utilizadores ou apenas em ficheiros que contêm dados confidenciais ou de elevado impacto comercial.

As instruções aplicam-se às seguintes circunstâncias:

-   Os ficheiros da Pasta de Trabalho que pretende proteger com proteção persistente são ficheiros do Office. Estes ficheiros podem ser protegidos nativamente pelo Azure Rights Management e não alteram a respetiva extensão de nome de ficheiro nem precisam de um fluxo de trabalho diferente para os abrir.

-   Quer aplicar a proteção persistente a todos os ficheiros do Office nas Pastas de Trabalho dos utilizadores ou a determinados ficheiros que tenham sido identificados através da Infraestrutura de Classificação de Ficheiros a partir do Gestor de Recursos do Servidor de Ficheiros no Windows Server.

-   Caso os ficheiros tenham de ser partilhados com pessoas que não estão especificadas no modelo de política de direitos (por exemplo, utilizadores de outra organização), os utilizadores têm de aplicar uma nova política de direitos para substituir a proteção da política de direitos original.

## Instruções de implementação
![Instruções do administrador para a Implementação Rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Certifique-se de que os seguintes requisitos são cumpridos e, em seguida, siga as instruções dos procedimentos de suporte antes de avançar para a documentação do utilizador.

## Requisitos para este cenário
Para que as instruções para este cenário funcionem, é necessário o seguinte:

|Requisito|Se precisar de mais informações|
|---------------|--------------------------------|
|O Azure Rights Management está ativado|[Activating Azure Rights Management (Ativar o Azure Rights Management – em inglês)](https://technet.microsoft.com/library/jj658941.aspx)|
|Sincronizou as suas contas de utilizador do Active Directory no local com o Azure Active Directory ou o Office 365, incluindo os respetivos endereços de e-mail. Isto é necessário para todos os utilizadores que utilizam Pastas de Trabalho.|[Preparing for Azure Rights Management (Preparar para o Azure Rights Management – em inglês)](https://technet.microsoft.com/library/jj585029.aspx)|
|Um dos seguintes:<br /><br />- Para utilizar um modelo predefinido para todos os utilizadores que não permita que os utilizadores apliquem uma nova política de direitos: o modelo predefinido não está arquivado, **&lt;nome da organização&gt; – Confidencial**<br /><br />- Para utilizar um modelo personalizado adequado para os utilizadores aplicarem uma nova política de direitos: utilize as instruções que se seguem para criar um modelo personalizado|[Configurar modelos personalizados para o Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|O conector Rights Management está instalado, autorizado para o computador Windows Server e configurado para a função **Servidor FCI**.|[Deploying the Azure Rights Management connector (Implementar o conector Azure Rights Management – em inglês)](https://technet.microsoft.com/library/dn375964.aspx)|
|A aplicação de partilha Rights Management está implementada nos computadores dos utilizadores que utilizam o Windows|[Automatic deployment for the Microsoft Rights Management sharing application (Implementação automática da aplicação de partilha Microsoft Rights Management – em inglês)](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|

### Configurar o modelo de política de direitos personalizado para que os utilizadores possam partilhar ficheiros de Pastas de Trabalho fora da organização

1.  Inicie sessão no portal clássico do Azure e navegue para os modelos do Azure Rights Management.

2.  Copie o modelo **&lt;nome da organização&gt; – Confidencial** e forneça um nome e uma descrição para este cenário de Pastas de Trabalho. Sugerimos o seguinte:

    -   Nome: **Conteúdos protegidos por Pastas de Trabalho**

    -   Descrição: **Estes conteúdos estão protegidos por Pastas de Trabalho e a sua utilização está restrita aos funcionários da empresa. Para partilhar estes conteúdos com pessoas externas à organização, anexe o documento a uma mensagem de e-mail e utilize a função Partilhar Protegido.**

3.  Na página **DIREITOS**:

    -   Altere os direitos existentes de **Personalizado** para **Coproprietário**.

4.  Na página **CONFIGURAR**:

    -   Certifique-se de que o **ESTADO** está definido para **PUBLICAR**

    -   Para o **nome e descrição**, elimine as entradas dos idiomas que não utiliza. Para os idiomas que utiliza, atualize o **NOME** e a **DESCRIÇÃO** para que correspondam ao nome e à descrição que deu a este modelo, utilizando o idioma especificado.

5.  Guarde o modelo.

### Configurar Pastas de Trabalho para aplicar proteção persistente a ficheiros do Office

1.  Implemente Pastas de Trabalho para os seus utilizadores, para que os ficheiros guardados localmente sejam sincronizados com uma pasta de servidor de ficheiros. Esta ação é conhecida como *partilha de sincronização*. A partilha de sincronização no servidor de ficheiros não pode estar no mesmo servidor que executa o conector Rights Management.

    Esta solução precisa do serviço de função de Pastas de Trabalho no Gestor de Servidor, para a função Serviços de Ficheiros e Armazenamento. O servidor de ficheiros tem de executar o Windows Server 2012 R2 ou uma versão posterior, podendo, além disso, estar no local ou numa máquina virtual no Azure. Para mais informações sobre as Pastas de Trabalho, consulte [Descrição Geral das Pastas de Trabalho](https://technet.microsoft.com/library/dn265974.aspx).

    Para obter instruções de implementação, consulte [Implementar Pastas de Trabalho](https://technet.microsoft.com/library/dn528861.aspx). Certifique-se de que seleciona a encriptação incorporada (a opção **Encriptar Pastas de Trabalho**), que será aplicada juntamente com a encriptação do Azure Rights Management. Além disso:

    -   Quando vincular o certificado SSL no servidor de sincronização (passo 4): utilize o comando netsh (em vez da consola de gestão do IIS) para vincular o certificado à interface de HTTPS do Site Predefinido.

    -   Para evitar que os utilizadores obtenham o erro de configuração de Pastas de Trabalho **Ocorreu um problema ao aplicar as políticas de segurança** e a necessidade de serem um administrador local nos respetivos computadores associados a um domínio, utilize o cmdlet [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) com o parâmetro PasswordAutolockExcludeDomain e especifique os nomes de domínio nos quais estes computadores residem (por exemplo, contoso.com).

2.  Para concluir a configuração do conector Rights Management:

    1.  Utilize o Gestor de Recursos do Servidor de Ficheiros para criar uma tarefa de gestão de ficheiros que identifique a pasta de partilha de sincronização como o âmbito.

    2.  Para a ação, selecione **Encriptação RMS** e selecione um modelo:

        -   Se não criou um modelo personalizado porque não quer que os utilizadores possam partilhar ficheiros com pessoas externas à organização, selecione o nome do modelo de **&lt;nome da organização&gt; – Confidencial**. Por exemplo, **VanArsdel, Ltd – Confidencial**.

        -   Se tiver criado um modelo personalizado com base nas instruções anteriores, selecione este modelo. Por exemplo, **Conteúdos protegidos por Pastas de Trabalho**.

    3.  Especifique um momento que permita despender bastante tempo para a encriptação de todos os ficheiros do Office através do Azure Rights Management e selecione a opção **Executar continuamente em ficheiros novos**.

3.  Para testar manualmente esta configuração, certifique-se de que a pasta contém alguns ficheiros do Office e, em seguida, utilize a opção **Executar Tarefa de Gestão de Ficheiros Agora** e selecione **Aguardar conclusão da tarefa**.

    Aguarde que a caixa de diálogo **A Executar Tarefa de Gestão de Ficheiros** seja fechada e, em seguida, veja os resultados no relatório que é automaticamente apresentado. Deverá ver o número de ficheiros que estão na pasta selecionada no campo **Ficheiros**. Confirme que os ficheiros na sua pasta selecionada estão agora protegidos pelo Azure Rights Management. Por exemplo, abra um ficheiro e confirme que vê a faixa de informações na parte superior do documento, que contém o nome e a descrição do modelo de Gestão de Direitos.

4.  Se decidiu proteger apenas determinados ficheiros através da Infraestrutura de Classificação de Ficheiros, configure a sua agenda e regra de classificação e, em seguida, modifique a tarefa de gestão de ficheiros para incluir esta propriedade de classificação como condição.

## Instruções da documentação do utilizador
Se não for necessário partilhar os ficheiros que está a proteger através do Azure Rights Management com pessoas externas à sua organização, poderá fornecer aos utilizadores apenas as instruções sobre como utilizar as Pastas de Trabalho. Quando os utilizadores abrem os ficheiros que estão protegidos pelo Azure Rights Management e o modelo predefinido, os ficheiros são abertos no Office como habitualmente. A única diferença é que poderá ser pedido aos utilizadores que efetuem a autenticação e estes verão uma barra de informações na parte superior do documento que os informa de que os conteúdos contêm informações de propriedade destinadas apenas a utilizadores internos.

Se tiver configurado o modelo personalizado conforme indicado neste cenário, os utilizadores verão a descrição do modelo na barra de informações: **Estes conteúdos estão protegidos por Pastas de Trabalho e a sua utilização está restrita aos funcionários da empresa. Para partilhar estes conteúdos com pessoas externas à organização, anexe o documento a uma mensagem de e-mail e utilize a função Partilhar Protegido.** Embora esta descrição forneça um resumo de como partilhar o ficheiro fora da organização, os utilizadores provavelmente precisarão de instruções detalhadas para realizar esta ação, especialmente nas primeiras vezes que o fizerem. Para conseguir este cenário, utilize as instruções do administrador e do utilizador final em [Scenario – Share an Office file with users in another organization (Cenário – Partilhar um ficheiro do Office com os utilizadores de outra organização – em inglês)](scenario-share-office-file-externally.md).

> [!TIP]
> Se decidiu não utilizar o modelo personalizado nestas instruções porque não quer que os utilizadores possam partilhar estes ficheiros fora da organização sem supervisão do departamento de TI, informe o suporte técnico, para que, se o requisito de partilha for legítimo, este possa ser satisfeito através do mecanismo mais adequado para a sua empresa. Por exemplo, um [superutilizador](https://technet.microsoft.com/library/mt147272.aspx) poderia aplicar um novo modelo aos conteúdos que conceda direitos de Controlo Total ao utilizador requerente, para que este possa depois utilizar a função Partilhar Protegido.
> 
> Se, após algum tempo, descobrir que existem muitos pedidos deste tipo, pode optar por definir o seu próprio modelo personalizado para este cenário, de forma a conceder a opção de Coproprietário apenas a determinados utilizadores (tais como gestores ou o suporte técnico), ao passo que aos utilizadores padrão é concedida a opção Coautor ou os [direitos](https://technet.microsoft.com/library/mt169423.aspx) que considerar adequados.




<!--HONumber=Jun16_HO4-->


