---
# required metadata

title: Como Funciona o Azure RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/02/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Como funciona o Azure RMS? Os bastidores

*Aplica-se a: Azure Rights Management, Office 365*

Um dos aspetos importantes que deve saber sobre o funcionamento do Azure RMS é que o serviço Rights Management (e a Microsoft) não visualizam nem armazenam os seus dados como parte do processo de proteção de informações. As informações que protege nunca são enviadas para ou armazenadas no Azure, a menos que as armazene explicitamente no Azure ou utilize outro serviço em nuvem que as armazene no Azure. O Azure RMS simplesmente torna os dados num documento ilegível para todas as pessoas que não sejam utilizadores e serviços autorizados:

-   Os dados são encriptados ao nível da aplicação e incluem uma política que define a utilização autorizada para esse documento.

-   Quando um documento protegido é utilizado por um utilizador legítimo ou processado por um serviço autorizado, os dados no documento são desencriptados e os direitos que estão definidos na política são aplicados.

Pode ver como este processo funciona de modo geral na imagem seguinte. O documento com a fórmula secreta é protegido e, em seguida, aberto com êxito por um utilizador ou serviço autorizado. O documento é protegido por uma chave de conteúdo (a chave verde nesta imagem). A chave é exclusiva para cada documento e colocada no cabeçalho do ficheiro onde é protegida pela sua chave de raiz de inquilino do RMS (a chave vermelha nesta imagem). A sua chave de inquilino pode ser gerada e gerida pela Microsoft ou o utilizador pode gerar e fazer a gestão da sua própria chave de inquilino.

Ao longo de todo o processo de proteção, quando o Azure RMS está a encriptar, desencriptar, autorizar e a impor restrições, a fórmula secreta nunca é enviada para o Azure.

![Como o Azure RMS protege um ficheiro](../media/AzRMS_SecretColaFormula_final.png)

Para obter uma descrição detalhada do processo, consulte a secção [Explicação passo a passo sobre como funciona o Azure RMS: primeira utilização, proteção de conteúdos, consumo de conteúdos](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) neste artigo.

Para obter detalhes técnicos sobre os algoritmos e os comprimentos de chave utilizados pelo Azure RMS, consulte a secção seguinte.

## Controlos criptográficos utilizados pelo Azure RMS: comprimentos de chave e algoritmos
Embora não tenha de saber como funciona o RMS, poderão ser-lhe pedidas informações sobre os controlos criptográficos que o RMS utiliza, para certificar que a proteção de segurança está em conformidade com a norma da indústria.


