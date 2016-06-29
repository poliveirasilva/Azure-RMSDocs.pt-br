---
# required metadata

title: Cenário – Os executivos trocam informações privilegiadas em segurança | Azure RMS
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

# Cenário – Os executivos trocam informações privilegiadas em segurança

*Aplica-se a: Azure Rights Management, Office 365*

Este cenário e a documentação do utilizador associada utilizam o Azure Rights Management para que os executivos possam trocar em segurança e-mails e anexos por e-mail e as políticas restrinjam automaticamente o acesso dos executivos sem necessidade de ação especial por parte deles. Os e-mails e quaisquer anexos serão automaticamente protegidos pelo Azure Rights Management.

Se necessário, pode adicionar uma exceção à regra, tal como a abreviatura DNP (de “Não Proteger”) no assunto da mensagem de e-mail, para que os executivos a possam especificar caso necessitem de enviar um e-mail desprotegido para outros executivos, por exemplo, para rever antes de reencaminhar para outras pessoas.

As instruções aplicam-se às seguintes circunstâncias:

-   Os executivos partilham entre si informações confidenciais que não devem ser partilhadas com outras pessoas.

-   Os executivos não necessitam de fazer nada de forma diferente quando enviam estes e-mails, exceto enviá-los para um endereço de e-mail de trabalho em vez de um endereço de e-mail pessoal.

-   Os executivos têm uma forma de contornar a regra se alguma vez precisarem de enviar uma mensagem de e-mail desprotegida para outros executivos.

## Instruções de Implementação
![Instruções do administrador para a Implementação Rápida do Azure RMS](../media/AzRMS_AdminBanner.png)

Certifique-se de que os seguintes requisitos são cumpridos e, em seguida, siga as instruções dos procedimentos de suporte antes de avançar para a documentação do utilizador.

## Requisitos para este cenário
Para que as instruções para este cenário funcionem, é necessário o seguinte:

