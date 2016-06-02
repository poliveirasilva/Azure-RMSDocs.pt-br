---
# required metadata

title: Configurando modelos personalizados do Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/23/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurando modelos personalizados do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Depois da [ativação do Azure Rights Management](activate-service.md) (Azure RMS), os usuários podem usar automaticamente dois modelos padrão que facilitam a aplicação de políticas a arquivos confidenciais que restringem o acesso a usuários autorizados em sua organização. Esses dois modelos têm as seguintes restrições de política de direitos:

-   Visualização de somente leitura para o conteúdo protegido

    -   Nome de exibição: **&lt;nome da organização&gt; - Somente exibição confidencial**

    -   Permissão específica: Exibir Conteúdo

-   As permissões de leitura ou modificação do conteúdo protegido

    -   Nome de exibição: **&lt;nome da organização&gt; - Confidencial**

    -   Permissões específicas: Exibir Conteúdo, Salvar Arquivo, Editar Conteúdo, Exibir Direitos Atribuídos, Permitir Macros, Encaminhar, Responder e Responder a Todos

Além disso, o [aplicativo RMS sharing](../rms-client/sharing-app-windows.md) permite que os usuários definam seu próprio conjunto de permissões. E, para o cliente Outlook e Outlook Web Access, os usuários podem selecionar a opção **Não Encaminhar** para mensagens de email.

Para muitas organizações, os modelos padrão podem ser suficientes. Porém, se você quiser criar seus próprios modelos personalizados de política de direitos, isso é possível. Os motivos para criar um modelo personalizado incluem o seguinte:

-   Você quer um modelo para conceder direitos a um subconjunto de usuários na organização, ao invés de todos os usuários.

-   Você deseja que apenas um subconjunto de usuários possa ver e selecionar um modelo (modelo departamental) de aplicativos, e não que todos os usuários da organização possam ver e selecionar o modelo.

-   Você quer definir um direito personalizado para um modelo, como Exibir e Editar, mas não Copiar e Imprimir.

-   Você quer configurar opções adicionais em um modelo que incluem uma data de validade e se o conteúdo pode ser acessado sem uma conexão com a Internet.

Para que os usuários possam selecionar um modelo personalizado que contenha definições como essas, é necessário primeiro criar um modelo personalizado, configurá-lo e depois publicá-lo. Embora provavelmente você venha a exigir apenas alguns modelos, você pode ter um máximo de 500 modelos personalizados salvos no Azure. 

Use as informações a seguir para ajudar a configurar e usar modelos personalizados:

-   [Como criar, configurar e publicar um modelo personalizado](create-template.md)

-   [Como copiar um modelo](copy-template.md)

-   [Como remover (arquivar) modelos](remove-template.md)

-   [Como atualizar modelos para usuários](refresh-templates.md)

-   [Usar o PowerShell para gerenciar modelos](configure-templates-with-powershell.md)




<!--HONumber=May16_HO5-->


