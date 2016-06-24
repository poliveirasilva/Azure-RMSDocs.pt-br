---
# required metadata

title: Novidades e notas de versão | Azure RMS
description: Descreve alterações e recursos importantes nesta nova versão do RMS SDK.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Novidades e notas de versão

## Novidades
O Microsoft Rights Management SDK 4.2 leva a habilitação do aplicativo RMS para um novo nível de facilidade e flexibilidade. Este tópico descreve alterações e recursos importantes nesta nova versão do RMS SDK.

-   [Novidades de nossa Atualização de dezembro de 2015](#new_for_our_december_2015_update)
-   [Atualização de julho de 2015 - Acrescenta suporte para Linux/desenvolvimento em C++](#july_2015_update_-_adds_support_for_linux___c___development)
-   [Atualização de maio de 2015 - Acrescenta o controle de registro em log](#may_2015_update_-_adds_logging_control)
-   [Atualização de fevereiro de 2015 - Acrescenta o suporte a aplicativos da Windows Store](#february_2015_update_-_adds_windows_store_application_support)
-   [Atualização de janeiro de 2015 - Acrescenta suporte à plataforma WinPhone](#january_2015_update_-_adds_winphone_platform_support)
-   [Atualização de outubro de 2014 - Atualiza para o Microsoft RMS SDK 4.1](#october_2014_update_-_upgrade_to_microsoft_rms_sdk_4.1)
-   [Notas de versão](#release-notes)
-   [Perguntas frequentes](#frequently_asked_questions)

### Novidades de nossa Atualização de dezembro de 2015

Com esta versão, o RMS SDK para dispositivos está na versão 4.2 e acrescenta:

-   Rastreamento de documentos, somente RMS Online, para sistemas operacionais Android e iOS/OS X.

    Para obter detalhes e orientações de uso no iOS/OS X, veja a classe [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc), que fornece informações de rastreamento e o método adicional de registro para rastreamento de documentos em [**MSUserPolicy**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msuserpolicy_interface_objc). Há adições semelhante para Android no [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) e [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy).

    Para obter uma descrição detalhada do recurso de rastreamento de documentos, veja [**Como usar o rastreamento de documentos**](how-to-use-document-tracking.md).

-   Um conjunto de métodos síncronos que corresponde às versões assíncronas da API do Android:

    [**Método síncrono CustomProtectedInputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_create_synchronous_method_java)

    [**Método síncrono CustomProtectedOutputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Método síncrono ProtectedFileInputStream.create**](/rights-management/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_synchronous_method)

    [**Método síncrono ProtectedFileOutputStream.create**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Método síncrono TemplateDescriptor.getTemplates**](/rights-management/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_gettemplates_synchronous_method_java)

    [**Método síncrono UserPolicy.acquire**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_acquire_synchronous_method_java)

    [**Método síncrono UserPolicy.create (PolicyDescriptor…)**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_policydescriptor_______synchronous_method_java)

    [**Método síncrono UserPolicy.create (TempalteDescriptor…)**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_templatedescriptor_______synchronous_method_java)

-   Uma nova classe [**ProtectedBuffer**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedbuffer_class) foi adicionada à API do Android.
-   Atualizações para melhorar a experiência com mensagens de erro e com a solução de problemas.
-   Aprimoramentos consideráveis de desempenho para operações criptográficas.

### Atualização de julho de 2015 - Acrescenta suporte para Linux/desenvolvimento em C++

Essa versão adiciona o seguinte:

-   RMS SDK 4.1 para plataformas Linux

    Para saber mais, confira [Introdução](get-started.md).

### Atualização de maio de 2015 - Acrescenta o controle de registro em log

Essa versão adiciona suporte para o seguinte:

-   iOS

    A criptografia e descriptografia de aplicativo pode operar independentemente e em paralelo.

    Para saber mais, confira [**MSProtector**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msprotector_class_objc).

    Configurações de controle do nível do log habilitadas.

    Para saber mais, confira [Como habilitar o registro em log de desempenho e de erros](enabling-logging.md)

    Adição do suporte à limpeza do cache.

    Para saber mais, confira [**MSProtection:resetStateWithCompletionBlock**](/rights-management/sdk/4.2/api/iOS/msprotection#msipcthin2_msprotection_resetstatewithcompletionblock_method_objc).

### Atualização de fevereiro de 2015 - Acrescenta o suporte a aplicativos da Windows Store

Essa versão adiciona suporte para aplicativos da Windows Store e fornece uma paridade funcional com a versão do RMS SDK 4.1 para iOS/OS X, Android e Windows Phone .

### Atualização de janeiro de 2015 - Acrescenta suporte à plataforma WinPhone

Essa versão adiciona suporte para o sistema operacional Windows Phone e fornece uma paridade funcional com a versão do RMS SDK 4.1 para iOS/OS X e Android.

## Atualização de outubro de 2014 - Atualiza para o Microsoft RMS SDK 4.1

A versão 4.1 do RMS SDK adiciona os seguintes recursos novos ao Google Android e Apple iOS/OS X.

-   Extensões da API do SDK para Android e iOS/OS X para processamento de *consentimento do usuário*, permitindo a confirmação do usuário de comportamentos do SDK. Atualmente, o rastreamento de documentos e o acesso a URLs de serviço desconhecidas do AD RMS são os tipos de consentimento com suporte.

    Para saber mais, veja como exemplo, a versão da API do Android da [**interface ConsentCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_consentcallback_interface_java).

-   Agora há suporte para iOS 8 e OS X10.10 (Yosemite). Também houve algumas alterações de nome de propriedade exigidas pelo Xcode 6.

    Exemplo; MSUserPolicy.name alterado para [**MSUserPolicy.policyName**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_name_property_objc).

## Notas de versão

Esta seção descreve as informações sobre as versões atuais e anteriores das APIs do Microsoft Rights Management SDK 4.x que você, como desenvolvedor, deseja conhecer.

**AD RMS SDK 4.1 - Versão de disponibilidade global para as plataformas iOS/OS X e Android**

-   **Suporte para AD RMS** - Os administradores de TI podem usar aplicativos habilitados para RMS em dispositivos móveis com as extensões de dispositivo móvel do novo servidor de AD RMS.
-   **Consumo offline** - Os usuários finais podem acessar no modo offline os dados do RMS protegidos.
-   **Autenticação separada** - Os desenvolvedores podem usar sua própria biblioteca de autenticação para o Azure RMS e o AD RMS (ou usar a [ADAL (Biblioteca de Autenticação do Azure AD)](https://MSDN.Microsoft.Com/en-us/library/jj573266.aspx)).
-   **Interface de usuário separada** - os desenvolvedores podem criar sua interface de usuário para proteger e consumir documentos protegidos do RMS.
-   **API reprojetada** – Os desenvolvedores podem aproveitar uma API simples e transparente de criptografia e descriptografia que fornece comportamentos e experiência de usuário consistentes de RMS com o mínimo de esforço.

**Comum a todas as plataformas**

-   As APIs do RMS SDK 4.x não são *thread-safe*.

**Android**

-   Quando você usa um aplicativo de exemplo em um dispositivo Amazon® Kindle para exibir anexos em .ptxt, primeiro precisa baixar o arquivo antes de visualizá-lo.

    **Solução** - Esse é um problema conhecido e será abordado posteriormente.

-   Um aplicativo que usa o SDK pode falhar se várias instâncias forem permitidas.

    **Solução** - Verifique se o aplicativo não permite chamadas de várias instâncias à API do Android.

-   Quando uso o método [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array, int offset, int length)** com um tamanho diferente no valor *array.length*, não sou capaz de consumir o conteúdo mais tarde usando o SDK.

    **Solução** - Esse é um problema conhecido. Para resolvê-lo, passe sempre uma matriz **bytes \[\]** com o mesmo valor de tamanho que o parâmetro de tamanho ou use o método [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array)**.

**iOS e OS X**

-   Há dois dialetos de português que recebem suporte de nossos SDKs para iOS e OS X. Infelizmente, devido a um bug, no momento não oferecemos suporte completo à primeira localização. Devido a esse bug, não há suporte total para português. A maior parte do texto está traduzida, mas não a interface de usuário.

    1. Português

    2. Português (Portugal)

**Somente iOS**

-   O RMS SDK 4.x não mostra o indicador de atividade de rede.

    Esse é um comportamento conhecido opcional para iOS de acordo com as Diretrizes de Interface Humana da Apple.

**Somente para OS X**

-   O RMS SDK 4.x não mostra o indicador de atividade de rede.

    Esse é um comportamento conhecido opcional para o OS X de acordo com as Diretrizes de Interface Humana da Apple.

-   **Solução** - para criar um aplicativo MDI (interface de vários documentos) usando nosso SDK para OS X, use as diretrizes a seguir.

    Os métodos abaixo não devem ser executados simultaneamente. Para monitorar a conclusão da execução, use a abordagem de bloco de conclusão, conforme indicado.

    - [**protectedDataWithProtectedFile**](/rights-management/sdk/4.2/api/iOS/msprotecteddata#msipcthin2_msprotecteddata_protecteddatawithprotectedfile_completionblock_method_objc)
    - [**customProtectedDataWithPolicy**](/rights-management/sdk/4.2/api/iOS/mscustomprotecteddata#msipcthin2_mscustomprotecteddata_customprotecteddatawithpolicy_protecteddata_contentstartposition_contentsize_completionblock_method_objc)



**Observação** Não há suporte para aplicativos MDI em nossa API para iOS.

## Perguntas frequentes

**Todas as plataformas**

**P**: Eu não vejo uma interface do usuário de seleção de **permissões personalizadas** no fluxo de trabalho de proteção. Por quê?

**R**: Esse é um problema conhecido e será abordado posteriormente.

**P**: Como obter novos locatários organizacionais para experimentar o SDK e os aplicativos de exemplo?

**R**: Para solicitar credenciais para organizações de teste do Azure AD RMS, envie um email para <rmcstbeta@microsoft.com>.

**P**: Não vejo qualquer discussão de hierarquia de teste aqui na documentação. Por quê?

**R**: Não há um conceito de hierarquia de teste com os novos AD RMS SDKs. Você sempre trabalhará com a hierarquia de produção.

**P**: Na versão 2.1 do RMS SDK, era necessário gerar um manifesto para cada aplicativo que implementasse a proteção de informações. Isso ainda é verdade para as versões 4.0 e posteriores do SDK?

**R**: Não, os manifestos não são mais necessários para as versões 3.0 e posteriores do Rights Management SDK.

**Android**

**P**: Em quais ambientes de desenvolvimento o SDK foi testado?

**R**: Eclipse Juno usando a API 15 do Google e posteriores.

**P**: Posso chamar cancel(), um método de cancelamento, do thread da interface de usuário?
**R**: Você deve chamar cancel() de um thread que não seja na interface de usuário, pois isso pode abortar uma conexão de rede.

**iOS**

**P**: Quais plataformas foram verificadas para o desenvolvimento do SDK?

**R**: Xcode 5.0 com iOS 7 e posterior.

**P**: Chamei um método cancel() em uma operação, no entanto, ainda recebo uma notificação de que a operação foi concluída. Por quê?

**R**: Nem todas as operações podem ser canceladas, portanto, uma operação de cancelamento é executada da melhor forma possível.

**OS x**

**P**: A estrutura do aplicativo de exemplo foi adaptada para o Xcode 5. Posso trabalhar com o Xcode 4.6?

**R**: O OSX SDK funciona apenas com o Xcode 4.6 e posterior, e também com o OS X 10.8 e posterior.

 

 


<!--HONumber=Apr16_HO4-->


