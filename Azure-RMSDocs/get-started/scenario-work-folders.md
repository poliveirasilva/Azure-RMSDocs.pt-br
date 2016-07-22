---
title: "Cenário: configurar pastas de trabalho para proteção persistente | Azure RMS"
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

# Cenário: configurar pastas de trabalho para proteção persistente

*Aplica-se a: Azure Rights Management, Office 365*

Esse cenário e a documentação do usuário de suporte usam o Azure Rights Management para aplicar proteção persistente a documentos do Office nas [Pastas de Trabalho](https://technet.microsoft.com/library/dn265974.aspx). As pastas de trabalho usam um serviço de função para servidores de arquivos executando o Windows Server que fornece uma maneira consistente para os usuários acessarem os arquivos de trabalho em seus PCs e dispositivos. Embora as pastas de trabalho forneçam suas próprias criptografias para proteger os arquivos, essa proteção será perdida se os arquivos forem movidos para fora do ambiente Pastas de Trabalho. Por exemplo, usuários copiam os arquivos sincronizados e os salvam em armazenamento que não está sob o controle do seu departamento de TI, ou eles são enviados por email para outras pessoas.

A proteção adicional que o Azure Rights Management fornece ajuda a evitar a perda acidental de dados, impedindo que os arquivos sejam exibidos por pessoas fora da sua organização. Para fazer isso, você pode usar um dos modelos internos de política de direitos padrão. No entanto, antes de implantar este cenário, pondere se os usuários precisam legitimamente compartilhar algum desses arquivos com pessoas fora da organização. Por exemplo, depois de trabalhar em uma lista de preços de rascunho, um usuário envia a versão final para os clientes em outra organização. Quando você usa o modelo de gerenciamento de direitos padrão para Pastas de Trabalho, o cliente na outra organização não é capaz de ler o documento enviado por email. Você pode atender a esse requisito criando um modelo personalizado que permite aos usuários aplicar uma nova política de direitos para o arquivo e substitui a restrição original de todos os funcionários para as pessoas que estão especificadas no email.

> [!NOTE]
> Quando você usa o modelo personalizado documentado para esse cenário, embora os usuários possam compartilhar arquivos com pessoas que você não definiu no modelo intencionalmente, a proteção adicional que você está aplicando com o Azure Rights Management fornece muitos benefícios. Essa proteção adicional impede a perda acidental de dados se o conteúdo é movido para fora do limite das Pastas de Trabalho, pois o conteúdo permanece protegido contra usuários não autorizados independentemente de estar ocioso ou ser transmitido. Por exemplo, um usuário perde um dispositivo que está usando Pastas de Trabalho, esse dispositivo foi roubado ou o conteúdo sincronizado do dispositivo é transferido por uma infraestrutura não protegida.
> 
> Se um usuário compartilhar conteúdo com alguém em outra organização, ao usar a funcionalidade Compartilhar Protegido do aplicativo de compartilhamento Rights Management,o usuário substituirá a proteção original pela sua própria política de proteção. Como resultado, o conteúdo ainda está protegido contra acesso não autorizado e somente as pessoas que o usuário especifica podem acessar o conteúdo.

Você pode aplicar essa proteção persistente a todos os documentos do Office nas Pastas de Trabalho dos usuários ou somente a arquivos que contêm dados confidenciais ou de alto impacto nos negócios.

As instruções são adequadas para o seguinte conjunto de circunstâncias:

-   Os arquivos da Pasta de Trabalho que você deseja proteger com proteção persistente são arquivos do Office. Esses arquivos podem ser protegidos nativamente pelo Azure Right Management e não mudam a extensão de nome de arquivo ou exigem um fluxo de trabalho diferente para abri-los.

-   Você deseja aplicar a proteção persistente a todos os arquivos do Office em Pastas de Trabalho dos usuários ou arquivos escolhidos que foram identificados usando a Infraestrutura de Classificação de Arquivos do Gerenciador de Recursos de Servidor de Arquivos no Windows Server.

-   Para arquivos que devem ser compartilhados com pessoas que não estão especificadas no modelo de política de direitos (por exemplo, usuários em outra organização), os usuários devem aplicar uma nova política de direitos para substituir a proteção de política de direitos original.

## Instruções de implantação
![Instruções do administrador para implantação rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Verifique se os requisitos a seguir foram aplicados e siga as instruções para os procedimentos de suporte antes de ir para a documentação do usuário.

## Requisitos para este cenário
Para que as instruções desse cenário funcionem, deve ser feito o seguinte:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Você sincronizou suas contas de usuário do Active Directory local com o Active Directory do Azure ou o Office 365, incluindo seu endereço de email. Isso é necessário para todos os usuários que usam Pastas de Trabalho.|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Um das seguintes condições:<br /><br />- Para usar um modelo padrão para todos os usuários que não permite que os usuários apliquem uma nova política de direitos: você não arquivou o modelo padrão, **&lt;nome da organização&gt; – Confidencial**<br /><br />- Para usar um modelo personalizado que é adequado para que os usuários apliquem uma nova política de direitos: use as instruções a seguir para criar um modelo personalizado|[Configurando modelos personalizados do Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|O conector do Rights Management está instalado, autorizado para o computador Windows Server e configurado para a função **Servidor FCI**.|[Implantando o conector do Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|O aplicativo Rights Management sharing é implantado nos computadores dos usuários que executam o Windows|[Implantação automática para o aplicativo de compartilhamento Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|

### Configuração do modelo de política de direitos personalizados para que os usuários possam compartilhar arquivos de Pastas de Trabalho fora da organização

1.  Entre no portal clássico do Azure e navegue até os modelos do Azure Rights Management.

2.  Copie o modelo **&lt;nome da organização&gt; - Confidencial** e forneça um nome e uma descrição para esse cenário de Pastas de Trabalho. Sugerimos o seguinte:

    -   Nome: **conteúdo protegido por Pastas de Trabalho**

    -   Descrição: **esse conteúdo é protegido por Pastas de Trabalho e é restrito aos funcionários da empresa. Para compartilhar esse conteúdo com pessoas de fora da organização, anexe o documento a uma mensagem de email e use a função Compartilhar Protegido.**

3.  Na página **DIREITOS**:

    -   Altere as permissões existentes de **Personalizada** para **Coproprietário**.

4.  Na página **CONFIGURAR**:

    -   Verifique se o **STATUS** está definido como **PUBLICAR**

    -   No caso do **nome e da descrição**, exclua as entradas dos idiomas que você não usa. No caso dos idiomas que você usa, atualize o **NOME** e a **DESCRIÇÃO** para que eles correspondam ao nome e à descrição que você deu a esse modelo, usando o idioma especificado.

5.  Salve o modelo.

### Configurando Pastas de Trabalho para aplicar proteção persistente ao arquivo do Office

1.  Implemente Pastas de trabalho para seus usuários a fim de que os arquivos salvos localmente sejam sincronizadas com uma pasta de servidor de arquivo, conhecida como *compartilhamento de sincronização*. O compartilhamento de sincronização no servidor de arquivos não deve ocorrer no mesmo servidor que executa o conector do Rights Management.

    Essa solução requer o serviço de função das Pastas de Trabalho no Gerenciador de Servidores para a função Serviços de Arquivo e Armazenamento. O servidor de arquivos deve estar executando uma versão mínima do Windows Server 2012 R2, e esse servidor pode ser local ou em uma máquina virtual no Azure. Para saber mais sobre Pastas de Trabalho, confira [Visão geral de Pastas de Trabalho](https://technet.microsoft.com/library/dn265974.aspx).

    Para obter instruções de implantação, confira [Implantando Pastas de Trabalho](https://technet.microsoft.com/library/dn528861.aspx). Selecione a criptografia interna (a opção **Criptografar Pastas de Trabalho**), que será aplicada além da criptografia do Azure Rights Management. Além disso:

    -   Quando você associa o certificado SSL ao servidor de sincronização (etapa 4): use o comando netsh (em vez do console de gerenciamento do IIS) para associar o certificado à interface HTTPS do Site da Web padrão.

    -   Para evitar que os usuários recebam o erro de configuração de Pastas de Trabalho **Houve um problema ao aplicar políticas de segurança** e o requisito de que eles devem ser administradores locais em seus computadores de domínio: use o cmdlet [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) com o parâmetro PasswordAutolockExcludeDomain e especifique os nomes de domínio em que esses computadores residem (por exemplo, contoso.com).

2.  Para concluir a configuração do conector do Rights Management:

    1.  Usando o Gerenciador de Recursos de Servidor de Arquivos, crie uma tarefa de gerenciamento de arquivos que identifica a pasta de compartilhamento de sincronização como escopo.

    2.  Para a ação, escolha **criptografia RMS** e selecione um modelo:

        -   Se você não criou um modelo personalizado porque não quer que os usuários possam compartilhar arquivos com outras pessoas fora da organização, selecione o nome do modelo de **&lt;nome da organização&gt; - Confidencial**. Por exemplo, **VanArsdel, Ltd - Confidencial**.

        -   Se você criou um modelo personalizado usando as instruções anteriores, selecione esse modelo. Por exemplo, **Conteúdo protegido por Pastas de Trabalho**.

    3.  Especifique um agendamento que dê tempo suficiente para que todos os arquivos do Office sejam criptografados pelo Azure Rights Management e especifique a opção de **Executar continuamente nos novos arquivos**.

3.  Para testar manualmente essa configuração, verifique se a pasta contém alguns arquivos do Office, use a opção **Executar Tarefa de Gerenciamento de Arquivos Agora** e selecione **Aguardar a conclusão da tarefa**.

    Aguarde até que a caixa de diálogo **Executando Tarefa de Gerenciamento de Arquivo** feche e, em seguida, veja os resultados no relatório exibido automaticamente. Você deve ver o número de arquivos que estão na pasta escolhida no campo **Arquivos** . Confirme que os arquivos na pasta escolhida estão agora protegidos pelo Azure Rights Management. Por exemplo, abra um arquivo e confirme que você vê a faixa de informações na parte superior do documento que exibe o nome e a descrição do modelo do Rights Management.

4.  Se você decidiu proteger arquivos seletivamente usando a Infraestrutura de Classificação de Arquivos, configure sua regra de classificação e o agendamento e modifique a tarefa de gerenciamento de arquivo para incluir essa propriedade de classificação como uma condição.

## Instruções sobre a documentação do usuário
Se os arquivos que está protegendo com o Azure Rights Management não precisam ser compartilhado com pessoas fora da sua organização, você não terá de fornecer aos usuários instruções além daquelas que fornecer para o uso das Pastas de Trabalho. Quando os usuários abrem os arquivos que são protegidos pelo Azure Rights Management e o modelo padrão, os arquivos abrem como de costume no Office; a única diferença é que os usuários podem ter que autenticar e eles verão uma barra de informações na parte superior do documento informando que o conteúdo contém informação proprietária para uso somente dos usuários internos.

Se você tiver configurado o modelo personalizado conforme documentado para esse cenário, os usuários verão a descrição do modelo na barra de informações: **este conteúdo é protegido por Pastas de Trabalho e é restrito aos funcionários da empresa. Para compartilhar esse conteúdo com pessoas de fora da organização, anexe o documento a uma mensagem de email e use a função Compartilhar Protegido.**. Embora essa descrição forneça um resumo de como compartilhar o arquivo fora da organização, os usuários provavelmente precisarão de instruções detalhadas sobre como fazer isso, especialmente nas primeiras vezes. Para dar suporte a esse cenário de acompanhamento, use as instruções do administrador e do usuário final de [Cenário: compartilhar um arquivo do Office com usuários em outra organização](scenario-share-office-file-externally.md).

> [!TIP]
> Se você optou por não usar o modelo personalizado nestas instruções porque não deseja que os usuários possam compartilhem esses arquivos fora da organização sem supervisão do departamento de TI, avise o suporte técnico para que os casos em que a necessidade de compartilhamento seja legítima possam ser atendidos usando o mecanismo mais apropriado para a sua empresa. Por exemplo, alguém que seja um [superusuário](https://technet.microsoft.com/library/mt147272.aspx) poderia aplicar um novo modelo para o conteúdo que concede ao usuário solicitante direitos de controle total, para que esse usuário possa usar a função Compartilhar Protegido
> 
> Após um período de tempo, se você descobrir que há muitas solicitações, poderá decidir definir seu próprio modelo personalizado para esse cenário que concede somente a usuários específicos (como gerentes ou o suporte técnico) a opção Coproprietário, enquanto os usuários padrão recebem de Coautor ou qualquer outro [direito](https://technet.microsoft.com/library/mt169423.aspx) que você entenda ser adequado.




<!--HONumber=Jul16_HO3-->


