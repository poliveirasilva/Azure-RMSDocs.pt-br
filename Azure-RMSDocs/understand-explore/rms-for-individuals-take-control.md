---
title: "Como os administradores podem controlar as contas criadas para o RMS para pessoas físicas | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: df006a27c97884c47c9bb5fb04bfa181a13b7443


---



# Como os administradores podem controlar as contas criadas para o RMS para pessoas físicas

*Aplica-se a: Azure Rights Management*


Se você não deseja converter o RMS de assinatura para pessoas físicas da sua organização em uma assinatura paga, você ainda pode controlar as contas de usuário no diretório do Azure que foi criado para a sua organização das seguintes maneiras:

-   Implemente soluções de integração de diretório para o Azure Active Directory e sua infraestrutura de Serviços de Domínio do Active Directory. É possível sincronizar contas e senhas para que os usuários não precisem criar novas contas para usar o Rights Management, e suas políticas de senha no local serão aplicáveis ​​às novas contas de usuário do Azure. Também é possível sincronizar senhas para que os usuários não precisem se lembrar de uma senha diferente para usar o Rights Management.

-   Você pode impedir que os usuários se inscrevam para usar o Azure Rights Management com a assinatura do RMS para pessoas físicas. Na maioria dos casos, há pouca vantagem em fazer isso, porque os usuários compartilharão arquivos sem proteção (o que poderia colocar sua empresa em risco) ou usarão outro mecanismo de proteção de arquivos que não dá ao departamento de TI a opção de acessar os dados. No entanto, se você quiser impedir que usuários se inscrevam para usar o RMS para pessoas físicas, efetue uma das ações a seguir após assumir a propriedade do diretório da sua organização no Azure:

    -   Impedir todos os usuários de obterem assinaturas de autoatendimento, que inclui o RMS para pessoas físicas.  No momento, não é possível definir isto por serviço; a configuração se aplica a todas as assinaturas do Azure que usam o processo de autoatendimento. Para fazer isso, defina o parâmetro **AllowAdHocSubscriptions** como falso com o cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) do módulo do Windows PowerShell para o Azure Active Directory. Por exemplo, **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   Impedir os usuários de criarem uma nova conta no Azure, o que significa que somente os usuários que já têm uma conta no Azure podem obter assinaturas de autoatendimento, que inclui o RMS para pessoas físicas.  Para fazer isso, defina o parâmetro **AllowEmailVerifiedUsers** como falso com o cmdlet [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) do módulo do Windows PowerShell para o Azure Active Directory. Por exemplo, **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Sincronize sua infraestrutura de serviços de domínio do Active Directory com o Active Directory do Azure. Essa ação impede que novas contas sejam criadas quando os usuários obtêm assinaturas de autoatendimento, como o RMS para pessoas físicas, e você pode excluir ou desativar contas que foram criadas anteriormente no diretório do Azure.

Para controlar as contas de usuário no diretório do Azure ou para impedir que os usuários se inscrevam no RMS para indivíduos, você deve ter uma assinatura do Azure e possuir o diretório. Se você ainda não tiver uma assinatura do Azure, você poderá obtê-la sem custos adicionais. Se um diretório foi criado automaticamente para você durante o processo de autoatendimento, aproprie-se do domínio que foi usado para criá-lo. Se você já possui um diretório no Azure, mas os usuários especificaram um novo domínio que você usa em sua organização, mescle esse domínio em seu diretório existente. Para obter mais informações, consulte as instruções em [O que é a inscrição de autoatendimento para o Azure?](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)


## Próximas etapas

Se os usuários, em vez dos administradores, podem criar suas contas no Azure Active Directory para o RMS para pessoas físicas, como você pode saber se eles fizeram isso?  Consulte [Como saber se os usuários se inscreveram para o RMS para pessoas físicas](rms-for-individuals-identify-sign-up.md).



<!--HONumber=Jun16_HO4-->


