---
title: "Como ativar o Azure Rights Management no portal clássico do Azure | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/27/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b214d7951820c8cb98c5d6f81af3325597ea72ec
ms.openlocfilehash: 9cde79791e8c2b04d1d7622f5aa69d654a70646e


---

# Como ativar o Azure Rights Management no portal clássico do Azure

*Aplica-se a: Azure Rights Management*


Siga estas instruções se você tiver acesso ao portal do Azure. Por exemplo, você tem uma assinatura do Enterprise Mobility Suite ou a assinatura Premium do Azure Rights Management.

> [!TIP]
> Assista a um vídeo de 2 minutos: [Como ativar o Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Após você ter se inscrito na sua conta do Azure, [entre no Portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=275081). Use uma conta de administrador global, como a conta usada para obter a assinatura que inclui o Azure Rights Management.

2.  No painel esquerdo, clique em **ACTIVE DIRECTORY**.

3.  Na página **active directory** , clique em **RIGHTS MANAGEMENT**.

4.  Selecione o diretório a gerenciar para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique em **ATIVAR** e confirme sua ação.

    > [!NOTE]
    >Caso você veja um erro de ativação, pode ser porque seu plano de serviço ou versão do produto não inclui [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].
    >
    >Use as informações em [Assinaturas de nuvem com suporte para Azure RMS](../get-started/requirements-subscriptions.md) para confirmar o suporte para RMS. Para obter ajuda com esse problema, envie uma mensagem de email para [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


O **STATUS do RIGHTS MANAGEMENT** agora deve exibir **Ativo** e a opção **ATIVAR** é substituída por **DESATIVAR**.

## Valores e descrições de status do Rights Management no Portal clássico do Azure
Além do status **ATIVO** , que indica que o serviço de gerenciamento de direitos está habilitado e pronto para uso, você também poderá ver **Inativo**, **Indisponível**, ou **Não Autorizado**.

|Valor do status|Descrição|
|----------------|---------------|
|**Ativo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está habilitado e pronto para usar.|
|**Inativo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está desabilitado e deve ser ativado antes de sua organização proteger os arquivos.|
|**Indisponível**|O [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] serviço está fora de funcionamento. Tente novamente mais tarde.|
|**Não Autorizado**|Você não tem permissão para ver o status do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] serviço. Por exemplo, sua conta está bloqueada ou você não é o administrador global do locatário selecionado.|

## Próximas etapas
Voltar para [Ativando o Azure Rights Management](activate-service.md).


<!--HONumber=Jun16_HO4-->


