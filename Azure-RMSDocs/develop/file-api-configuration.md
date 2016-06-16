---
# required metadata

title: Configuração da API do arquivo | Azure RMS
description: O comportamento da API do arquivo pode ser definido nas configurações do registro.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuração da API do arquivo


O comportamento da API do arquivo pode ser definido nas configurações do registro.

A API do arquivo fornece dois tipos de proteção: proteção nativa e proteção PFile.

-   **Proteção nativa** – o arquivo é protegido em um formato de AD RMS com base em seu tipo MIME (extensão de nome de arquivo).
-   **Proteção PFile** – o arquivo é protegido no formato de arquivo AD RMS protegido (PFile).

Para saber mais sobre formatos de arquivo com suporte, confira **Detalhes de suporte a arquivo da API do arquivo** neste tópico.

## Descrições e tipos de chave/valor de chave

As seções a seguir descrevem as chaves e valores de chave que controlam a criptografia.

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection

**Tipo**: chave

**Descrição**: contém a configuração geral para a API do Arquivo.

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;

**Tipo**: chave

**Descrição**: especifica informações de configuração para uma extensão de arquivo específica. Por exemplo, TXT, JPG e assim por diante.

- O caractere curinga ' *', é permitido. No entanto, uma configuração de uma extensão específica tem precedência sobre a configuração de um curinga. O caractere curinga não afeta as configurações dos arquivos do Microsoft Office. Estes devem ser desabilitados explicitamente por tipo de arquivo.
- Para especificar os arquivos que não têm uma extensão, use '.'
- Não especifique o caractere '.' ao especificar a chave para uma extensão de arquivo específica. Por exemplo, use `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` a fim de especificar configurações para arquivos .txt. (Não use `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`.)

Defina o valor **Criptografia** na chave para especificar o comportamento de proteção. Se o valor **Criptografia** não for definido, o comportamento padrão para o tipo de arquivo será seguido.


### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;\Encryption*

**Tipo**: REG_SZ

**Descrição**: contém um dos três valores:

- **Desativada**: a criptografia está desabilitada.

> [AZURE.NOTE] Essa configuração não tem nenhuma relevância para a descriptografia. Qualquer arquivo criptografado, seja com proteção nativa ou Pfile, pode ser descriptografado, desde que o usuário tenha o direito de **EXTRAÇÃO**.

- **Nativa**: a criptografia nativa é usada. No caso de arquivos do Office, o arquivo criptografado terá a mesma extensão do arquivo original. Por exemplo, um arquivo com a extensão de arquivo .docx será criptografado como um arquivo com uma extensão .docx. No caso de outros arquivos que podem ter a proteção nativa aplicada, o arquivo será criptografado como um arquivo com uma extensão do formato p*zzz*, em que *zzz* é a extensão de arquivo original. Por exemplo, arquivos. txt serão criptografados em um arquivo com a extensão. ptxt. Abaixo temos uma lista de extensões de arquivo que pode ter a proteção nativa aplicada.

- **Pfile**: a criptografia Pfile é usada. O arquivo criptografado terá pfile acrescentado à extensão do original. Por exemplo, após a criptografia, um arquivo. txt, terá uma extensão. txt.pfile.


> [AZURE.NOTE] Essa configuração não tem nenhuma relevância para formatos de arquivo do Office. Por exemplo, se o valor `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` for definido como &quot;Pfile”, os arquivos .docx ainda serão criptografados usando a proteção nativa e o arquivo criptografado ainda terá uma extensão de arquivo .docx.

A configuração de qualquer outro valor ou a ausência valor resulta no comportamento padrão.

## Comportamento padrão para formatos de arquivo diferentes

-   **Arquivos do Office** A criptografia nativa está habilitada.
-   **Arquivos txt, xml, jpg, jpeg, pdf, png, tiff, bmp, gif, giff, jpe, jfif, jif** A criptografia nativa está habilitada (xxx se torna pxxx)
-   **Todos os outros arquivos** A criptografia de arquivo protegido (pfile) está habilitada (xxx se torna xxx.pfile)

Se a criptografia é tentada em um tipo de arquivo que está bloqueado, ocorre um erro [**IPCERROR\_FILE\_ENCRYPT\_BLOCKED**](/rights-management/sdk/2.1/api/win/error%20codes).

### API de arquivo – detalhes do suporte a arquivo

Suporte nativo pode ser adicionado a qualquer tipo de arquivo (extensão). Por exemplo, qualquer extensão &lt;ext&gt; (não office e pdf), \*.p&lt;ext&gt; será usada se a configuração de administração para essa extensão for "NATIVA".

**Arquivos do Office**

-   Extensões de arquivo: doc, dot, xla, xls, xlt, pps, ppt, docm, docx, dotm, dotx, xlam, xlsb, xlsm, xlsx, xltm, xltx, xps, potm, potx, ppsx, ppsm, pptm, pptx, thmx.
-   Tipo de proteção = nativa (padrão): sample.docx é criptografado como sample.docx
-   Tipo de proteção = Pfile: em arquivos do Office, o efeito é o mesmo da Nativa.
-   Desativada: desabilita a criptografia.

**Arquivos PDF**

-   Tipo de proteção = nativa: sample.pdf é criptografado e denominado sample.ppdf
-   Tipo de proteção = Pfile: sample.pdf é criptografado e denominado sample.pdf.pfile.
-   Desativada: desabilita a criptografia.

**Todos os outros formatos de arquivo**

-   Tipo de proteção = Pfile: sample.*zzz* é criptografado e chamado sample.*zzz*. pfile, em que *zzz* é a extensão de arquivo original.
-   Desativada: desabilita a criptografia.

### Exemplos

As configurações a seguir habilitam a criptografia Pfile para arquivos txt. Arquivos do Office terão proteção nativa aplicada (por padrão), arquivos txt terão proteção Pfile aplicada e todos os outros arquivos terão bloqueio de proteção (por padrão).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

As configurações a seguir habilitam a criptografia Pfile para todos os arquivos que não sejam do Office, exceto arquivos txt. Arquivos do Office terão proteção nativa aplicada (por padrão), arquivos txt terão bloqueio de proteção e todos os outros arquivos terão proteção Pfile aplicada.

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

As configurações a seguir desabilitam a criptografia nativa para arquivos docx. Arquivos do Office, exceto arquivos docx, terão proteção nativa aplicada (por padrão) e todos os outros arquivos terão bloqueio de proteção (por padrão).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## Tópicos relacionados

* [Notas do desenvolvedor](developer-notes.md)
* [**IPCERROR\_FILE\_ENCRYPT\_BLOCKED**](/rights-management/sdk/2.1/api/win/error%20codes)
 

 


<!--HONumber=Jun16_HO2-->


