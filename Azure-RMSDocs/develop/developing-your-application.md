---
title: Desenvolvendo seu aplicativo | Azure RMS
description: "Instruções sobre como desenvolver um aplicativo usando o RMS SDK 2.1."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 07/06/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79397c82d9478cbd55630a376fe2d12f3873ebc4
ms.openlocfilehash: e00af9b9b0a5f2d917ac96812e980505d4cfd347


---

# Desenvolvendo seu aplicativo

Este tópico contém diretrizes essenciais sobre os principais aspectos de um aplicativo habilitado para RMS e pode servir como a base do desenvolvimento de seu próprio aplicativo.

## Introdução

As diretrizes neste tópico têm como base o aplicativo de exemplo, IPCHelloWorld, que ajudará você a entender os conceitos básicos e o código de um aplicativo habilitado para direitos. Você pode baixar o aplicativo de exemplo completo, [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440), do Microsoft Connect.

> [!Note] 
> O projeto IPCHelloWorld já está configurado para o Rights Management Services SDK 2.1. Para saber mais sobre como configurar um novo projeto a fim de usar o SDK 2.1 do RMS, confira [Configurar o Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md).

## Como carregar o MSIPC.dll

Antes de chamar quaisquer funções do RMS SDK 2.1, primeiro você precisa chamar a função [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) para carregar o MSIPC.dll.

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## Enumeração de modelos

Um modelo RMS define a política usada para proteger os dados, ou seja, define os usuários que têm permissão para acessar os dados e seus direitos. Os modelos RMS são instalados no servidor RMS.

O trecho de código a seguir enumera os modelos RMS disponíveis no servidor RMS padrão.

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

Essa chamada recuperará os modelos RMS instalados no servidor padrão e carregará os resultados na estrutura [IPC_TIL](/rights-management/sdk/2.1/api/win/ipc_til#msipc_ipc_til) apontada pela variável *pcTil* e, em seguida, exibirá os modelos.

      C++
      if (0 == pcTil->cTi) {
        wprintf(L"*** No templates configured for your RMS server ***\n\n");
        wprintf(L"\\------------------------------------------------------\n\n");
        goto exit;
      }

      for (DWORD dw = 0; dw < pcTil->cTi; dw++) {
        wprintf(L"Template #%d:\n", dw);
        wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
        wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
        wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
        wprintf(L"\n");
      }

## Serialização de uma licença

Antes de poder proteger os dados, você precisa serializar uma licença e obter uma chave de conteúdo. A chave de conteúdo é usada para criptografar os dados confidenciais. A licença serializada geralmente está associada aos dados criptografados e é usada pelo consumidor dos dados protegidos. O consumidor precisará chamar a função [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey) usando a licença serializada para obter a chave de conteúdo para descriptografar o conteúdo e obter a política associada ao conteúdo.

Para simplificar, use o primeiro modelo RMS retornado por [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) para serializar uma licença.

Normalmente, você usaria uma caixa de diálogo de interface do usuário para permitir que o usuário selecione o modelo desejado.

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

Depois de fazer isso você terá a chave de conteúdo, *hContentKey*, e a licença serializada, *pSerializedLicense*, que você precisa anexar aos dados protegidos.


## Proteção de dados

Agora você está pronto para criptografar os dados confidenciais usando a função [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt). Primeiro, você precisa perguntar à função **IpcEncrypt** qual será o tamanho dos dados criptografados.

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Aqui, wszText contém o texto sem formatação que você pretende proteger. A função [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) retorna o tamanho dos dados criptografados no parâmetro *cbEncrypted*.

Agora, aloque memória para os dados criptografados.

      C++
      pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

      if (NULL == pbEncrypted) {
        wprintf(L"Out of memory\n");
        goto exit;
      }

Por fim, você pode realizar a criptografia.

      C++
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        pbEncrypted, cbEncrypted, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Depois desta etapa, você terá os dados criptografados, *pbEncrypted*, e a licença serializada, *pSerializedLicense*, que será usado pelos consumidores para descriptografar os dados.

## Tratamento de erros

Em todo este exemplo de aplicativo, a função *DisplayError* está sendo usada para manipular erros.

      C++
      void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
      {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
      }

A função *DisplayError* usa a função [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) para obter a mensagem de erro do código de erro correspondente e a imprime na saída padrão.

## Limpeza

Antes de terminar, você também precisa liberar todos os recursos alocados.

      C++
      if (NULL != pbEncrypted) {
        LocalFree((HLOCAL)pbEncrypted);
      }

      if (NULL != pSerializedLicense) {
        IpcFreeMemory((LPVOID)pSerializedLicense);
      }

      if (NULL != hContentKey) {
        IpcCloseHandle((IPC_HANDLE)hContentKey);
      }

      if (NULL != pcTil) {
        IpcFreeMemory((LPVOID)pcTil);
      }

## Tópicos relacionados

- [Informações e diretrizes para desenvolvedores](developer-notes.md)
- [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt)
- [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
- [IPC_TIL](/rights-management/sdk/2.1/api/win/ipc_til#msipc_ipc_til)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Jul16_HO4-->


