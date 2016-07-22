---
title: "Novidades e notas de versão | Azure RMS"
description: "Descreve as funcionalidades e alterações importantes nesta versão nova do SDK RMS."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: eccc0ba9c13e0c35c8d0c8877ce92f9b99e83835


---

# Novidades e notas de versão

## Novidades
O SDK Microsoft Rights Management 4.2 leva a aplicação RMS a um novo nível de facilidade e flexibilidade. Este tópico descreve as funcionalidades e alterações importantes nesta versão nova do SDK RMS.

-   [Novidades para junho de 2016](#new_for_June_2016)
-   [atualização de dezembro de 2015](#december_2015_update)
-   [Atualização de julho de 2015 – adiciona suporte para a programação em Linux/C++](#july_2015_update_-_adds_support_for_linux___c___development)
-   [Atualização de maio de 2015 – adiciona o controlo de registo](#may_2015_update_-_adds_logging_control)
-   [Atualização de fevereiro de 2015 – adiciona o suporte para aplicações da Loja Windows](#february_2015_update_-_adds_windows_store_application_support)
-   [Atualização de janeiro de 2015 – adiciona o suporte da plataforma WinPhone](#january_2015_update_-_adds_winphone_platform_support)
-   [Atualização de outubro de 2014 – atualizar para o SDK Microsoft RMS 4.1](#october_2014_update_-_upgrade_to_microsoft_rms_sdk_4.1)
-   [Notas de versão](#release-notes)
-   [Perguntas mais frequentes](#frequently_asked_questions)

### Novidades para junho de 2016

- **Suporte para a Autenticação Moderna** - isto proporciona um início de sessão baseado em ADAL (Active Directory Authentication Library) para as aplicações com RMS. Permite funcionalidades de início de sessão como o Multi-Factor Authentication, Fornecedores de Identidade terceiros baseados em SAML com aplicações de cliente, autenticação baseada em smart card e em certificado e remove a necessidade de aplicações com RMS utilizarem o protocolo de autenticação básico.
- **Suporte ao Controlo de Documentos** - os programadores agora podem ativar o controlo de documentos ao proteger um documento nas suas aplicações 
- Melhoramentos de desempenho
- Correções


### atualização de dezembro de 2015

Com esta versão, o SDK RMS para dispositivos está agora na versão 4.2 e adiciona:

-   O controlo de documentos e o RMS apenas online para sistemas operativos Android e iOS/OS X.

    Para obter detalhes e instruções de utilização no iOS/OS X, consulte a classe [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc), que fornece informações de controlo e o método adicional de registo de controlo de documentos [**MSUserPolicy**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msuserpolicy_interface_objc). Existem adições semelhantes para o Android em [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) e [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy).

    Para obter uma descrição detalhada da funcionalidade de controlo de documentos, consulte [**Como: utilizar o controlo de documentos**](how-to-use-document-tracking.md).

-   Um conjunto de métodos síncronos paralelos às versões assíncronas para a API do Android:

    [**Método síncrono CustomProtectedInputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_create_synchronous_method_java)

    [**Método síncrono CustomProtectedOutputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Método síncrono ProtectedFileInputStream.create**](/rights-management/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_synchronous_method)

    [**Método síncrono ProtectedFileOutputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Método síncrono TemplateDescriptor.getTemplates**](/rights-management/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_gettemplates_synchronous_method_java)

    [**Método síncrono UserPolicy.acquire**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_acquire_synchronous_method_java)

    [**Método síncrono UserPolicy.create (PolicyDescriptor…)**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_policydescriptor_______synchronous_method_java)

    [**Método síncrono UserPolicy.create (TempalteDescriptor…)**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_templatedescriptor_______synchronous_method_java)

-   Foi adicionada uma nova classe [**ProtectedBuffer**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedbuffer_class) à API do Android.
-   Atualizações para melhorar a experiência de resolução de problemas e de mensagens de erro.
-   Melhorias de desempenho significativas para operações de criptografia.

### Atualização de julho de 2015 – adiciona suporte para a programação em Linux/C++

Esta versão adiciona o seguinte:

-   SDK RMS 4.1 para plataformas Linux

    Para obter mais informações, consulte [Introdução](get-started.md).

### Atualização de maio de 2015 – adiciona o controlo de registo

Esta versão adiciona o suporte para o seguinte:

-   iOS

    A encriptação e a desencriptação de aplicações podem funcionar independentemente e em paralelo.

    Para obter mais informações, consulte [**MSProtector**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msprotector_class_objc).

    Definições de controlo do nível de registo ativadas.

    Para obter mais informações, consulte [Como: ativar registo de erros e de desempenho](enabling-logging.md)

    Suporte de limpeza da cache adicionado.

    Para obter mais informações, consulte [**MSProtection:resetStateWithCompletionBlock**](/rights-management/sdk/4.2/api/iOS/msprotection#msipcthin2_msprotection_resetstatewithcompletionblock_method_objc).

### Atualização de fevereiro de 2015 – adiciona o suporte para aplicações da Loja Windows

Esta versão adiciona o suporte para aplicações da Loja Windows e fornece paridade funcional com o lançamento para Windows Phone, Android e iOS/OS X do SDK RMS 4.1.

### Atualização de janeiro de 2015 – adiciona o suporte da plataforma WinPhone

Esta versão adiciona o suporte para o sistema operativo Windows Phone e fornece paridade funcional com o lançamento para Android e iOS/OS X do SDK RMS 4.1.

## Atualização de outubro de 2014 – atualizar para o SDK Microsoft RMS 4.1

O lançamento da versão 4.1 do SDK RMS adiciona as seguintes funcionalidades novas para o Google Android e Apple iOS/OS X.

-   Extensões da API do SDK iOS/OS X para o processamento do *consentimento do utilizador*, permitindo a confirmação do utilizador de comportamentos do SDK. Atualmente, o controlo de documentos e o acesso a URLs desconhecidos do serviço AD RMS são os tipos de consentimento suportados.

    Para obter mais informações, consulte, como exemplo, a versão da API do Android da [**interface ConsentCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_consentcallback_interface_java).

-   O iOS 8 e o OS X 10.10 (Yosemite) já são suportados. De igual modo, houve algumas alterações de nomes de propriedades obrigatórias pelo Xcode 6.

    Exemplo: alterou-se MSUserPolicy.name para [**MSUserPolicy.policyName**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_name_property_objc).

## Notas de versão

Esta secção apresenta as informações sobre as versões atuais e anteriores das APIs SDK Microsoft Rights Management 4. x que o programador deve ter em consideração.

**SDK AD RMS 4.1 – Lançamento de Disponibilidade Global para as plataformas iOS/OS X e Android**

-   **Suporte do AD RMS** – os administradores de TI podem utilizar aplicações com suporte RMS em dispositivos móveis com as novas extensões para dispositivos móveis do servidor AD RMS.
-   **Consumo offline** – os utilizadores finais podem aceder a dados protegidos por RMS offline.
-   **Autorização Separada** – os programadores podem utilizar a sua própria biblioteca de autenticação para o Azure RMS e AD RMS (ou utilizar a [Azure AD Authentication Library (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx) recomendada).
-   **IU Separada** – os programadores podem criar a sua interface de utilizador para proteger e consumir documentos protegidos por RMS.
-   **API Reformulada** – os programadores podem agora desfrutar de uma API de encriptação e desencriptação simples e transparente, que fornece uma interface de utilizador e comportamentos de RMS consistentes, com esforços mínimos.

**Comuns a todas as plataformas**

-   As APIs do SDK RMS 4.x não são *seguras para os threads*.

**Android**

-   Quando utilizar uma aplicação de exemplo num dispositivo Amazon® Kindle para ver anexos .ptxt, tem primeiro de transferir o ficheiro antes de o visualizar.

    **Solução** – isto é um problema conhecido e será resolvido mais tarde.

-   Uma aplicação que utilize o SDK pode falhar se forem permitidas várias instâncias.

    **Solução** – certifique-se de que a aplicação não permite chamadas de várias instâncias para a API do Android.

-   Quando utilizo o método [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array, int offset, int length)** com um comprimento diferente do valor *array.length*, não consigo consumir o conteúdo posteriormente utilizando o SDK.

    **Solução** – isto é um problema conhecido. Para o resolver, transmita sempre uma matriz de **bytes \[\]** com o mesmo valor de comprimento que o parâmetro de comprimento ou utilize o método [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array)**.

**iOS e OS X**

-   Existem dois dialetos de português que os nossos SDKs para iOS e OS X suportam. Infelizmente, devido a um erro, de momento, não suportamos a 1ª localização completamente. Devido a este erro, o português não é totalmente suportado. A maior parte do texto é traduzido, mas não a IU.

    1. Português

    2. Português (Portugal)

**Apenas no iOS**

-   O SDK RMS 4.x não mostra o indicador da atividade de rede.

    Este é um comportamento opcional conhecido do iOS, de acordo com as Diretrizes de Interface Humana da Apple.

**Apenas no OS X**

-   O SDK RMS 4.x não mostra o indicador da atividade de rede.

    Este é um comportamento opcional conhecido do OS X, de acordo com as Diretrizes de Interface Humana da Apple.

-   **Solução** – para criar uma aplicação de interface MDI (multiple document interface) através do nosso SDK para OS X, utilize as seguintes orientações.

    Os seguintes métodos não podem ser executados em simultâneo. Para poder monitorizar a conclusão da execução, utilize a abordagem do bloco de conclusão, conforme indicado.

    - [**protectedDataWithProtectedFile**](/rights-management/sdk/4.2/api/iOS/msprotecteddata#msipcthin2_msprotecteddata_protecteddatawithprotectedfile_completionblock_method_objc)
    - [**customProtectedDataWithPolicy**](/rights-management/sdk/4.2/api/iOS/mscustomprotecteddata#msipcthin2_mscustomprotecteddata_customprotecteddatawithpolicy_protecteddata_contentstartposition_contentsize_completionblock_method_objc)



**Nota** As aplicações MDI não são suportadas pela nossa API do iOS.

## Perguntas mais frequentes

**Todas as plataformas**

**P**: não consigo ver uma IU de seleção de **Permissões Personalizadas** no fluxo de trabalho da proteção. Por que motivo?

**R** – isto é um problema conhecido e será resolvido mais tarde.

**P**: de que forma obtenho novos inquilinos organizacionais para experimentar o SDK e as aplicações de exemplo?

**R**: para pedir credenciais para as organizações de teste do Azure AD RMS, envie um e-mail para <rmcstbeta@microsoft.com>.

**P**: não vejo qualquer debate sobre a hierarquia de testes aqui na documentação. Por que motivo?

**R**: não existe qualquer conceito de hierarquia de testes com os novos SDKs AD RMS. Irá sempre trabalhar com a hierarquia de produção.

**P**: na versão 2.1 do SDK RMS, era necessário um manifesto gerado para cada aplicação que implementasse a proteção de informações, isto ainda se mantém para as versões 4.0 e posteriores do SDK?

**R**: não, os manifestos já não são necessários para as versões 3.0 e posteriores do SDK Rights Management.

**Android**

**P**: com que ambientes de desenvolvimento foi o SDK testado?

**R**: Eclipse Juno através da API do Google 15 e superior.

**P**: posso chamar um método de cancelamento cancel() a partir do thread da IU?
**R**: deve chamar cancel() a partir de um thread não IU, pois pode abortar uma ligação de rede.

**iOS**

**P**: que plataformas foram verificadas para o desenvolvimento de SDK?

**R**: Xcode 5.0 com iOS 7 e posterior.

**P**: chamei um método cancel() numa operação; no entanto, ainda obtive uma notificação sobre a conclusão da operação. Por que motivo?

**Um**: nem todas as operações podem ser canceladas, pelo que uma operação de cancelamento é executada da melhor forma possível.

**OS x**

**P**: a estrutura de aplicações de exemplo é adaptada para o Xcode 5, posso trabalhar com o Xcode 4.6?

**R**: o SDK OS X apenas funciona com o Xcode 4.6 e versões posteriores, bem como o OS X 10.8 e versões posteriores.

 

 



<!--HONumber=Jul16_HO2-->


