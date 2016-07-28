---
title: "Alterar permissões nos arquivos que foram protegidos pelo Rights Management | Azure RMS"
description: "Quando um arquivo foi protegido pelo Rights Management, você pode alterar as permissões protegendo-o novamente e, em seguida, especificando todos os usuários que devem ter acesso a ele e quais permissões deseja conceder a eles."
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5ac121b3-d7a0-40e4-8fe7-90bf4cf796f1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 51050497fe128d94e069d0ac010435bea5623af2
ms.openlocfilehash: 985d3d2f1151b50fcde8f8bb916e984e1de71b00


---

# Alterar permissões nos arquivos que foram protegidos pelo Rights Management

*Aplica-se a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 com SP1, Windows 8, Windows 8.1*

Quando um arquivo foi protegido pelo Rights Management, você pode alterar as permissões protegendo-o novamente e, em seguida, especificando todos os usuários que devem ter acesso a ele e quais permissões deseja conceder a eles.

> [!IMPORTANT]
> Essa não é uma alteração incremental, mas uma substituição completa. Você está efetivamente protegendo novamente o arquivo com o conjunto de permissões completo desejado.
> 
>  Por exemplo, se um arquivo estiver protegido, de modo que somente as pessoas do departamento de Marketing possam abri-lo e você desejar que as pessoas no departamento de Vendas também possam abri-lo, será necessário proteger o arquivo novamente para que os departamentos de Vendas e de Marketing possam abri-lo.
>
> Da mesma forma, se você quiser adicionar ou remover uma permissão, não será possível apenas especificar a permissão a ser adicionada ou removida, mas será necessário especificar todas as permissões que você deseja que as pessoas especificadas tenham.

Se você for o proprietário do arquivo que deseja proteger novamente (por exemplo, você o protegeu originalmente usando o aplicativo de compartilhamento), automaticamente terá as permissões para proteger o arquivo novamente. Se você não for o proprietário, poderá ou não ter permissões para proteger o arquivo novamente, dependendo das permissões que o arquivo protegido tem no momento. 

Por exemplo, se outra pessoa protegeu o arquivo usando o aplicativo de compartilhamento do Rights Management e especificou um grupo ao qual você pertence e **Coproprietário** como a permissão personalizada, você poderá proteger o arquivo novamente. No entanto, se ela não especificou seu nome ou um grupo ao qual você pertence, ou se ela selecionou **Revisor – Exibir e Editar** ou um modelo que não permite a remoção de permissões, você não poderá proteger o arquivo novamente. A maneira mais fácil de descobrir é tentar proteger o arquivo novamente.

Se você quiser remover completamente todas as permissões para que o arquivo não esteja mais protegido, consulte [Remover a proteção de um arquivo](sharing-app-remove-protection.md).

## Para proteger novamente um arquivo in-loco

