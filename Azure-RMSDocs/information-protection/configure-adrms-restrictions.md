---
title: "Restrições de HYOK | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/11/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
translationtype: Human Translation
ms.sourcegitcommit: cfab76a97034b58eec8dfdbdc82cc1037a647d11
ms.openlocfilehash: 95f64c00c28fb52a0bd7d78a997705f7ed515557


---

# Requisitos e restrições de HYOK (Mantenha sua própria chave) para a proteção do AD RMS

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Ao proteger seus documentos e emails mais confidenciais, geralmente, você fará isso aplicando a proteção do Azure Rights Management para ter os seguintes benefícios:

- Nenhuma infraestrutura de servidor necessária, o que torna a solução mais rápida e mais econômica de ser implantada e mantida comparado a uma solução local.

- Compartilhamento mais fácil com parceiros e usuários de outras organizações com a autenticação baseada em nuvem.

- Integração estreita com os serviços do Office 365, como pesquisa, visualizadores Web, exibições dinâmicas, antimalware, Descoberta Eletrônica e Delve.

- Rastreamento de documentos, revogação e notificação por email para documentos confidenciais que você compartilhou.

O Azure RMS protege os documentos e emails de sua organização usando uma chave privada para a organização que é gerenciada pela Microsoft (o padrão) ou gerenciada por você (o cenário BYOK ou “traga sua própria chave”). As informações que você protege com o Azure RMS nunca são enviadas para a nuvem; os documentos e emails protegidos não são armazenados no Azure, a menos que você armazene-os explicitamente lá ou use outro serviço de nuvem que os armazene no Azure. Para obter mais informações sobre as opções de chave de locatário, veja [Planejando e implementando sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md). 

No entanto, alguns clientes poderão precisar proteger documentos e emails selecionados com uma chave que é hospedada localmente. Por exemplo, isso pode ser necessário por motivos regulatórios e de conformidade. 

Essa configuração é às vezes denominada HYOK (“mantenha sua própria chave”) e tem suporte no Azure Information Protection quando você tem uma implantação funcional do AD RMS (Active Directory Rights Management Services) com os requisitos documentados na próxima seção. 

Nesse cenário de HYOK, as políticas de direitos e a chave privada da organização que protege essas políticas são gerenciadas e mantidas localmente, enquanto a política do Azure Information Protection referente à rotulagem e classificação permanece gerenciada e armazenada no Azure. Assim como ocorre com a proteção do Azure RMS, as informações protegidas com o AD RMS nunca são enviadas para a nuvem.

> [!NOTE]
> Use essa configuração somente quando necessário e somente para os documentos e emails que a exigirem. A proteção do AD RMS não oferece os benefícios listados que você obtém quando você usa a proteção do Azure RMS e sua finalidade é a “opacidade de dados a qualquer custo”.

Os usuários não perceberão quando um rótulo usar a proteção do AD RMS em vez da proteção do Azure RMS. Devido às restrições que acompanham a proteção do AD RMS, lembre-se de fornecer uma orientação clara para os casos em que os usuários devem selecionar rótulos que se aplicam à proteção do AD RMS.

## Requisitos do HYOK

Verifique se sua implantação do AD RMS atende aos requisitos a seguir para fornecer a proteção do AD RMS ao Azure Information Protection.

- Configuração do AD RMS:
    
    - Único cluster raiz do AD RMS.
    
    - [Modo Criptográfico 2](https://technet.microsoft.com/library/hh867439.aspx).
    
    - Modelos de direitos configurados.

- A sincronização de diretórios é configurada entre o Active Directory local e o Azure Active Directory e os usuários que usarão a proteção do AD RMS são configurados para logon único.

- Se você compartilha documentos ou emails protegidos pelo AD RMS com outras pessoas fora de sua organização: o AD RMS é configurado para relações de confiança definidas explicitamente em uma relação direta ponto a ponto com outras organizações usando TUDs (domínios de usuário confiável) ou relações de confiança federadas criadas com os Serviços de Federação do Active Directory (AD FS).

- Os usuários têm uma versão do Office que é o Office 2013 Pro Plus com o Service 1 ou Office 2016 Pro Plus, executado no Windows 7 Service Pack 1 ou posterior. Observe que não há suporte para o Office 2010 nem para o Office 2007 neste cenário.

- O [cliente Azure Information Protection](info-protect-client.md) é a versão **1.0.233.0** ou posterior.

> [!IMPORTANT]
> Para atender à alta garantia oferecida por esse cenário, recomendamos que os servidores do AD RMS não estejam localizados na DMZ e que sejam usados somente por computadores bem gerenciados (por exemplo, não dispositivos móveis nem computadores do grupo de trabalho).

Para obter informações sobre implantação e instruções para o AD RMS, confira [Visão geral do Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) na biblioteca do Windows Server. 


## Localizando as informações para especificar a proteção do AD RMS com um rótulo do Azure Information Protection

Quando você configura um rótulo para a proteção do AD RMS, é necessário especificar o GUID do modelo e a URL de licenciamento referente ao cluster do AD RMS. Você pode encontrar esses dois valores no console do Active Directory Rights Management Services:

- Para localizar o GUID do modelo: expanda o cluster e clique em **Modelos de Política de Direitos**. Com base nas informações de **Modelos de Política de Direitos Distribuídos**, você pode copiar o GUID do modelo que deseja usar. Por exemplo: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Para localizar a URL de licenciamento: clique no nome do cluster. Com base nas informações de **Detalhes do Cluster**, copie o valor de **Licenciamento** menos a cadeia de caracteres **/_wmcs/licensing**. Por exemplo: https://rmscluster.contoso.com 
    
    Se você tiver um valor de licenciamento de extranet, bem como um valor de licenciamento de intranet e eles forem diferentes: especifique o valor de extranet somente se você for compartilhar documentos ou emails protegidos com parceiros que você tenha definido com relações de confiança explícitas ponto a ponto. Caso contrário, use o valor de intranet e verifique se todos os computadores cliente que usam a proteção do AD RMS com o Azure Information Protection se conectam usando uma conexão com a intranet (por exemplo, computadores remotos usam uma conexão VPN).

## Próximas etapas

Para obter mais informações sobre esse recurso de visualização, confira o comunicado na postagem no blog, [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/) (Azure Information Protection com HYOK [mantenha sua própria chave]).

Para configurar um rótulo para a proteção do AD RMS, veja [Como configurar um rótulo para aplicar a proteção do Rights Management](configure-policy-protection.md). 



<!--HONumber=Aug16_HO2-->


