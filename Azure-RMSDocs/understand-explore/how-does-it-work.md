---
# required metadata

title: Como funciona o Azure RMS | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
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


# Como funciona o Azure RMS? De modo subjacente

*Aplica-se a: Azure Rights Management, Office 365*

Uma coisa importante a entender sobre como o Azure RMS funciona é que o serviço do Rights Management (e Microsoft) não vê ou armazena seus dados como parte do processo de proteção de informações. As informações que você protege nunca são enviadas ou armazenadas no Azure, a menos que as armazene explicitamente no Azure ou utilize outro serviço de nuvem que as armazene no Azure. O Azure RMS simplesmente transforma os dados em um documento ilegível para qualquer outra pessoa que não sejam os usuários e serviços autorizados:

-   Os dados são criptografados no nível do aplicativo e incluem uma política que define o uso autorizado para esse documento.

-   Quando um documento protegido é utilizado por um usuário legítimo ou é processado por um serviço autorizado, os dados no documento são decifrados e os direitos que são definidos na política são aplicados.

Em um nível alto, você pode ver como esse processo funciona na seguinte imagem. Um documento contendo a fórmula secreta é protegido e depois aberto com sucesso por um usuário ou serviço autorizado. O documento é protegido por uma chave de conteúdo (a chave verde nesta imagem). Ela é única para cada documento e é colocada no cabeçalho do arquivo onde é protegido por sua chave raiz de locatário RMS (a chave vermelha nesta imagem). A chave de locatário pode ser gerada e gerenciada pela Microsoft, ou você pode gerar e gerenciar a sua própria chave de locatário.

Durante o processo de proteção quando o Azure RMS está criptografando e descriptografando, autorizando e impondo restrições, a fórmula secreta nunca é enviada para o Azure.

![Como o Azure RMS protege um arquivo](../media/AzRMS_SecretColaFormula_final.png)

Para obter uma descrição detalhada do que está acontecendo, consulte a seção [Passo a passo de como funciona o Azure RMS: primeiro uso, proteção de conteúdo, consumo de conteúdo](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) neste artigo.

Para obter mais detalhes técnicos sobre os algoritmos e comprimentos de chave que o Azure RMS usa, consulte a próxima seção.

## Controles criptográficos utilizados pelo Azure RMS: Algoritmos e comprimentos de chave
Mesmo que você não precise conhecer como o RMS funciona, podem ser-lhe colocadas perguntas sobre os controlos criptográficos que ele usa, para se certificar de que a proteção de segurança é padrão da indústria.