|Requisito|Se precisar de mais informações|
|---------------|--------------------------------|
|Preparou contas e grupos para o Office 365 ou o Azure Active Directory:<br /><br />- Um grupo com capacidade de correio com o nome **Executivos** e todos os executivos são membros deste grupo<br /><br />- Um grupo com capacidade de correio com o nome **Administradores de RMS** e todos os administradores que irão configurar o Azure RMS são membros deste grupo|[Preparar para o Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|A chave de inquilino do Azure Rights Management é gerida pela Microsoft; não está a utilizar o BYOK|[Planear e implementar a chave de inquilino do Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|O Azure Rights Management está ativado|[Ativar o Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Uma das seguintes configurações:<br /><br />- O Exchange Online está ativado para o Azure Rights Management<br /><br />- O conetor RMS está instalado e configurado para o Exchange no local|Para o Exchange Online: consulte a secção **Exchange Online: Configuração de IRM** em [Configurar aplicações do Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx).<br /><br />Para o Exchange no local: [Implementar o conector Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Configurou um modelo personalizado, tal como descrito a seguir|[Configurar modelos personalizados para o Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|Configurou uma regra de proteção de transporte para IRM, conforme descrito mais à frente neste artigo|Para o Exchange Online: [Criar uma Regra de Proteção de Transporte](https://technet.microsoft.com/library/dd302432.aspx)<br /><br />Para o Exchange 2013: [Criar uma Regra de Proteção de Transporte](https://technet.microsoft.com/en-us/library/dd302432%28v=exchg.150%29.asp)<br /><br />Para o Exchange 2010: [Criar uma Regra de Proteção de Transporte](https://technet.microsoft.com/en-us/library/dd302432%28v=exchg.141%29.aspx)|

### Para configurar o modelo personalizado para executivos

1.  No portal clássico do Azure: crie um novo modelo personalizado para o Azure Rights Management que contenha estes valores e definições:

    -   Nome: **Executivos**

    -   Direitos: conceda ao grupo **Executivos** com capacidade de correio direitos de **Coproprietário**

    -   Âmbito: selecione o grupo **Executivos** com capacidade de correio e o grupo **Administradores de RMS** com capacidade de correio.

2.  Publique o novo modelo.

3.  Apenas para o Exchange Online: atualize os modelos utilizando o seguinte comando do Windows PowerShell para o Exchange Online:

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### Para configurar a regra de transporte para IRM

-   Utilize a documentação do Exchange referenciada na tabela para obter informações sobre os procedimentos para criar a regra de transporte com as seguintes definições:

    -   Nome: **Aplicar os modelos Executivos a e-mail executivos**

    -   Especifique o grupo **Executivos** como o remetente e o destinatário da regra e da condição adicional.

    -   Para a ação, selecione **Aplicar proteção de direitos à mensagem com** e, em seguida, selecione o modelo **Executivos** que configurou.

    -   Adicione a exceção de **DNP** (como uma abreviatura de “Não Proteger”) ou a sua opção de palavras para identificar esta exceção, para ser incluída no assunto.

    -   Certifique-se de que a regra está configurada para **Impor**.

## Instruções da documentação do utilizador
A não ser que pretenda fornecer instruções sobre como especificar **DNP** ou a sua opção de palavras ou expressões da exceção no assunto do e-mail, não existem instruções sobre procedimentos a dar aos utilizadores para este cenário, uma vez que proteger e-mails de e para executivos não requer qualquer ação especial por parte deles. As mensagens de e-mail e quaisquer anexos são automaticamente protegidos para que apenas os membros do grupo Executivos possam aceder aos mesmos.

No entanto, poderá ter de informar os executivos e o suporte técnico de que estes e-mails serão automaticamente protegidos e sobre a forma como tal pode restringir a utilização dos mesmos. Por exemplo, se os e-mails ou os anexos forem reencaminhados para outras pessoas mais tarde, estas não os conseguirão ler. Se tiver configurado a exceção DNP (ou equivalente), certifique-se de que o suporte técnico está ciente desta configuração para que os próprios executivos possam contornar a regra, sem necessidade de ação por parte de um administrador do Exchange.

Utilizando o modelo seguinte, copie e cole o anúncio numa comunicação destinada aos utilizadores finais e efetue estas alterações para refletir o seu ambiente:

1.  Substitua as instâncias de *&lt;nome da organização&gt;* pelo nome da sua organização.

2.  Caso tenha optado por uma cadeia diferente de DNP para a isenção, substitua esse valor e a explicação em conformidade.

3.  Substitua *&lt;domíniodee-mail&gt;* pelo nome de domínio de e-mail da sua organização.

4.  Substitua *&lt;detalhes de contacto&gt;* por instruções sobre como os utilizadores podem contactar o suporte técnico, tais como uma ligação para um site, um endereço de e-mail ou um número de telefone.

5.  Efetue quaisquer modificações adicionais que pretenda ao anúncio e, em seguida, envie-o aos utilizadores.

A documentação de exemplo mostra que aspeto este anúncio poderá ter para os utilizadores depois das personalizações.

![Modelo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_UsersBanner.png)

### Anúncio de TI: os e-mails executivos da &lt;nome da organização&gt; são agora automaticamente protegidos
A partir de agora, sempre que enviar e-mails para outro executivo da &lt;nome da organização&gt; na empresa, os conteúdos desses e-mails e quaisquer anexos serão automaticamente protegidos de forma a que apenas outro executivo da empresa lhes possa aceder para ler as respetivas informações, imprimi-los, copiá-los, etc. Esta restrição aplica-se mesmo que reencaminhe a mensagem de e-mail para outras pessoas ou guarde os anexos. Esta proteção ajuda a evitar a perda de dados de informações confidenciais e delicadas.

Tenha em atenção que, se pretender que outras pessoas que não sejam executivos da &lt;nome da organização&gt; possam ler e editar as informações que envia nestes e-mails, tem de as enviar separadamente para essas pessoas. Em alternativa, para contornar a proteção automática, escreva as letras **DNP** (como uma abreviatura de Não Proteger) em qualquer parte do assunto da mensagem de e-mail.

Ao enviar informações confidenciais da empresa para outro executivo da &lt;nome da organização&gt;, não se esqueça de as enviar para o respetivo endereço de e-mail de trabalho (*nome*@&lt;domíniodee-mail&gt;) e não para um endereço de e-mail pessoal.

**Precisa de ajuda?**

-   Contacte o suporte técnico: &lt;detalhes de contacto&gt;

### Exemplo de documentação do utilizador
![Exemplo de documentação do utilizador para a Implementação Rápida do Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Anúncio de TI: os e-mails executivos da VanArsdel são agora automaticamente protegidos
A partir de agora, sempre que enviar e-mails para outro executivo da VanArsdel na empresa, os conteúdos desses e-mails e quaisquer anexos serão automaticamente protegidos de forma a que apenas outro executivo da empresa possa aceder aos mesmos para ler as respetivas informações, imprimi-los, copiá-los, etc. Esta restrição aplica-se mesmo que reencaminhe a mensagem de e-mail para outras pessoas ou guarde os anexos. Esta proteção ajuda a evitar a perda de dados de informações confidenciais e delicadas.

Tenha em atenção que, se pretender que outras pessoas que não sejam executivos da VanArsdel possam ler e editar as informações que envia nestes e-mails, tem de as enviar separadamente para essas pessoas. Em alternativa, para contornar a proteção automática, escreva as letras **DNP** (como uma abreviatura de Não Proteger) em qualquer parte do assunto da mensagem de e-mail.

Ao enviar informações confidenciais da empresa para outro executivo da VanArsdel, não se esqueça de as enviar para o respetivo endereço de e-mail de trabalho (*nome*@vanarsdelltd.com) e não para um endereço de e-mail pessoal.

**Precisa de ajuda?**

-   Contacte o suporte técnico: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO3-->


