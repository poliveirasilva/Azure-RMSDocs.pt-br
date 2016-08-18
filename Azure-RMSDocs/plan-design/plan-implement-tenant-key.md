---
title: "Planejando e implementando sua chave de locatário do Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f01d57759ab80b4946c07a627269550c80114131
ms.openlocfilehash: aa482dace1086222f63e9165e3089051b5de3e8c


---

# Planejando e implementando sua chave de locatário do Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use as informações nesse artigo para ajudá-lo a planejar e a gerenciar sua chave de locatário do RMS (Rights Management) para o Azure RMS. Por exemplo, em vez da Microsoft gerenciar sua chave de locatário (o padrão), caso queira gerenciar a sua própria chave de locatário de acordo com as normas específicas que se aplicam à sua organização.  Gerenciar a sua chave de locatário também é chamado de trazer sua própria chave, ou BYOK.

> [!NOTE]
> A chave de locatário do RMS também é conhecida como chave do certificado de licenciante para servidor (SLC). O Azure RMS mantém uma ou mais chaves para cada organização que assina o Azure RMS. Sempre que uma chave é usada para o RMS dentro de uma organização (tais como chaves de usuário, chaves de computador, chaves de criptografia de documento), eles a encadeiam criptograficamente com a sua chave de locatário do RMS.

**Visão geral:** Use a seguinte tabela como um guia rápido para sua topologia de chave de locatário recomendada. Então, use a documentação adicional para obter mais informações.

Se você implantar o Azure RMS usando uma chave de locatário gerenciada pela Microsoft, você pode alterar para BYOK posteriormente. No entanto, no momento você não pode alterar sua chave de locatário do Azure RMS de BYOK para gerenciada pela Microsoft.

|Requisito de negócios|Topologia de chave de locatário recomendada|
|------------------------|-----------------------------------|
|Implantar o Azure RMS rapidamente e sem a necessidade de hardware especial|Gerenciada pela Microsoft|
|Precisa de funcionalidade completa do IRM no Exchange Online com o Azure RMS|Gerenciada pela Microsoft|
|As suas chaves são criadas por você e protegidas em um módulo de segurança de hardware (HSM)|BYOK<br /><br />Atualmente, essa configuração resultará em funcionalidade reduzida do IRM no Exchange Online. Para obter mais informações, consulte [Preços e restrições do BYOK](byok-price-restrictions.md).|

## Escolha sua topologia de chave de locatário: Gerenciada pela Microsoft (o padrão) ou gerenciada por você (BYOK)
Decida qual topologia de chave de locatário é melhor para sua organização. Por padrão, o Azure RMS gera sua chave de locatário e gerencia a maioria dos aspectos do ciclo de vida da chave de locatário. Esta é a opção mais simples com as menores despesas administrativas gerais. Na maioria dos casos, você não precisa nem saber que você tem uma chave de locatário. Basta se inscrever no Azure RMS e o resto do processo de gerenciamento de chave é feito pela Microsoft.

Como alternativa, você pode querer ter controle total sobre a sua chave de locatário, que envolve criá-la e manter a cópia mestra em suas instalações. Este cenário é, muitas vezes, mencionado como trazer a sua própria chave (BYOK). Com esta opção, acontece o seguinte:

1.  Você gera a chave de locatário em suas instalações, de acordo com suas políticas de TI.

2.  Transfira com segurança a chave de locatário de um HSM (Módulo de Segurança de Hardware) em sua posse para HSMs que são de propriedade e gerenciados pela Microsoft. Durante todo esse processo, a chave de locatário nunca sai do limite de proteção de hardware.

3.  Ao transferir a chave de locatário para a Microsoft, ela permanece protegida por HSMs da Thales. A Microsoft trabalhou com a Thales para garantir que a chave de locatário não possa ser extraída de HSMs da Microsoft.

Embora seja opcional, recomendamos o uso em logs de uso do Azure RMS e quase tempo real para ver exatamente como e quando a chave de locatário é usada.

> [!NOTE]
> Como medida de proteção adicional, o Azure RMS usa mundos de segurança separados para seus centros de dados na América do Norte, EMEA (Europa, Oriente Médio e África) e Ásia. Ao gerenciar a sua própria chave de locatário, ela é vinculada ao mundo de segurança da região em que o locatário do RMS está registrado. Por exemplo, uma chave de locatário de um cliente europeu não pode ser utilizada em centros de dados na América do Norte ou na Ásia.

## O ciclo de vida da chave de locatário
Se você decidir que a Microsoft deve gerenciar sua chave de locatário, a Microsoft lidará com a maioria das operações de chave do ciclo de vida. No entanto, se decidir gerenciar sua chave de locatário, você será responsável por muitas das operações do ciclo de vida da chave e por alguns procedimentos adicionais.

