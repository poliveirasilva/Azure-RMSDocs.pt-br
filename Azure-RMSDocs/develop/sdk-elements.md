---
# required metadata

title: Arquivos do ambiente de desenvolvimento | Azure RMS
description: Este tópico mostra os arquivos do ambiente de desenvolvimento e seus locais de instalação correspondentes no seu computador.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Arquivos do ambiente de desenvolvimento

Este tópico mostra os arquivos do ambiente de desenvolvimento e seus locais de instalação correspondentes no seu computador.

O Rights Management Services SDK 2.1 inclui os arquivos a seguir, instalados no computador no local padrão ou aquele que você especificou: %MsipcSDKDir%.

|Arquivo|Caminho|Descrição|
|----|----|-----------|
|ReadMe.htm| \ | Contém um link para a Ajuda do RMS e [Notas de versão](release-notes-rtm.md).|
|Isvtier5appsigningprivkey.dat|\bin|Contém a chave privada usada para gerar um manifesto para uso durante o desenvolvimento de um aplicativo habilitado para RMS.|
|Isvtier5appsigningpubkey.dat|\bin|Contém a chave pública usada para gerar um manifesto para uso durante o desenvolvimento de um aplicativo habilitado para RMS.|
|Isvtier5appsignsdk_client.xml|\bin|Usado para gerar um manifesto para uso durante o desenvolvimento de um aplicativo habilitado para RMS.|
|YourAppName.isv.mcf|\bin|Um arquivo de configuração clichê do manifesto, que você pode usar para gerar um manifesto durante o desenvolvimento de um aplicativo habilitado para RMS.|
|Ipcsecproc_isv.dll|\bin\x86|DLL usado internamente, para aplicativos x86, pelo Cliente Active Directory Rights Management Services 2.1 ao operar na hierarquia do ISV.|
|Ipcsecproc_ssp_isv.dll|\bin\x86|DLL usado internamente, em aplicativos x86, pelo AD RMS 2.1 ao operar na hierarquia do ISV.|
|Ipcsecproc_isv.dll|\bin\x64|DLL usado internamente, em aplicativos x64, pelo Cliente AD RMS 2.1 ao operar na hierarquia do ISV.|
|Ipcsecproc_ssp_isv.dll|\bin\x64|DLL usado internamente, em aplicativos x64, pelo Cliente AD RMS 2.1 ao operar na hierarquia do ISV.|
|Msipc.h|\inc|Arquivo de inclusão principal para o RMS SDK 2.1.|
|Ipcprot.h|\inc|Contém a interface pública exportada com o RMS SDK 2.1.|
|Ipcbase.h|\inc|Contém tipos básicos e funções auxiliares exportadas com o RMS SDK 2.1.|
|Ipcerror.h|\inc|Contém códigos de erro públicos exportados pelo RMS SDK 2.1.|
|Ipcfile.h|\inc|Contém as interfaces de APIs de arquivo exportadas com o RMS SDK 2.1|
|Msipc.lib|\lib|Biblioteca a vincular ao usar o RMS SDK 2.1 para compilar aplicativos x86.|
|Msipc_s.lib|\lib|Fornece o ponto de entrada para [<strong>IpcInitialize</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) para aplicativos x86.|
|Msipc.lib|\lib\x64|Biblioteca a vincular ao usar o RMS SDK 2.1 para compilar aplicativos x64.|
|Msipc_s.lib|\lib\x64|Fornece o ponto de entrada para [<strong>IpcInitialize</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) para aplicativos x64.|
|Genmanifest.exe|\tools|Gera um manifesto para uso durante o desenvolvimento de um aplicativo habilitado para RMS.|
 

 

 


<!--HONumber=Apr16_HO4-->


