---
# required metadata

title: Monitorar o conector do Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Monitorar o conector do Azure Rights Management

*Aplica-se a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Depois de instalar e configurar o conector RMS, você pode usar os métodos e as informações a seguir para ajudá-lo a monitorar o conector e o uso do Azure RMS pela sua organização.

## Entradas de log de eventos do aplicativo

O conector RMS usa o log de eventos do aplicativo para registrar entradas para o **conector Microsoft RMS**. 

Por exemplo, eventos de Informações, como ID 1000, confirmam que o serviço do conector foi iniciado, ID 1002 quando um servidor conecta-se com êxito ao conector RMS e ID 1004 sempre que a lista de contas autorizadas (cada conta é listada) é baixada para o conector. 

Se você não tiver configurado o conector para usar HTTPS, espere ver um Aviso ID 2002 dizendo que um cliente está usando uma conexão (HTTP) não segura.

Se a conexão do conector ao Azure RMS falhar, você provavelmente verá o Erro 3001. Por exemplo, isso pode ser o resultado de um problema de DNS ou da falta de acesso à Internet para um ou mais servidores que estão executando o conector RMS. 

> [!TIP] Quando servidores de conector RMS não conseguem se conectar ao Azure RMS, o motivo costuma ser as configurações de proxy Web.

Como acontece com todas as entradas de log de eventos, analise a mensagem para obter mais detalhes.

Além de verificar o log de eventos ao implantar o conector pela primeira vez, verifique se há avisos e erros de maneira contínua. Por exemplo, o conector pode estar funcionando conforme o esperado inicialmente, mas outros administradores podem alterar configurações dependentes. Por exemplo, outro administrador altera a configuração do servidor proxy Web de modo que os servidores do conector RMS não conseguem mais acessar a Internet (Erro 3001) ou remove uma conta de computador de um grupo que você especificou como autorizado a usar o conector (Aviso 2001).

## Contadores de desempenho

Quando você instala o conector RMS, ele cria automaticamente contadores de desempenho do **conector do Microsoft Rights Management** que podem ser úteis para ajudá-lo a monitorar o desempenho do uso do Azure RMS por meio do conector. 

Por exemplo, se você enfrentar atrasos regularmente ao proteger documentos ou emails ou ao abrir documentos ou emails protegidos, os contadores de desempenho poderão ajudar a determinar se o atraso é devido ao tempo de processamento do conector, ao tempo de processamento do Azure RMS ou a atrasos na rede. Para ajudá-lo a identificar a origem do atraso, procure os contadores que incluem as contagens médias de **Tempo de Processamento do Conector**, **Tempo de Resposta do Serviço** e **Tempo de Resposta do Conector**. Por exemplo: **Tempo Médio de Resposta do Conector para Solicitação em Lote Bem-sucedida de Licenciamento**.

Se você tiver adicionado recentemente novas contas de servidor para usar o conector, um bom contador a verificar será o **Tempo desde a última atualização de política de autorização** para confirmar se o conector baixou a lista desde que você a atualizou, ou se você precisa esperar um pouco mais (até 15 minutos).

## Analisador do RMS

Você pode usar a ferramenta Analisador do Rights Management Services para ajudá-lo a monitorar a integridade do conector e identificar problemas de configuração.

Se você ainda não tiver baixado essa ferramenta, poderá fazer isso no [Centro de Download](https://www.microsoft.com/en-us/download/details.aspx?id=46437) e instalá-la em qualquer computador com acesso à Internet e que possa conectar-se ao conector RMS. Execute a ferramenta e, na página **Bem-vindo**, selecione a opção **Conector Azure RMS**.

Para obter informações e instruções adicionais, consulte o **Detalhes** e **Instruções de Instalação** na página de download.

## Logging

O log de uso ajuda a identificar quando os emails e documentos estão protegidos e consumidos. Quando isso é feito usando o conector RMS, o campo de ID de usuário nos logs de contém o nome da entidade de serviço gerado automaticamente ao instalar o conector RMS.

Para obter mais informações, consulte [Registrando em log e analisando o uso do Azure Rights Management](log-analyze-usage.md).

Se você precisar de logs mais detalhados para fins de diagnóstico, poderá usar [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) do Windows Sysinternals e habilitar o rastreamento para o conector RMS modificando o arquivo web.config para o site Padrão no IIS. Para fazer isto:

1. Localize o arquivo web.config em **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Altere a seguinte linha:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Substitua essa linha pela seguinte:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Pare e inicie o IIS para ativar o rastreamento. 

5.  Depois de capturar todos os rastreamentos necessários, reverta a linha na etapa 3 e pare e inicie o IIS novamente.



<!--HONumber=Jun16_HO2-->