1.  No Explorador de arquivos, selecione um arquivo para proteger. Clique com o botão direito do mouse, selecione **Proteger com RMS** e, em seguida, selecione **Proteger in-loco**. Por exemplo:

    ![Opção de menu Proteger in-loco](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Se você não vir a opção **Proteger com RMS** , é provável que o aplicativo RMS sharing não esteja instalado no seu computador ou que o computador tenha de ser reiniciado para concluir a instalação. Para obter mais informações sobre como instalar o aplicativo RMS sharing, consulte [Baixar e instalar o aplicativo de compartilhamento Rights Management](install-sharing-app.md).

2.  Realize um dos seguintes procedimentos:

    -   Selecione um modelo de política: essas são permissões predefinidas que normalmente restringem o acesso e o uso para as pessoas em sua organização. Por exemplo, se o nome da sua organização é “Contoso, Ltd”, você deverá encontrar **Contoso, Ltd - Somente Exibição Confidencial**. Se esta for a primeira vez que protege um arquivo neste computador, você primeiro precisará selecionar **Proteção definida pela empresa** para baixar os modelos.

        Da próxima vez que você clicar na opção **Proteger in-loco**, você verá até 10 modelos dentre os quais escolher. Se houver mais de 10 modelos disponíveis e o que você quiser não for exibido, clique em **Proteção Definida pela Empresa** para baixar e ver todos os modelos.

        Quando seleciona um modelo de política, você também pode proteger vários arquivos e uma pasta. Quando você seleciona uma pasta, todos os arquivos nessa pasta serão automaticamente selecionados para proteção, mas novos arquivos criados nessa pasta não serão automaticamente protegidos.

    -   Selecione **Permissões personalizadas**: escolha esta opção se os modelos não fornecerem o nível de proteção que você precisa ou se você deseja definir explicitamente as opções de proteção por conta própria. Especifique as opções que você deseja para esse arquivo na [caixa de diálogo Adicionar Proteção](sharing-app-dialog-box.md) e, em seguida, clique em **Aplicar**.

3. Se você não tiver permissões para proteger o arquivo novamente, você verá uma mensagem **Unable to protect content** (Não foi possível proteger o conteúdo), com o endereço de email da pessoa com quem entrar em contato (o proprietário do documento) para que ela possa alterar as permissões para você.

    Se você tiver as permissões para proteger o arquivo novamente, poderá ver rapidamente uma caixa de diálogo para informar que o arquivo está sendo protegido e, em seguida, o foco retorna para o Explorador de Arquivos. Os arquivos selecionados agora estão protegidos com suas alterações. 

> [!NOTE]
> Antes de ser possível proteger o arquivo novamente, o RMS precisará primeiro confirmar que você está autorizado a realizar essa ação para esse arquivo, o que é feito através da verificação de seu nome de usuário e senha. Em alguns casos, isto pode estar em cache e você não verá um prompt solicitando suas credenciais. Em outros casos, será solicitado que você forneça suas credenciais.
>
> Se a sua organização não usa o Azure Rights Management (Azure RMS) ou o AD RMS, você pode se registrar para obter uma conta gratuita que aceitará as suas credenciais para que possa usar arquivos protegidos por RMS:
>
> -   Para se registrar para esta conta, clique no link de registro do [RMS para pessoas físicas](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Ao se registrar, use seu endereço de email da empresa em vez de um endereço de email pessoal. Se você estiver se registrando porque recebeu por email um anexo protegido, use o mesmo endereço de email no qual a mensagem foi recebida.
> -   Para saber mais, confira [RMS para pessoas físicas e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## Para proteger novamente um arquivo enviado por email

Se você quiser alterar as permissões para um arquivo que você enviou por email:

- **Para permitir que mais pessoas leiam o arquivo**: envie o email para elas, seguindo as instruções em [Proteger um arquivo que você compartilha por email](sharing-app-protect-by-email.md).

- **Para alterar as permissões para o arquivo**: envie o arquivo por email novamente, seguindo as instruções em [Proteger um arquivo que você compartilha por email](sharing-app-protect-by-email.md) e selecione as novas permissões desejadas. 

    Como você não pode remover as permissões anteriores no arquivo originalmente enviado por email, apenas as substitua pela nova versão. Considere revogar o arquivo enviado por email anteriormente para que os destinatários não possam mais abrir aquela versão do documento. A revogação será apropriada se você precisar tornar as permissões mais restritivas (por exemplo, remover as pessoas que não devem ter acesso ao arquivo ou não devem mais ser capazes de editá-lo).

    Para revogar um arquivo enviado por email, consulte [Rastrear e revogar seus documentos](sharing-app-track-revoke.md).


## Exemplos e outras instruções
Para obter exemplos de como você pode usar o aplicativo Rights Management sharing e instruções, consulte as seguintes seções do guia de usuário do aplicativo Rights Management sharing:

-   [Exemplos de uso do aplicativo RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [O que você deseja fazer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## Consulte também
[Guia do usuário do aplicativo de compartilhamento Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jul16_HO3-->


