---
# required metadata

title: Configuração do Android | Azure RMS
description: Aplicativos Android podem usar o Microsoft Rights Management SDK 4.2 para habilitar a proteção integrada de informações em seus aplicativos.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9728c135-0e7f-4f5c-95ba-1db79e418080

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Configuração do Android

Aplicativos Android podem usar o Microsoft Rights Management SDK 4.2 para habilitar a proteção de informações em seus aplicativos usando o AAD RM (Azure Active Directory Rights Management).

Este tópico orientará você pela configuração de seu ambiente para criação de seus próprios aplicativos novos.

-   [Pré-requisitos](#prerequisites)
-   [Opcional](#optional)
-   [Configuração de seu ambiente de desenvolvimento](#configuring_your_development_environment_)
-   [Consulte também](#see_also)

## Pré-requisitos

Recomendamos o seguinte software em seu sistema de desenvolvimento:

-   Sistema operacional Windows ou OS X para executar o ambiente de desenvolvimento do [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
-   Este guia pressupõe que você esteja usando o SDK do Eclipse, começando com o Eclipse Juno 4.2, e uma instalação padrão.
-   Java a partir do Java 1.6.
-   [Plugin do ADT (Android Developer Tools)](http://developer.android.com/sdk/installing/index.html). OBSERVAÇÃO - Talvez você receba uma solicitação para reiniciar o Eclipse a fim de concluir a instalação.

     

-   O pacote do MS RMS SDK 4.2 para Android. Para saber mais, confira [Introdução](get-started.md).

    Esse SDK pode ser usado para desenvolver para Android 4.0.3 (API nível 15) e posterior.

-   Biblioteca de autenticação: recomendamos o uso da [ADAL (Biblioteca de Autenticação do Azure AD)](https://msdn.microsoft.com/en-us/library/jj573266.aspx). No entanto, outras bibliotecas de autenticação que oferecem suporte a OAuth 2.0 também podem ser usadas.

    Para saber mais, confira [ADAL para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

    **Observação** Se o seu aplicativo não usar a Biblioteca ADAL como a biblioteca de autenticação do OAuth 2.0, analise esta orientação do Android, [Some SecureRandom Thoughts](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html) (Algumas ideias sobre SecureRandom).

     

Leia o tópico [Novidades](release-notes.md) para saber mais sobre as atualizações de API, notas de versão e perguntas frequentes (FAQ).

## Opcional

Nossa biblioteca de interface de usuário fornece uma interface de usuário reutilizável para operações de consumo e proteção para desenvolvedores que não querem criar sua própria interface de usuário personalizada - [Biblioteca de interface do usuário e exemplo de aplicativo para Android](https://github.com/AzureAD/rms-sdk-ui-for-android).

## Configuração de seu ambiente de desenvolvimento

**Observação** Versão de visualização do MS RMS SDK 4.2: nesta versão de visualização, as capturas de tela não foram atualizadas para mostrar a mudança no nome dos caminhos de com/microsoft/protection para com/microsoft/rightsmanagment. No entanto, o texto foi atualizado.

 
-   Abra o ambiente de desenvolvimento do Eclipse.
-   Para criar um novo projeto de Aplicativo do Android, no menu **Arquivo**, clique em **Novo**, clique em **Projeto** e, em seguida, selecione **Projeto de Aplicativo Android**.

    ![](../media/Android-setup-01c.png)

-   Digite o nome do aplicativo. O nome do projeto e o nome do pacote é preenchido com base no nome do aplicativo.
-   Clique em **Avançar** e selecione onde você deseja criar o espaço de trabalho.

    ![](../media/Android-setup-02a.jpg)

-   Clique em **Avançar** e selecione um ícone para seu aplicativo.

    ![](../media/Android-setup-03.png)

-   Clique em **Avançar** e selecione **Atividade em Branco** para criar a atividade.

    ![](../media/Android-setup-04.png)

-   Clique em **Avançar** e forneça um nome para a atividade. Você pode deixar *MainActivity* como o nome padrão, com o nome de layout *activity\_main*.

    ![](../media/Android-setup-05a.jpg)

-   Clique em **Finalizar**.

    ![](../media/Android-setup-06.jpg)

-   O projeto foi criado, junto com a classe de atividade principal *MainActivity.java*.

**Referência ao SDK**

-   Navegue até a pasta na qual você extraiu o *adrms\_android\_sdk.zip*. Na pasta "SDK > com > microsoft > rightsmanagement", verifique se os arquivos *.classpath*, *.project* e *project.properties* não estão marcados como somente leitura.
-   Para fazer referência ao SDK, você deve importá-lo no espaço de trabalho.

    No Eclipse, clique em **Arquivo**. No menu **Arquivo**, clique em **Importar**. Na caixa de diálogo **Importar**, selecione **Android/Código Existente do Android no Espaço de Trabalho**.

    ![](../media/Android-setup-07.png)

-   Clique em **Avançar**. Navegue para selecionar a pasta na qual você extraiu o *adrms\_android\_sdk.zip*. O SDK deve aparecer na lista como **com.microsoft.rightsmanagement**.

    ![](../media/Android-setup-08c.jpg)

-   Quando você clicar em **Concluir**, o projeto do SDK aparecerá como um irmão de seu aplicativo criado anteriormente.

    ![](../media/Android-setup-09.jpg)

-   Clique com botão direito no ícone **Projeto** e veja as propriedades do projeto.
-   Navegue até a guia **Android**.
-   Clique em **Adicionar** e, em seguida, selecione a biblioteca *com.microsoft.rightsmanagement* do espaço de trabalho.

    ![](../media/Android-setup-10b.jpg)

-   Clique em **OK**.

    Como o MS RMS SDK 4.2 se conecta ao AAD RM, o aplicativo receber a permissão **INTERNET** e **ACCESS\_NETWORK\_STATE**. Para fazer isso, abra o arquivo *AndroidManifest.xml* na raiz do projeto.

    Para adicionar as permissões, clique em **Adicionar** e, em seguida, escolha **Permissões de Uso**.

    ![](../media/Android-setup-11d.jpg)

-   Você pode verificar a etapa do manifesto exibindo o manifesto no modo de exibição de editor de texto. Verifique se as linhas abaixo aparecem:


    <uses-sdk
         android:minSdkVersion="15"
         android:targetSdkVersion="19"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission/>


**Observação** O SDK usa *android.support.v4*

-   Agora você está pronto para criar seus próprios aplicativos novos do Android.

### Consulte também

[Introdução](get-started.md)

[Novidades](release-notes.md)

[Termos e conceitos de desenvolvedor](core-concepts.md)

[Referência à API do Android](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement)

 

 


<!--HONumber=Apr16_HO3-->


