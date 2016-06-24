---
# required metadata

title: Cenário - Executivos trocam informações privilegiadas de maneira segura | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cenário - Executivos trocam informações privilegiadas de maneira segura

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação de usuário de suporte usam o Azure Rights Management para que os executivos possam trocar emails e anexos por email entre si com segurança e para que políticas restrinjam automaticamente o acesso para os executivos sem exigir ações especiais da parte deles. Os emails e anexos serão automaticamente protegidos pelo Azure Rights Management.

Se for necessário, você pode adicionar uma exceção à regra, como a abreviação de DNP (para "Do Not Protect" ou Não proteja) no assunto do email, para que os executivos possam especificar isso se precisarem enviar um email desprotegido para outros executivos, por exemplo, para examinar antes de encaminhar para outras pessoas.

As instruções são adequadas para o seguinte conjunto de circunstâncias:

-   Os executivos compartilham entre si informações confidenciais que não devem ser compartilhadas com outras pessoas.

-   Os executivos não precisam fazer algo diferente ao enviar esses emails, exceto enviá-los a um endereço de email de trabalho em vez de um endereço de email pessoal.

-   Os executivos podem substituir a regra por conta própria se algum dia precisarem enviar um email desprotegido para outros executivos.

## Instruções de implantação
![Instruções do administrador para implantação rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Verifique se os requisitos a seguir foram aplicados e siga as instruções para os procedimentos de suporte antes de ir para a documentação do usuário.

## Requisitos para este cenário
Para que as instruções desse cenário funcionem, deve ser feito o seguinte:

|Requisito|Se você precisar de mais informações|
|---------------|--------------------------------|
|Você preparou as contas e os grupos para o Office 365 ou o Active Directory do Azure:<br /><br />- Um grupo habilitado para email nomeado **Executivos**, e todos os executivos são membros desse grupo<br /><br />- Um grupo habilitado para email nomeado **Administradores de RMS**, e todos os administradores que configuram o Azure RMS são membros desse grupo|[Preparando o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Sua chave de locatário do Azure Rights Management é gerenciada pela Microsoft. Você não está usando BYOK|[Planejando e implementando sua chave de locatário do Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|O Azure Rights Management está ativado|[Ativando o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Uma destas configurações:<br /><br />- O Exchange Online está habilitado para o Azure Rights Management<br /><br />- O conector RMS está instalado e configurado para o Exchange local|Para o Exchange Online: confira a seção **Exchange Online: configuração do IRM** em [Configuração de aplicativos para o Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx).<br /><br />Para o Exchange local: [Implantação do conector do Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx).|
|Você configurou um modelo personalizado conforme descrito a seguir|[Configurando modelos personalizados do Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|Você configurou uma regra de proteção de transporte para IRM, conforme descrito posteriormente neste artigo|Para o Exchange Online: [Criar uma Regra de proteção de transporte](https://technet.microsoft.com/library/dd302432.aspx)<br /><br />Para o Exchange 2013: [Criar uma Regra de proteção de transporte](https://technet.microsoft.com/en-us/library/dd302432%28v=exchg.150%29.asp)<br /><br />Para o Exchange 2010: [Criar uma Regra de proteção de transporte](https://technet.microsoft.com/en-us/library/dd302432%28v=exchg.141%29.aspx)|

### Para configurar o modelo personalizado para executivos

1.  No portal clássico do Azure: crie um novo modelo personalizado para o Azure Rights Management contendo estes valores e configurações:

    -   Nome: **Executivos**

    -   Direitos: conceda ao grupo habilitado para email **Executivos** direitos de **Coproprietário**

    -   Escopo: selecione o grupo habilitado para email **Executivos** e o grupo habilitado para email **Administradores de RMS**.

2.  Publique o novo modelo.

3.  Somente para o Exchange Online: Atualize os modelos usando o comando do Windows PowerShell para Exchange Online:

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### Para configurar a regra de transporte para IRM

-   Use a documentação do Exchange citada na tabela para obter informações de procedimentos a fim de criar a regra de transporte com as seguintes configurações:

    -   Nome: **Aplique os modelos Executivos aos emails de executivos**

    -   Especifique o grupo **Executivos** como o remetente e o destinatário da regra e condição adicional.

    -   Para a ação, selecione **Aplicar proteção de direitos à mensagem com** e, em seguida, selecione o modelo **Executivos** que você configurou.

    -   Adicione a exceção de **DNP** (como uma abreviação para "Do Not Protect" ou Não proteja), ou palavras de sua preferência para identificar essa exceção, a ser incluída no assunto.

    -   Verifique se a regra está configurada para **Impor**.

## Instruções sobre a documentação do usuário
A menos que queira fornecer instruções sobre como especificar **DNP** ou palavras ou frases de sua preferência no assunto do email, não haverá quaisquer instruções de procedimentos a serem enviadas aos usuários para esse cenário, pois a proteção de emails entre os executivos não exige uma ação especial da parte deles. As mensagens de email e os anexos são protegidos automaticamente. Assim, apenas os membros do grupo Executivos podem acessá-los.

No entanto, talvez seja necessário informar aos executivos e a seu suporte técnico que os emails serão automaticamente protegidos e como isso pode restringir o uso dos emails. Por exemplo, eles não poderão ser lidos com êxito por outras pessoas se os emails ou os anexos forem encaminhados mais tarde para outros destinatários. Se você tiver configurado a exceção DNP (ou equivalente), avise o suporte técnico sobre essa configuração para que os executivos possam substituir a regra por conta própria, sem a necessidade de ação por parte de um administrador do Exchange.

Usando o modelo a seguir, copie e cole o anúncio em uma comunicação para seus usuários finais e faça com que essas modificações reflitam o seu ambiente:

1.  Substitua as instâncias de *&lt;nome da organização&gt;* pelo nome de sua organização.

2.  Se você escolher uma cadeia de caracteres diferente de DNP para a isenção, substitua o valor e a explicação adequadamente.

3.  Substitua *&lt;emaildomain&gt;* pelo nome de domínio de email de sua organização.

4.  Substitua *&lt;detalhes de contato&gt;* por instruções de como os usuários podem entrar em contato com o suporte técnico, como um link de site, endereço de email ou número de telefone.

5.  Faça modificações adicionais no anúncio, se desejar, e envie-o para esses usuários.

A documentação de exemplo mostra como esse anúncio pode parecer para os usuários depois das personalizações.

![Documentação de usuário do modelo para implantação rápida de RMS do Azure](../media/AzRMS_UsersBanner.png)

### Comunicado de TI: os emails de executivos de &lt;Nome da organização&gt; agora são protegidos automaticamente
De agora em diante, sempre que você enviar emails a outro executivo da &lt;nome da organização&gt; o conteúdo dos emails e os anexos serão automaticamente protegidos para que apenas outro executivo da empresa possa acessá-los para ler as informações, imprimi-los, copiá-los e assim por diante. Essa restrição se aplica mesmo se você encaminhar a mensagem de email a outras pessoas ou salvar os anexos. Essa proteção ajuda a impedir a perda de dados de informações confidenciais e sigilosas.

Observe que, se você quiser que outras pessoas que não sejam executivos da &lt;nome da organização&gt; possam ler e editar as informações enviadas nesses emails, você deverá enviá-los por email separadamente. Ou, para substituir a proteção automática, digite as letras **DNP** (uma abreviação Do Not Protect, ou Não proteja) em qualquer lugar no assunto do email.

Ao enviar informações confidenciais da empresa a outro executivo da &lt;nome da organização&gt;, lembre-se de enviá-las ao seu endereço de email de trabalho (*nome*@&lt;emaildomain&gt;), e não a um endereço de email pessoal.

**Precisa de ajuda?**

-   Entre em contato com o suporte técnico: &lt;detalhes do contato&gt;

### Documentação do usuário de exemplo
![Documentação de usuário de exemplo para implantação rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Anúncio de TI: Os emails de executivos da VanArsdel agora são protegidos automaticamente
De agora em diante, sempre que você enviar emails a outro executivo da VanArsdel, o conteúdo dos emails e os anexos serão automaticamente protegidos para que apenas outro executivo da empresa possa acessá-los para ler as informações, imprimi-los, copiá-los e assim por diante. Essa restrição se aplica mesmo se você encaminhar a mensagem de email a outras pessoas ou salvar os anexos. Essa proteção ajuda a impedir a perda de dados de informações confidenciais e sigilosas.

Observe que se você quiser que outras pessoas que não sejam executivos da VanArsdel possam ler e editar as informações enviadas nesses emails, você deverá enviá-los por email separadamente. Ou, para substituir a proteção automática, digite as letras **DNP** (uma abreviação Do Not Protect, ou Não proteja) em qualquer lugar no assunto do email.

Ao enviar informações confidenciais da empresa a outro executivo da VanArsdel, lembre-se de enviá-las a seu endereço de email de trabalho (*nome*@vanarsdelltd.com), não a um endereço de email pessoal.

**Precisa de ajuda?**

-   Contate o suporte técnico: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO3-->