|Controles de criptografia|Uso no Azure RMS|
|-|-|
|Algoritmo: AES<br /><br />Comprimento da chave: 128 bits e 256 bits [[1]](#footnote-1)|Proteção de documentação|
|Algoritmo: RSA<br /><br />Comprimento da chave: 2048 bits|Proteção de chave|
|SHA-256|Assinatura de certificado|

###### Nota de rodapé 1 

256 bits é usado pelo aplicativo de compartilhamento do Rights Management para proteção genérica e nativa quando o arquivo tem uma extensão de nome de arquivo .ppdf ou é um arquivo de texto ou de imagem protegido (como .ptxt ou .pjpg).

Como as chaves de criptografia são armazenadas e protegidas:

- Para cada documento ou email que é protegido pelo Azure RMS, o Azure RMS cria uma única chave AES (a "chave de conteúdo"), e essa chave é incorporada ao documento e persiste após as edições do documento. 

- A chave de conteúdo é protegida com a chave RSA da organização (a "chave de locatário do Azure RMS") como parte da política no documento, e a política também é assinada pelo autor do documento. Esta chave de locatário é comum a todos os documentos e emails protegidos pelo Azure RMS para a organização e poderá ser alterada somente por um administrador do Azure RMS se a organização estiver usando uma chave de locatário gerenciada pelo cliente (conhecida como BYOK ou "Traga sua própria chave"). 

    Esta chave de locatário é protegida nos serviços online da Microsoft, em um ambiente altamente controlado e sob estrita vigilância. Quando você usar uma BYOK (chave de locatário gerenciada por cliente), esta segurança é reforçada pelo uso de uma matriz de HSMs (módulos de segurança de hardware) de alto nível em cada região do Azure, sem capacidade para que as chaves sejam extraídas, exportadas ou compartilhadas sob quaisquer circunstâncias. Para obter mais informações sobre como gerenciar sua chave de locatário e BYOK, consulte [Planejando e implementando sua chave de locatário do Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

- Licenças e certificados que são enviados a um dispositivo Windows são protegidos com chave privada de dispositivo do cliente, que é criada na primeira vez que um usuário no dispositivo usa o Azure RMS. Esta chave privada, por sua vez, é protegida com a DPAPI do cliente, que protege esses segredos usando uma chave derivada da senha do usuário. Em dispositivos móveis, as chaves são usadas apenas uma vez, então como elas não são armazenadas nos clientes, essas chaves não precisam ser protegidas no dispositivo. 



## Passo a passo de como funciona o Azure RMS: Primeiro uso, proteção de conteúdo, consumo de conteúdo
Para entender mais detalhadamente como o Azure RMS funciona, vamos analisar um fluxo normal após o [serviço do Azure RMS ser ativado](../deploy-use/activate-service.md) e quando um usuário utiliza pela primeira vez o RMS em seu computador Windows (um processo algumas vezes conhecido como **inicialização do ambiente de usuário** ou inicialização), **protege conteúdo** (um documento ou email) e, em seguida, **consome** (abre e usa) o conteúdo que foi protegido por alguém.

Após o ambiente do usuário ser inicializado, o usuário pode, então, proteger documentos ou consumir documentos protegidos nesse computador.

> [!NOTE]
> Se este usuário se desloca para outro computador Windows, ou outro usuário usa esse mesmo computador Windows, o processo de inicialização é repetido.

### Inicializar o ambiente do usuário
Antes que um usuário possa proteger o conteúdo ou consumir conteúdo protegido em um computador Windows, o ambiente do usuário deve estar preparado no dispositivo. Este é um processo de uma única vez e acontece automaticamente, sem intervenção do usuário quando um usuário tenta proteger ou consumir conteúdo protegido:

![Ativação do cliente RMS - etapa 1](../media/AzRMS.png)

**O que acontece na etapa 1**: o cliente RMS no computador conecta-se pela primeira vez ao Azure RMS e autentica o usuário usando a conta do Azure Active Directory.

Quando a conta do usuário é federada com o Azure Active Directory, essa autenticação é automática e as credenciais não são solicitadas ao usuário.|

![Ativação do cliente RMS - etapa 2](../media/AzRMS_useractivation2.png)

**O que acontece na etapa 2**: depois que o usuário é autenticado, a conexão é automaticamente redirecionada para o locatário do RMS da organização, que emite certificados que permitem ao usuário autenticar no Azure RMS para consumir conteúdo protegido e proteger conteúdo offline.

Uma cópia do certificado do usuário é armazenada no Azure RMS para que, se o usuário se desloca para outro dispositivo, os certificados são criados usando as mesmas chaves.

### Proteção de conteúdo
Quando um usuário protege um documento, o cliente RMS realiza as seguintes ações em um documento não protegido:

![Proteção da documentação de RMS – etapa 1](../media/AzRMS_documentprotection1.png)

**O que acontece na etapa 1**: o cliente RMS cria uma chave aleatória (a chave de conteúdo) e criptografa o documento usando essa chave com o algoritmo de criptografia simétrica AES.

![Proteção de documentos do RMS - etapa 2](../media/AzRMS_documentprotection2.png)

**O que acontece na etapa 2**: o cliente RMS cria um certificado que inclui uma política para o documento, com base em um modelo ou especificando direitos específicos para o documento. Esta política inclui os direitos para diferentes usuários ou grupos e outras restrições, como uma data de expiração.

O cliente RMS então usa a chave da organização que foi obtida quando o ambiente de usuário foi inicializado e usa essa chave para criptografar a política e a chave de conteúdo simétrica. O cliente RMS também assina a política com o certificado do usuário que foi obtido quando o ambiente de usuário foi inicializado.|

![Proteção de documentos do RMS – etapa 3](../media/AzRMS_documentprotection3.png)

**O que acontece na etapa 3**: finalmente, o cliente RMS incorpora a política em um arquivo com o corpo do documento criptografado anteriormente, que em conjunto forma um documento protegido.

Este documento pode ser armazenado ou compartilhado em qualquer lugar, usando qualquer método e a política sempre fica com o documento criptografado.

### Consumo de conteúdo
Quando um usuário quer consumir um documento protegido, o cliente RMS começa por solicitar o acesso ao serviço Azure RMS:

![Consumo de documentos de RMS - etapa 1](../media/AzRMS_documentconsumption1.png)

**O que acontece na etapa 1**: o usuário autenticado envia a política de documentos e os certificados do usuário para o Azure RMS. O serviço descriptografa e avalia a política, e cria uma lista de direitos (se houver) que o usuário tem para o documento.

![Consumo da documentação de RMS – etapa 2](../media/AzRMS_documentconsumption2.png)

**O que acontece na etapa 2**: o serviço então extrai a chave de conteúdo AES da política de descriptografada. Esta chave é então criptografada com a chave RSA pública do usuário que foi obtida com o pedido.

A chave de conteúdo recriptografada é então incorporada em uma licença de uso criptografada com a lista de direitos do usuário, que é então devolvida ao cliente RMS.

![Consumo de documento do RMS - etapa 3](../media/AzRMS_documentconsumption3.png)

**O que acontece na etapa 3**: finalmente, o cliente RMS pega a licença de uso criptografada e descriptografa essa licença com sua própria chave privada de usuário. Isso permite que o cliente RMS descriptografe o corpo do documento, uma vez que é necessário e renderiza-o na tela.

O cliente também descriptografa a lista de direitos e passa-a para o aplicativo, que impõe esses direitos na interface do usuário do aplicativo.

### Variações
As orientações anteriores cobrem os cenários normais, mas existem algumas variações:

-   **Dispositivos móveis**: Quando dispositivos móveis protegem ou consomem arquivos com o Azure RMS, os fluxos de processo são muito mais simples. Os dispositivos móveis não passam primeiro pelo processo de inicialização do usuário pois, em vez disso, cada transação (para proteger ou consumir conteúdo) é independente. Tal como acontece com os computadores Windows, os dispositivos móveis se conectam ao serviço do Azure RMS e autenticam. Para proteger o conteúdo, os dispositivos móveis apresentam uma política e o Azure RMS envia-lhes uma licença de publicação e de chave simétrica para proteger o documento. Para consumir o conteúdo, quando os dispositivos móveis se conectam ao serviço do Azure RMS e autenticam, eles enviam a política de documentos ao Azure RMS e solicitam uma licença de uso para consumir o documento. Em resposta, o Azure RMS envia as chaves e restrições necessárias para os dispositivos móveis. Ambos os processos usam TLS para proteger a troca de chaves e outras comunicações.

-   **Conector RMS**: Quando o Azure RMS é utilizado com o conector RMS, os fluxos de processo permanecem os mesmos. A única diferença é que os conectores agem como uma retransmissão entre os serviços no local (como o Exchange Server e SharePoint Server) e o Azure RMS. O conector em si não realiza quaisquer operações, como a inicialização do ambiente do usuário, ou criptografia ou descriptografia. Ele simplesmente retransmite a comunicação que geralmente iria para um servidor AD RMS, manipulando a tradução entre os protocolos que são usados em cada lado. Este cenário permite que você use o Azure RMS com serviços locais.

-   **Proteção genérica (.pfile)**: Quando o Azure RMS protege genericamente um arquivo, o fluxo é basicamente o mesmo para a proteção de conteúdo, exceto que o cliente RMS cria uma política que concede todos os direitos. Quando o arquivo é consumido, ele é descriptografado antes de ser passado para o aplicativo de destino. Este cenário permite proteger todos os arquivos, mesmo que eles não suportem nativamente o RMS.

-   **PDF Protegido (.ppdf)**: Quando o Azure RMS protege nativamente um arquivo do Office, ele também cria uma cópia desse arquivo e protege-o da mesma forma. A única diferença é que a cópia do arquivo está em formato de arquivo PPDF, que o aplicativo de compartilhamento do RMS sabe abrir apenas para visualização. Este cenário permite-lhe enviar anexos protegidos por email, sabendo que o destinatário em um dispositivo móvel sempre será capaz de lê-los, mesmo que o dispositivo móvel não tenha um aplicativo que suporte nativamente arquivos do Office protegidos.

## Próximas etapas

Para saber mais sobre o Azure RMS, use os outros artigos na seção **Compreensão e exploração**, por exemplo, [Como o Azure Rights Management dá suporte para aplicativos](applications-support.md) para saber como integrar seus aplicativos existentes com o Azure RMS para fornecer uma solução de proteção de informações. 

Examine [Terminologia para o Azure Rights Management](../get-started/terminology.md) para se familiarizar com os termos que poderá se deparar ao configurar e usar o Azure RMS e certifique-se também de verificar [Requisitos para o Azure Rights Management](../get-started/requirements-azure-rms.md) antes de iniciar a implantação. Para entrar diretamente e experimentá-lo por conta própria, use o [Tutorial de início rápido do Azure Rights Management](../get-started/quick-start-tutorial.md).

Se estiver pronto para iniciar a implantação do Azure RMS para sua organização, use o [Roteiro de implantação do Azure Rights Management](../plan-design/deployment-roadmap.md) para obter as etapas e os links de implantação das instruções.

> [!TIP]
> Para obter ajuda e informações adicionais, use os recursos e links em [Informações e suporte para o Azure Rights Management](../get-started/information-support.md).


<!--HONumber=Apr16_HO4-->


