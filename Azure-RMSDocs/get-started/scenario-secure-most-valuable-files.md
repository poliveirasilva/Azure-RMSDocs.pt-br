---
# required metadata

title: "Cenário: proteger seus arquivos mais valiosos (alguns) | Azure RMS"
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteger seus arquivos mais valiosos (alguns)

*Aplica-se a: Azure Rights Management, Office 365*

Esse cenário e a documentação do usuário de suporte usam o Azure Rights Management para proteger manualmente e de maneira personalizada alguns arquivos que você identificou como sendo os mais valiosos, o que garante o mais alto nível de proteção contra acesso não autorizado. Geralmente, esses são arquivos que somente algumas pessoas devem poder acessar. Por exemplo, instruções de receita para o produto alimentício que é o carro-chefe da sua empresa ou planos de tomada de controle não devem se tornar públicos antes de uma data especificada.

As instruções são adequadas para o seguinte conjunto de circunstâncias:

-   Você identificou um pequeno conjunto de arquivos a serem protegidos.

-   Os arquivos estão em um dos formatos de arquivo do Office que dão suporte ao Rights Management. Se os arquivos estiverem em outros formatos de arquivo (por exemplo, arquivos CAD), verifique se esses formatos dão suporte ao Azure RMS e implante aplicativos que dão suporte ao Azure RMS nativamente. Para saber mais, confira [Como os aplicativos dão suporte ao Azure Rights Management](https://technet.microsoft.com/library/jj585004.aspx).

-   Os arquivos contêm informações altamente confidenciais que devem ficar acessíveis somente para algumas pessoas.

-   Exigir uma conexão de Internet para autorizar cada acesso individual a um arquivo é uma compensação aceitável para essas pessoas, pois isso fornece maior segurança.

-   Essas pessoas não têm a obrigação de compartilhar essas informações com outras pessoas, mas podem modificá-las e salvar suas alterações.

-   O administrador deve ser capaz de controlar quem está acessando os arquivos e quando, e de revogar o acesso, se necessário.

## Instruções de implantação
![Instruções do administrador para implantação rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Verifique se os requisitos a seguir foram aplicados e siga as instruções para os procedimentos de suporte antes de ir para a documentação do usuário.

## Requisitos para este cenário
Para que este cenário funcione, faça o seguinte:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|Você preparou as contas e os grupos para o Office 365 ou o Active Directory do Azure:<br /><br />- Um grupo habilitado para email nomeado **Acesso privilegiado**, que contém as pessoas que devem ter acesso a esses documentos altamente confidenciais<br /><br />- Um grupo habilitado para email nomeado **Gerenciadores de conformidade de TI**, que contém as pessoas cujo trabalho inclui descoberta automática, monitoramento e auditoria<br /><br />- Um grupo habilitado para email nomeado **Administradores de RMS**, e todos os administradores que configuram o Azure RMS são membros desse grupo|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Você configurou um modelo personalizado conforme descrito a seguir|[Configurando modelos personalizados do Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|O aplicativo de compartilhamento Rights Management é implantado em seu computador Windows para que você possa proteger esses arquivos no local, conforme descrito na próxima seção|[Baixar e instalar o aplicativo Rights Management sharing](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx)|
|Os usuários autorizados têm uma versão mínima do Office 2013|Se os usuários têm o Office 2010, eles também devem instalar o aplicativo de compartilhamento Rights Management.|
|Sua assinatura do Azure RMS inclui rastreamento de documento|Se a sua assinatura do Azure RMS não incluir revogação e acompanhamento de documento, não poderá usar o site de acompanhamento de documento para ver quem está acessando o documento e revogar o acesso, se necessário. Nesse caso, adquira uma assinatura que dê suporte a rastreamento de documentos ou aceite essa limitação. Você também pode considerar os recursos de [log de uso](https://technet.microsoft.com/library/dn529121.aspx) do Azure RMS, que fornece informações como quem acessou cada arquivo e quando, para ajudá-lo a detectar comportamentos potencialmente suspeitos.<br /><br />Para verificar o suporte de assinatura: [Comparação de Ofertas do Rights Management Services (RMS)](https://technet.microsoft.com/dn858608).|

### Para configurar o modelo personalizado

1.  No portal clássico do Azure: crie um novo modelo personalizado para o Azure Rights Management contendo estes valores e configurações:

    -   Nome: **acesso privilegiado**

    -   Direitos: conceder ao grupo habilitado para email **Acesso privilegiado** direitos de **Coautor**

    -   Escopo: selecionar o grupo habilitado para email **Acesso privilegiado**, o grupo habilitado para email **Gerenciadores de conformidade de TI** e o grupo habilitado para email **Administradores RMS**.

    -   Acesso offline: **o conteúdo está disponível apenas com conexão à Internet**

2.  Publique o novo modelo.

### Para proteger o arquivos no local

1.  No Explorador de Arquivos, navegue até a primeira pasta que contém os arquivos que serão protegidos:

    -   Se você deseja proteger todos os arquivos na pasta, selecione a pasta.

    -   Se você deseja proteger apenas alguns arquivos na pasta, selecione os arquivos que serão protegidos.

2.  Clique com o botão direito do mouse, selecione **Proteger com RMS** e **Proteger in-loco**.

3.  Selecione **Acesso privilegiado**.

4.  Suas credenciais não serão solicitadas. Aguarde até que os arquivos sejam protegidos e clique em **Fechar** quando vir a página **Os arquivos foram protegidos**.

5.  Se você tiver mais arquivos para proteger em outras pastas, repita as etapas 1 a 4 para cada pasta.

Para saber mais sobre como proteger os arquivos no local, confira [Proteger um arquivo em um dispositivo (proteger in-loco) usando o aplicativo de compartilhamento Rights Management](https://technet.microsoft.com/library/dn574733%28v=ws.10%29.aspx)

> [!TIP] Se o número de arquivos a proteger um for muito alto para fazê-lo manualmente, considere usar a [ferramenta de proteção RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256) a fim de proteger os arquivos em massa usando o modelo.

### Para monitorar e, se necessário, revogar acesso aos arquivos

1.  No Explorador de Arquivos, clique com o botão direito do mouse, selecione **Proteger com RMS** e selecione **Controlar Uso**:

2.  Se solicitado, entre para acessar o site de acompanhamento de documento.

3.  Verifique quem acessou o arquivo e outros arquivos protegidos, prestando atenção especialmente em tentativas com falha se elas indicarem um comportamento suspeito. Se for apropriado, você pode revogar o acesso arquivo a arquivo.

## Instruções sobre a documentação do usuário
Não há instruções específicas para dar aos usuários nesse cenário porque as bibliotecas protegidas não exigem ações especiais dos usuários. Os arquivos foram protegidos por você e serão monitorados por você. No entanto, talvez você tenha que informar aos usuários e aos seus canais de suporte quais arquivos estão protegidos e como isso pode restringir o uso dos documentos. Por exemplo, se um usuário autorizado não tiver uma conexão de Internet, ela não poderá abrir o arquivo.

Usando o modelo a seguir, copie e cole o anúncio em uma comunicação para seus usuários finais e faça estas modificações:

1.  Forneça os nomes reais dos arquivos ou use uma referência clara que os usuários autorizados irão entender.

2.  Substitua os *&lt;detalhes de contato&gt;* por instruções sobre como esses usuários podem contatar o suporte técnico ou o departamento de TI com um canal de suporte escalonado que corresponda à importância desses documentos. Por exemplo, forneça um número de telefone 24 horas para chamadas de suporte de severidade alta.

3.  Faça modificações adicionais no anúncio, se desejar, e envie-o para esses usuários.

A documentação de exemplo mostra como esse anúncio pode parecer para os usuários depois das personalizações.

![Documentação de usuário do modelo para implantação rápida de RMS do Azure](../media/AzRMS_UsersBanner.png)

### Comunicado de TI: protegendo os documentos secretos da &lt;nome da organização&gt;
Os arquivos a seguir agora têm um nível muito alto de proteção aplicado a eles, para que somente &lt;usuários restritos&gt; possam acessá-los e alterá-los. Para ajudar a protegê-los contra acesso não autorizado, seu aplicativo solicitará autorização automaticamente cada vez que os arquivos forem abertos. Portanto, agora você precisa ter uma conexão com a Internet e suas credenciais poderão ser solicitadas:

-   &lt;principal documento secreto, tipo ou local 1&gt;

-   &lt;principal documento secreto, tipo ou local 2&gt;

-   &lt;principal documento secreto, tipo ou local 3&gt;

**Precisa de ajuda?**

-   Se você não consegue acessar esses arquivos ou observou alterações suspeitas nos arquivos &lt;detalhes de ação e contato&gt;.

#### Documentação do usuário personalizada de exemplo
![Documentação de usuário de exemplo para implantação rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

##### Anúncio de TI: protegendo documentos secretos da VanArsdel
Os arquivos a seguir agora têm um nível muito alto de proteção aplicado a eles, para que somente as pessoas na linha Para dessa mensagem de email possam acessá-los e alterá-los. Para ajudar a protegê-los contra acesso não autorizado, seus aplicativos solicitarão autorização automaticamente cada vez que os arquivos forem abertos. Portanto, agora você precisa ter uma conexão com a Internet para abri-los e suas credenciais poderão ser solicitadas:

-   Especificações de design para o nome do código "Mercury"

-   Especificações de design o nome do código "Jupiter"

-   Especificações de design para o nome do código "Saturn"

-   Especificações de design o nome do código "Neptune"

**Precisa de ajuda?**

-   Se você não consegue acessar esses arquivos ou observou alterações suspeitas nos arquivos, ligue para a linha de escalonamento de suporte 24 horas que foi enviada a você em uma mensagem de email protegido pelo departamento de TI.



<!--HONumber=May16_HO3-->