|Controlos criptográficos|Função no Azure RMS|
|-|-|
|Algoritmo: AES<br /><br />Comprimento de chave: 128 bits e 256 bits [[1]](#footnote-1)|Proteção da documentação|
|Algoritmo: RSA<br /><br />Comprimento de chave: 2048 bits|Proteção da chave|
|SHA-256|Assinatura do certificado|

###### Nota de rodapé 1 

O controlo de 256 bits é utilizado pela aplicação de partilha Rights Management para uma proteção genérica e nativa quando o ficheiro tem uma extensão de nome de ficheiro .ppdf ou quando se trata de um ficheiro de imagem ou de texto protegido (como .ptxt ou .pjpg).

Como as chaves criptográficas são armazenadas e protegidas:

- O Azure RMS cria uma chave AES única (a "chave de conteúdo") para cada documento ou mensagem de e-mail que protege. Essa chave é incorporada no documento e persiste nas várias edições do documento. 

- A chave de conteúdo é protegida pela chave RSA da organização (a "chave de inquilino do Azure RMS") como parte da política no documento. Além disso, a política também é assinada pelo autor do documento. Esta chave de inquilino é comum a todos os documentos e e-mails protegidos pelo Azure RMS da organização e só pode ser alterada por um administrador do Azure RMS se a organização estiver a utilizar uma chave de inquilino gerida pelo cliente, conhecida como BYOK (Bring Your Own Key – Traga a Sua Própria Chave). 

    Esta chave de inquilino está protegida nos serviços online da Microsoft, num ambiente altamente controlado e sob monitorização rigorosa. Quando utiliza uma chave de inquilino gerida pelo cliente (BYOK), esta segurança é melhorada pela utilização de uma matriz de módulos de segurança de hardware de ponta (HSMs) em cada região do Azure, impossibilitando completamente a extração, exportação ou partilha das chaves. Para obter mais informações sobre a chave de inquilino e a BYOK, consulte [Planear e implementar a sua chave de inquilino do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

- As licenças e certificados enviados para um dispositivo Windows estão protegidos pela chave privada do dispositivo do cliente, que é criada quando um utilizador usa o Azure RMS pela primeira vez num dispositivo. Por sua vez, esta chave privada está protegida com a DPAPI do cliente, que protege estes segredos com uma chave derivada da palavra-passe do utilizador. Em dispositivos móveis, as chaves são utilizadas apenas uma vez, pois como não estão armazenadas nos clientes, não precisam de ser protegidas no dispositivo. 



## Explicação passo a passo sobre como funciona o Azure RMS: primeira utilização, proteção de conteúdos, consumo de conteúdos
Para compreender melhor como funciona o Azure RMS, vamos mostrar-lhe um fluxo típico após o [serviço do Azure RMS ser ativado](../deploy-use/activate-service.md) e o que acontece quando um utilizador usa pela primeira vez o RMS no seu computador Windows (um processo por vezes conhecido como **inicializar o ambiente de utilizador** ou arranque do sistema), **protege conteúdos** (um documento ou e-mail) e, em seguida, **consome** (abre e utiliza) os conteúdos que foram protegidos por outra pessoa.

Após o ambiente de utilizador ser iniciado, esse utilizador pode proteger documentos ou consumir documentos protegidos nesse computador.

> [!NOTE] Se o utilizador mudar de computador Windows ou outro utilizador usar este computador Windows, o processo de iniciação é repetido.

### Inicializar o ambiente de utilizador
Antes de um utilizador poder proteger conteúdos ou consumir conteúdos protegidos num computador Windows, o ambiente de utilizador tem de ser preparado no dispositivo. Este é um processo único e ocorre automaticamente sem a intervenção do utilizador quando este tenta proteger ou consumir conteúdos protegidos:

![Ativação do Cliente de RMS – passo 1](../media/AzRMS.png)

**O que acontece no passo 1**: primeiro, o cliente de RMS no computador liga-se ao Azure RMS e autentica o utilizador ao utilizar a sua conta do Azure Active Directory.

Quando a conta do utilizador está federada com o Azure Active Directory, esta autenticação é automática e não serão pedidas ao utilizador as suas credenciais.

![Ativação do Cliente de RMS – passo 2](../media/AzRMS_useractivation2.png)

**O que acontece no passo 2**: após o utilizador ser autenticado, a ligação é automaticamente redirecionada para o inquilino do RMS da organização, que emite certificados que permitem ao utilizador efetuar a autenticação no Azure RMS para poder consumir conteúdos protegidos e proteger conteúdos offline.

É guardada uma cópia do certificado do utilizador no Azure RMS para que, se o utilizador usar outro dispositivo, os certificados sejam criados com as mesmas chaves.

### Proteção de conteúdos
Quando um utilizador protege um documento, o cliente de RMS efetua as seguintes ações num documento não protegido:

![Proteção de documentos pelo RMS – passo 1](../media/AzRMS_documentprotection1.png)

**O que acontece no passo 1**: o cliente de RMS cria uma chave aleatória (a chave de conteúdo) e encripta o documento com esta chave com o algoritmo de encriptação simétrica AES.

![Proteção de documentos peli RMS – passo 2](../media/AzRMS_documentprotection2.png)

**O que acontece no passo 2**: em seguida, o cliente de RMS cria um certificado que inclui uma política para o documento, baseada num modelo ou ao especificar direitos para o documento. Esta política inclui os direitos para diferentes utilizadores ou grupos e outras restrições, como uma data de expiração.

Em seguida, o cliente de RMS utiliza a chave da organização obtida quando o ambiente de utilizador foi inicializado para encriptar a política e a chave de conteúdo simétrica. O cliente RMS também assina a política com o certificado do utilizador obtido quando o ambiente do utilizador foi inicializado.

![Proteção de documentos pelo RMS – passo 3](../media/AzRMS_documentprotection3.png)

**O que acontece no passo 3**: por fim, o cliente de RMS incorpora a política num ficheiro com o corpo do documento previamente encriptado e que, em conjunto, constituem um documento protegido.

Este documento pode ser armazenado em qualquer lugar ou partilhado com qualquer método e a política permanece sempre com o documento encriptado.

### Consumo de conteúdos
Quando um utilizador pretende consumir um documento protegido, o cliente de RMS começa por pedir acesso ao serviço do Azure RMS:

![Consumo de documentos pelo RMS – passo 1](../media/AzRMS_documentconsumption1.png)

**O que acontece no passo 1**: o utilizador autenticado envia a política do documento e os certificados do utilizador para o Azure RMS. O serviço desencripta e avalia a política e cria uma lista de direitos (se aplicável) que o utilizador tem sobre o documento.

![Consumo de documentos pelo RMS – passo 2](../media/AzRMS_documentconsumption2.png)

**O que acontece no passo 2**: em seguida, o serviço extrai a chave de conteúdo AES da política desencriptada. Esta chave é então encriptada com a chave RSA pública do utilizador que foi obtida com o pedido.

A chave de conteúdo encriptada novamente é incorporada numa licença de utilização encriptada com a lista de direitos de utilizador que, em seguida, é devolvida ao cliente de RMS.

![Consumo de documentos pelo RMS – passo 3](../media/AzRMS_documentconsumption3.png)

**O que acontece no passo 3**: por fim, o cliente de RMS obtém a licença de utilização encriptada e desencripta a mesma com a sua própria chave privada de utilizador. Isto permite que o cliente de RMS desencripte o corpo do documento conforme necessário e o apresente no ecrã.

O cliente também desencripta a lista de direitos e passa-a para a aplicação, que impõe esses direitos na interface de utilizador da aplicação.

### Variações
Os passos anteriores abrangem os cenários padrão, mas existem algumas variações:

-   **Dispositivos móveis**: quando os dispositivos móveis protegem ou consomem ficheiros com o Azure RMS, os fluxos do processo são muito mais simples. Os dispositivos móveis não passam pelo processo de inicialização do utilizador efetuado em primeiro lugar, pois cada transação (para proteger ou consumir conteúdos) é independente. À semelhança dos computadores Windows, os dispositivos móveis ligam-se ao serviço do Azure RMS e efetuam a autenticação. Para proteger os conteúdos, os dispositivos móveis submetem uma política e o Azure RMS envia-lhes uma licença de publicação e uma chave simétrica para proteger o documento. Para consumir conteúdos, quando os dispositivos móveis se ligam ao serviço do Azure RMS e efetuam a autenticação, os mesmos enviam a política do documento para o Azure RMS e pedem uma licença de utilização para consumir o documento. Em resposta, o Azure RMS envia as chaves e restrições necessárias para os dispositivos móveis. Ambos os processos utilizam o TLS para proteger a troca de chaves e outras comunicações.

-   **Conector RMS**: quando o Azure RMS é utilizado com o conector RMS, os fluxos do processo mantêm-se os mesmos. A única diferença é que o conector funciona como um reencaminhamento entre os serviços no local (como o Exchange Server e o SharePoint Server) e o Azure RMS. O conector propriamente dito não executa quaisquer operações, como a inicialização do ambiente de utilizador, a encriptação ou a desencriptação. Apenas reencaminha a comunicação que normalmente iria para um servidor AD RMS, através do processamento da tradução entre os protocolos que são utilizados em cada lado. Este cenário permite-lhe utilizar o Azure RMS com serviços no local.

-   **Proteção genérica (.pfile)**: quando o Azure RMS protege genericamente um ficheiro, o fluxo é basicamente o mesmo para a proteção de conteúdos com exceção do facto do cliente de RMS criar uma política que concede todos os direitos. Quando o ficheiro é consumido, é desencriptado antes de ser transmitido para a aplicação de destino. Este cenário permite-lhe proteger todos os ficheiros, mesmo que não suportem o RMS originalmente.

-   **PDF protegido (.ppdf)**: quando o Azure RMS protege originalmente um ficheiro do Office, também cria uma cópia desse ficheiro e protege-o da mesma forma. A única diferença é que a cópia do ficheiro está no formato de ficheiro PPDF, que a aplicação de partilha RMS sabe como abrir no modo só de visualização. Este cenário permite-lhe enviar anexos protegidos por e-mail, sabendo que o destinatário num dispositivo móvel poderá sempre lê-los, mesmo que o dispositivo móvel não tenha uma aplicação que suporte ficheiros protegidos do Office de raiz.

## Passos seguintes

Para obter mais informações sobre o Azure RMS, utilize os outros artigos na secção **Compreender e Explorar**, por exemplo [How applications support Azure Rights Management (Como é que as aplicações suportam o Azure Rights Management – em inglês)](applications-support.md) para saber como é que as suas aplicações existentes se podem integrar com o Azure RMS para fornecer uma solução de proteção de informações. 

Consulte a [Terminology for Azure Rights Management (Terminologia do Azure Rights Management – em inglês)](../get-started/terminology.md) para estar familiarizado com os termos que possam ser apresentados quando estiver a configurar e utilizar o Azure RMS e certifique-se de que também consulta os [Requirements for Azure Rights Management (Requisitos para o Azure Rights Management– em inglês)](../get-started/requirements-azure-rms.md) antes de iniciar a implementação. Se quiser começar já a experimentá-lo, utilize o [Tutorial do guia de introdução ao Azure Rights Management](../get-started/quick-start-tutorial.md).

Se estiver pronto para iniciar a implementação do Azure RMS na sua organização, utilize as [Azure Rights Management deployment roadmap (Informações gerais de implementação do Azure Rights Management – em inglês)](../plan-design/deployment-roadmap.md) para obter os passos da sua implementação e ligações para instruções sobre como proceder.

> [!TIP] Para obter ajuda e informações adicionais, utilize os recursos e as ligações em [Informações e suporte do Azure Rights Management](../get-started/information-support.md).


<!--HONumber=Jun16_HO1-->


