---
# required metadata

title: Configuração da API de Ficheiros | Azure RMS
description: O comportamento da API de Ficheiros pode ser configurado através de definições no registo.
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

# Configuração da API de Ficheiros


O comportamento da API de Ficheiros pode ser configurado através de definições no registo.

A API de Ficheiros fornece dois tipos de proteção: a proteção nativa e a proteção PFile.

-   **Proteção nativa** – o ficheiro é protegido para um formato do AD RMS baseado no respetivo tipo de MIME (extensão de nome de ficheiro).
-   **Proteção PFile** – o ficheiro é protegido para o formato de Ficheiro Protegido (PFile) do AD RMS.

Para obter mais informações sobre formatos de ficheiro suportados, consulte **Detalhes de Suporte de Ficheiros da API de Ficheiros** neste tópico.

## Tipos e descrições de Chaves/Valores de Chave

As secções seguintes descrevem as chaves e os valores de chave que controlam a encriptação.

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection

**Tipo**: Chave

**Descrição**: contém a configuração geral da API de Ficheiros.

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;

**Tipo**: Chave

**Descrição**: especifica as informações de configuração de uma extensão de ficheiro específica. Por exemplo, TXT, JPG, entre outras.

- O caráter universal (*) é permitido. No entanto, uma definição para uma extensão específica tem prioridade sobre a definição da condição universal. O caráter universal não afeta as definições de ficheiros do Microsoft Office. Estas devem ser explicitamente desativadas por tipo de ficheiro.
- Para especificar os ficheiros que não tenham uma extensão, utilize '.'
- Não especifique o caráter '.' quando especificar a chave para uma extensão de ficheiro específica. Utilize, por exemplo, `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` para especificar definições para os ficheiros .txt. (Não utilize `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`).

Defina o valor de **Encriptação** na chave para especificar o comportamento de proteção. Se o valor de **Encriptação** não for definido, é aplicado o comportamento predefinido para o tipo de ficheiro.


### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;\Encryption*

**Tipo**: REG_SZ

**Descrição**: contém um de três valores:

- **Desativar**: a encriptação está desativada.

> [!Note] Esta definição não tem efeito na desencriptação. Qualquer ficheiro encriptado, seja ele encriptado com a proteção nativa ou Pfile, pode ser desencriptado, desde que o utilizador tenha o direito **EXTRAIR**.

- **Nativa**: a encriptação nativa é utilizada. Para ficheiros do Office, o ficheiro encriptado terá a mesma extensão que o ficheiro original. Por exemplo, um ficheiro com a extensão de ficheiro .docx será encriptado para um ficheiro com uma extensão .docx. Para outros ficheiros que podem ter a proteção nativa aplicada, o ficheiro será encriptado para um ficheiro com uma extensão no formato p*zzz*, em que *zzz* é a extensão do ficheiro original. Por exemplo, os ficheiros .txt serão encriptados para um ficheiro com a extensão .ptxt. Consulte abaixo a lista de extensões de ficheiros que podem ter a proteção nativa aplicada.

- **Pfile**: a encriptação PFile é utilizada. O ficheiro encriptado terá .pfile anexado à extensão original. Por exemplo, depois da encriptação, um ficheiro .txt terá uma extensão .txt.pfile.


> [!Note] Esta definição não tem efeito em formatos de ficheiros do Office. Por exemplo, se o valor `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` estiver definido para &quot;Pfile”, os ficheiros .docx ainda serão encriptados com a proteção nativa e o ficheiro encriptado continuará a ter uma extensão de ficheiro .docx.

A definição de qualquer outro valor ou nenhum valor resulta no comportamento predefinido.

## Comportamento predefinido para formatos de ficheiro diferentes

-   **Ficheiros do Office** A encriptação nativa está ativada.
-   **Ficheiros txt, xml, jpg, jpeg, pdf, png, tiff, bmp, gif, giff, jpe, jfif, jif** A encriptação nativa está ativada (xxx torna-se pxxx)
-   **Todos os outros ficheiros** A encriptação ativada é a de ficheiro protegido (.pfile) (xxx torna-se xxx.pfile)

Se a encriptação for tentada num tipo de ficheiro que está bloqueado, ocorre um erro [**IPCERROR\_FILE\_ENCRYPT\_BLOCKED**](/rights-management/sdk/2.1/api/win/error%20codes).

### API de Ficheiros – Detalhes de Suporte de Ficheiros

É possível adicionar suporte nativo a qualquer tipo de ficheiro (extensão). Por exemplo, para qualquer extensão &lt;ext&gt; (não Ooffice), \*.p&lt;ext&gt; será utilizado se a configuração de administração para essa extensão for "NATIVO".

**Ficheiros do Office**

-   Extensões de ficheiros: doc, dot, xla, xls, xlt, pps, ppt, docm, docx, dotm, dotx, xlam, xlsb, xlsm, xlsx, xltm, xltx, xps, potm, potx, ppsx, ppsm, pptm, pptx, thmx.
-   Tipo de proteção = Nativa (predefinição): exemplo.docx está encriptado para exemplo.docx
-   Tipo de proteção = Pfile: nos ficheiros do Office tem o mesmo efeito que Nativa.
-   Desativar: desativa a encriptação.

**Ficheiros PDF**

-   Tipo de proteção = Nativa: exemplo.pdf é encriptado e é-lhe atribuído o nome exemplo.ppdf
-   Tipo de proteção = Pfile: exemplo.pdf é encriptado e é-lhe atribuído o nome exemplo.pdf.pfile.
-   Desativar: desativa a encriptação.

**Todos os outros formatos de ficheiros**

-   Tipo de proteção = Pfile: exemplo.*zzz* é encriptado e é-lhe atribuído o nome exemplo.*zzz*.pfile; em que *zzz* é a extensão de ficheiro original.
-   Desativar: desativa a encriptação.

### Exemplos

As definições seguintes ativam a encriptação PFile para ficheiros txt. Os ficheiros do Office terão a proteção nativa aplicada (por predefinição), os ficheiros txt terão a proteção PFile aplicada e todos os outros ficheiros terão a proteção bloqueada (por predefinição).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

As definições seguintes ativam a encriptação PFile para todos os ficheiros não Office, exceto os txt. Os ficheiros do Office terão a proteção nativa aplicada (por predefinição), os ficheiros txt terão a proteção bloqueada e todos os outros ficheiros terão a proteção PFile aplicada.

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

As definições seguintes desativam a encriptação nativa para ficheiros docx. Os ficheiros do Office, exceto os ficheiros docx, terão a proteção nativa aplicada (por predefinição) e todos os outros ficheiros terão a proteção bloqueada (por predefinição).

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

* [Notas do programador](developer-notes.md)
* [**IPCERROR\_FILE\_ENCRYPT\_BLOCKED**](/rights-management/sdk/2.1/api/win/error%20codes)
 

 


<!--HONumber=Jun16_HO2-->