Os diagramas a seguir mostram e comparam essas duas opções. O primeiro diagrama mostra que há poucas sobrecargas de administrador para você na configuração padrão, quando a Microsoft gerencia a chave de locatário.

![Ciclo de vida da chave de locatário do Azure RMS - gerenciado pela Microsoft, o padrão](../media/RMS_BYOK_cloud.png)

O segundo diagrama mostra os passos adicionais necessários ao gerenciar a sua própria chave de locatário.

![Ciclo de vida da chave de locatário do Azure RMS - gerenciado por você, BYOK](../media/RMS_BYOK_onprem.png)

Se decidir deixar a Microsoft gerenciar sua chave de locatário, não será necessária nenhuma ação adicional para gerar a chave e você pode ir direto para as [Próximas etapas](plan-implement-tenant-key.md#next-steps).

Se optar por gerenciar sua chave de locatário por conta própria, leia as seguintes seções para obter mais informações.

## Implementando sua chave de locatário do Azure Rights Management

Use as informações e os procedimentos desta seção se você tiver decidido gerar e gerenciar sua chave de locatário; o cenário BYOK (trazer a sua própria chave):


> [!IMPORTANT]
> Se você já tiver começado a usar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (o serviço está ativado) e tiver usuários que executem o Office 2010, [entre em contato com o Suporte da Microsoft](../get-started/information-support.md#to-contact-microsoft-support) antes de executar estes procedimentos. Dependendo do cenário e dos requisitos, talvez seja possível usar o BYOK, mas com algumas limitações ou passos adicionais.
> 
> Também entre em [contato com o Suporte Microsoft](../get-started/information-support.md#to-contact-microsoft-support) se a sua organização tiver políticas específicas para a manipulação de chaves.

### Pré-requisitos para o BYOK
Veja a tabela a seguir para obter uma lista de pré-requisitos para trazer sua própria chave (BYOK).

|Requisito|Mais informações|
|---------------|--------------------|
|Uma assinatura que dá suporte ao Azure RMS.|Para obter mais informações sobre as assinaturas disponíveis, consulte [Assinaturas da nuvem que dão suporte ao Azure RMS](../get-started/requirements-subscriptions.md).|
|Você não pode usar o RMS para indivíduos ou Exchange Online. Ou, se você usar o Exchange Online, entenda e aceite as limitações do uso do BYOK com essa configuração.|Para obter mais informações sobre as atuais restrições e limitações do BYOK, consulte [Preços e restrições do BYOK](byok-price-restrictions.md).<br /><br />**Importante**: atualmente, o BYOK não é compatível com o Exchange Online.|
|HSM da Thales, smartcards e software de suporte.<br /><br />**Observação**: se estiver migrando do AD RMS para o Azure RMS usando a chave de software para a chave de hardware, você deverá ter uma versão mínima de 11.62 para os drivers da Thales.|É necessário ter acesso a um Módulo de Segurança de Hardware da Thales e um conhecimento operacional básico dos HSMs da Thales. Consulte [Módulo de Segurança de Hardware da Thales](http://www.thales-esecurity.com/msrms/buy) para obter a lista de modelos compatíveis ou para comprar um HSM, se você não tiver um.|
|Se deseja transferir sua chave de locatário via Internet, em vez de estar fisicamente presente em Redmond, EUA, há 3 requisitos:<br /><br />1: uma estação de trabalho x64 offline com um sistema operacional Windows mínimo do software Windows 7 e Thales nShield que seja, pelo menos, da versão 11.62.<br /><br />Se esta estação de trabalho executa o Windows 7, você deve [instalar o Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br /><br />2: uma estação de trabalho que esteja conectada à Internet e que tenha um sistema operacional Windows mínimo de Windows 7.<br /><br />3: uma unidade USB ou outro dispositivo de armazenamento portátil que tenha, pelo menos, 16 MB de espaço livre.|Esses pré-requisitos não são necessários se você viajar para Redmond e transferir sua chave de locatário pessoalmente.<br /><br />Por razões de segurança, recomendamos que a primeira estação de trabalho não esteja conectada a uma rede. No entanto, isto não é programaticamente aplicado.<br /><br />Observação: nas instruções a seguir, essa estação de trabalho é mencionada como a **estação de trabalho desconectada**.<br /><br />Além disso, se a chave de locatário for para uma rede de produção, recomendamos o uso de uma segunda estação de trabalho separada para baixar o conjunto de ferramentas e fazer o upload da chave de locatário. Mas para fins de teste, é possível usar a mesma estação de trabalho como a primeira.<br /><br />Observação: nas instruções a seguir, essa segunda estação de trabalho é mencionada como a **estação de trabalho conectada à Internet**.|

Os procedimentos para gerar e utilizar a sua própria chave de locatário dependem se você deseja fazer isso pela Internet ou pessoalmente:

-   **Através da Internet:** Isso requer algumas etapas de configuração extras, como baixar e usar um conjunto de ferramentas e cmdlets do Windows PowerShell. No entanto, não é necessário estar fisicamente em uma instalação da Microsoft para transferir a chave de locatário. A segurança é mantida pelos seguintes métodos:

    -   Você gera a chave de locatário de uma estação de trabalho offline, o que reduz a superfície de ataque.

    -   A chave de locatário é criptografada com uma KEK (Key Exchange Key - Chave de Troca de Chave), que permanece criptografada até que seja transferida para os HSMs do Azure RMS. Apenas a versão criptografada da chave de locatário deixa a estação de trabalho de origem.

    -   Uma ferramenta define propriedades na sua chave de locatário que se vincula à sua chave de locatário para a segurança mundial do Azure RMS. Portanto, após os HSMs do Azure RMS receberem e descriptografarem a chave de locatário, somente esses HSMs poderão usá-la. Sua chave de locatário não pode ser exportada. Essa associação é exigida pelos HSMs da Thales.

    -   O KEK (Key Exchange Key) que é usado para criptografar a chave de locatário é gerado dentro dos HSMs do Azure RMS e não é exportável. Os HSMs exigem que não haja nenhuma versão clara do KEK fora dos HSMs. Além disso, o conjunto de ferramentas inclui atestado da Thales de que a KEK não é exportável e foi gerada dentro de um HSM original que foi fabricado pela Thales.

    -   O conjunto de ferramentas inclui atestado da Thales de que o mundo de segurança do Azure RMS também foi gerado em um HSM original fabricado pela Thales. Isso comprova que a Microsoft está usando hardware original.

    -   A Microsoft usa KEKs separadas, bem como mundos de segurança separados em cada região geográfica, o que garante que a sua chave de locatário só pode ser utilizada em centros de dados na região em que você a criptografou. Por exemplo, uma chave de locatário de um cliente europeu não pode ser utilizada em centros de dados na América do Norte ou na Ásia.

    > [!NOTE]
    > Sua chave de locatário pode se mover com segurança em computadores e redes não confiáveis​​, pois é criptografada e protegida com permissões de nível de controle de acesso, o que torna utilizável apenas dentro de seus HSMs e HSMs da Microsoft para o Azure RMS. Você pode usar os scripts que são fornecidos no conjunto de ferramentas para verificar as medidas de segurança e ler mais informações sobre como isso funciona a partir da Thales: [Gerenciamento de chaves de hardware na nuvem do RMS](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **Pessoalmente:** isso requer que você [entre em contato com o Suporte da Microsoft](../get-started/information-support.md#to-contact-microsoft-support) para agendar um compromisso de transferência de chave para o Azure RMS. Será necessário viajar para um escritório da Microsoft em Redmond, Washington, nos Estados Unidos, para transferir a chave de locatário para o mundo de segurança do Azure RMS.

Para instruções, selecione se você vai gerar e transferir sua chave de locatário pela Internet ou pessoalmente: 

- [Pela Internet](generate-tenant-key-internet.md)
- [Pessoalmente](generate-tenant-key-in-person.md)


## Próximas etapas

Agora que você já planejou e, se necessário, gerou sua chave de locatário, faça o seguinte:

1.  Comece a usar sua chave de locatário:

    -   Se ainda não tiver feito isso, será necessário agora ativar o Rights Management de modo que sua organização possa começar a usar o RMS. Os usuários começam imediatamente a utilizar a chave de locatário (gerenciada pela Microsoft ou por você).

        Para obter mais informações sobre uma ativação, consulte [Ativando o Microsoft Azure Rights Management](../deploy-use/activate-service.md).

    -   Se já tiver ativado o Rights Management e decidir gerenciar sua própria chave de locatário, os usuários farão a transição gradual da chave de locatário antiga para a nova chave de locatário, e essa transição escalonada pode levar algumas semanas para ser concluída. Os documentos e arquivos que foram protegidos com a chave de locatário antiga, permanecem acessíveis para usuários autorizados.

2.  Considere usar o registro em log de uso, que registra todas as transações que o RMS executa.

    Se você decidiu gerenciar sua própria chave de locatário, o log inclui informações sobre como usar sua chave de locatário. Consulte o trecho de um arquivo de log exibido no Excel a seguir, no qual os tipos de solicitação **KMSPDecrypt** e **KMSPSignDigest** mostram que a chave de locatário está sendo usada.

    ![arquivo de log no Excel no qual a chave de locatário está sendo usada](../media/RMS_Logging.png)

    Para obter mais informações sobre registro em log de uso, consulte [Registrando em log e analisando o uso do Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Mantenha sua chave de locatário.

    Para obter mais informações, consulte [Operações para sua chave de locatário do Azure Rights Management](../deploy-use/operations-tenant-key.md).




<!--HONumber=Jul16_HO3-->


