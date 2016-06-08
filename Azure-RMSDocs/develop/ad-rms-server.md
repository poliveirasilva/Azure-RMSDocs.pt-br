---
# required metadata

title: Servidor do AD RMS | Azure RMS
description: O componente de servidor do Rights Management Services (RMS) é implementado por um conjunto de serviços Web executados nos Serviços de Informações da Internet da Microsoft.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Este conteúdo do SDK não é atual. Por um curto período, encontre a [versão atual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) da documentação no MSDN. **

# Servidor do AD RMS
Este tópico descreve o propósito e as funções do servidor do RMS.

O componente de servidor do RMS (Rights Management Services) é implementado por um conjunto de serviços Web executados no IIS ([Serviços de Informações da Internet da Microsoft](http://www.iis.net/overview)). Você também pode usar a implementação baseada em nuvem por meio do RMS no Azure. Para obter mais informações sobre como usar o serviço de Azure Rights Management, consulte [Habilitar seu aplicativo de serviço para trabalhar com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

Para servidores locais, começando com o Windows Server 2008, você pode instalar e configurar o serviço RMS adicionando-o como uma função. Para instalar o serviço em sistemas operacionais anteriores, baixe-o do Centro de Download da Microsoft em [Microsoft Windows Rights Management Services com Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909).

Dos muitos serviços Web instalados, os seguintes são importantes para o desenvolvimento de aplicativos.

**Administração** - hospeda o site de administração que permite gerenciar o RMS. O serviço é executado em servidores de certificação raiz e servidores de licenciamento. Você pode usar o [API Active Directory Rights Management Services scripts](https://msdn.microsoft.com/library/Bb968797) para escrever scripts de administração.

**Certificação de Conta** - cria certificados de computador que identificam computadores na hierarquia de certificados RMS e certificados da conta de direitos que associam usuários a computadores específicos. Para obter mais informações, consulte [Ativando um usuário](https://msdn.microsoft.com/library/Cc530378).

Esse serviço é executado no servidor de certificação raiz.

**Licenciamento** - emite uma licença de usuário final que permite aos usuários finais consumir conteúdo protegido. O serviço é executado em servidores de certificação raiz e servidores de licenciamento.

**Publicação** - gera [Criando uma licença de emissão](https://msdn.microsoft.com/library/Aa362355). O serviço é executado em servidores de certificação raiz e servidores de licenciamento.

**Pré-certificação** - permite que um servidor solicite um certificado de conta de direitos (RAC) em nome de um usuário. Um RAC usa o certificado do computador de ativação do RMS para associar contas de usuário a computadores específicos ou grupos de computadores e é usado para habilitar os consumidores utilizem conteúdo protegido. O serviço é executado em servidores de certificação raiz e servidores de licenciamento.

**Localizador de Serviço** - fornece a URL da certificação de conta e dos serviços de licenciamento e publicação ao Active Directory para que possam ser descobertos por clientes do RMS. O serviço é executado em servidores de certificação raiz e servidores de licenciamento.

 

## Tópicos relacionados ##
* [Visão geral](ad-rms-overview.md)
* [Serviços de Informações da Internet da Microsoft](http://www.iis.net/overview)
* [Habilite seu aplicativo de serviço a operar com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services com Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [API de script do Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Ativando um computador](https://msdn.microsoft.com/library/Cc530377)
* [Ativando um usuário](https://msdn.microsoft.com/library/Cc530378)
* [Criando uma licença de emissão](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Jun16_HO1-->


