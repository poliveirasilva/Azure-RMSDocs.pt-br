---
title: Servidor do AD RMS | Azure RMS
description: "O componente de servidor do Rights Management Services (RMS) é implementado por um conjunto de serviços Web executados nos Serviços de Informações da Internet da Microsoft."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 56d0538243af49580f24c701ad5097b30f3059b0
ms.openlocfilehash: 2b7c99e3adafde7140d7997364ec2643ba79a2ac


---

# Servidor

Este tópico descreve o a finalidade e as funções do Servidor RMS para Azure e Windows Server.

**Azure RMS** – para obter mais informações sobre como usar o serviço do Azure Rights Management, consulte [Habilitar seu aplicativo de serviço para trabalhar com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md).

> [!IMPORTANT] 
> Recomendamos que você desenvolva e teste seu aplicativo usando o Azure RMS.

**Windows Server** – para servidores RMS locais, começando com o Windows Server 2008, você pode instalar e configurar o serviço RMS adicionando-o como uma função. Para instalar o serviço em sistemas operacionais anteriores, baixe-o do Centro de Download da Microsoft em [Microsoft Windows Rights Management Services com Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909).

Dos muitos serviços Web instalados, os seguintes são importantes para o desenvolvimento de aplicativos para Servidor RMS no Windows Server.

| Serviço | Descrição |
|---------|-------------|
| Administração | Hospeda o site de administração que permite gerenciar o RMS. O serviço é executado em servidores de certificação raiz e servidores de licenciamento. Você pode usar a API de Scripts do Active Directory Rights Management Services para escrever scripts de administração.|
| Certificação de conta |Cria certificados de computador que identificam computadores na hierarquia de certificados RMS e certificados da conta de direitos que associam usuários a computadores específicos. Para obter mais informações, consulte Ativando um usuário e Ativando um computador.<p><p>Esse serviço é executado no servidor de certificação raiz. |
|Licenciamento | Publica uma *licença de usuário final*. O serviço é executado em servidores de certificação raiz e servidores de licenciamento.|
|Publicando | Cria um *licença de publicação* que define as políticas que podem ser enumeradas em uma licença do usuário final. Para obter mais informações, consulte [Criando uma licença de publicação](https://msdn.microsoft.com/library/Aa362355).<p><p>O serviço é executado em servidores de certificação raiz e servidores de licenciamento.|
|Pré-certificação | Permite que um servidor solicite um *certificado de conta de direitos* em nome de um usuário. O serviço é executado em servidores de certificação raiz e servidores de licenciamento.|
|Localizador de serviço | Fornece a URL da certificação de conta e dos serviços de licenciamento e publicação ao Active Directory para que possam ser descobertos por clientes RMS. O serviço é executado em servidores de certificação raiz e servidores de licenciamento.|

## Tópicos relacionados ##
* [Visão geral](ad-rms-overview.md)
* [Serviços de Informações da Internet da Microsoft](http://www.iis.net/overview)
* [Habilite seu aplicativo de serviço a operar com RMS baseado em nuvem](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services com Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [API de script do Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Ativando um computador](https://msdn.microsoft.com/library/Cc530377)
* [Ativando um usuário](https://msdn.microsoft.com/library/Cc530378)
* [Criando uma licença de emissão](https://msdn.microsoft.com/library/Aa362355)

 

 



<!--HONumber=Jun16_HO4-->


