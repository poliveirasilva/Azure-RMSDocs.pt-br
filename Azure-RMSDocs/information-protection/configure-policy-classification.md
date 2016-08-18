---
title: "Como configurar condições para classificação automática e recomendada do Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 80c201dcf316a5aa5e123645d47c6741f8b61f05


---

# Como configurar condições para classificação automática e recomendada do Azure Information Protection

>*Aplica-se a: visualização do Azure Information Protection*

**[Estas informações são preliminares e estão sujeitas a alterações. ]**

Ao configurar as condições de um rótulo, você pode atribuir automaticamente um rótulo a um documento ou email. Ou, você pode solicitar que os usuários selecionem o rótulo recomendado: 

- A classificação automática aplica-se ao Word, Excel e PowerPoint quando arquivos são salvos e ao Outlook quando emails são enviados. Você não pode usar a classificação automática de arquivos que já foram rotulados manualmente.
 
- A classificação recomendada aplica-se ao Word, Excel e PowerPoint quando arquivos são salvos.

Ao configurar condições, você pode usar padrões predefinidos, como "Números de cartão de crédito" ou "Número do seguro social dos EUA". Ou, você pode definir uma cadeia de caracteres personalizada ou padrão como uma condição para a classificação automática. Para obter mais informações sobre as condições, consulte a seção [Information about the built-in conditions](#information-about-the-built-in-conditions) (Informações sobre as condições internas).

Como várias condições são avaliadas quando elas se aplicam a mais de um rótulo:

1. Os rótulos são ordenados por avaliação, de acordo com as posições que você especifica na política: o rótulo posicionado primeiro tem a posição mais baixa (menos confidencial) e o rótulo posicionado por último tem a posição mais alta (mais confidencial).

2. O rótulo mais confidencial é aplicado.
 
3. O último sub-rótulo é aplicado.

> [!TIP]
>Para melhorar a experiência do usuário e garantir a continuidade dos negócios, recomendamos que você comece com a classificação recomendada pelo usuário e não pela classificação automática. Essa configuração oferece aos usuários a capacidade de aceitar a ação de rotulagem ou proteção ou de substituir essas sugestões, caso elas não sejam adequadas ao documento ou à mensagem de email.

Um exemplo de aviso que é exibido ao configurar uma condição para aplicar um rótulo como uma ação recomendada, com uma dica de política personalizada:

![Detecção e recomendação do Azure Information Protection](../media/info-protect-recommend-callouts.png)

Neste exemplo, o usuário pode clicar em **Alterar Agora** para aplicar o rótulo recomendado ou substituir a recomendação fechando a barra.

## Para configurar a classificação automática ou recomendada para um rótulo

1. Se você ainda não fez isso, entre no [portal do Azure](https://portal.azure.com) e navegue até a folha **Azure Information Protection**. 
    
    Por exemplo, no menu hub, clique em **Procurar** e comece a digitar **Information** na caixa Filtro. Selecione **Azure Information Protection**.

2. Na folha **Azure Information Protection**, selecione a folha que deseja configurar para classificação automática ou recomendada.

3. Na folha **Rótulo**, na seção **Configurar condições para aplicar este rótulo automaticamente**, clique em **Adicionar uma nova condição**.

4. Na folha **Condição**, selecione **Interno** se desejar usar uma condição predefinida ou **Personalizado** se desejar especificar sua própria condição e, em seguida, clique em **Salvar**:

    - Para **Interno**: selecione na lista de condições disponíveis e, em seguida, selecione o número mínimo de ocorrências e se a ocorrência deve ter um valor exclusivo a ser incluído na contagem de ocorrências.
        
        Para obter mais informações sobre as regras de detecção dessas condições e alguns exemplos, consulte a seção [Information about the built-in conditions](#information-about-the-built-in-conditions) (Informações sobre as condições internas).

    - Para **Personalizado**: especifique um nome e uma frase de correspondência, sem usar aspas e caracteres especiais. Em seguida, especifique se a correspondência deve ocorrer como expressão regular, o uso de diferenciação de maiúsculas e minúsculas, o número mínimo de ocorrências e se a ocorrência deve ter um valor exclusivo a ser incluído na contagem de ocorrências.
        
    **Exemplo de opções de ocorrências**: você seleciona a opção interna de número do seguro social e define o número mínimo de ocorrências como 2, e um documento tem o mesmo número do seguro social listado duas vezes: se você definiu **Contar ocorrências apenas com valores exclusivos** como **Ativado**, a condição não é atendida e, se você definiu essa opção como **Desativado**, a condição é atendida.

5. Na folha **Rótulo**, configure o seguinte e, em seguida, clique em **Salvar**:

    - Escolha a classificação automática ou recomendada: em **Selecionar como esse rótulo é aplicado: automaticamente ou recomendado ao usuário**, selecione **Automático** ou **Recomendado**.

    - Especifique o texto do aviso ao usuário ou da dica de política: mantenha o texto padrão ou especifique sua própria cadeia de caracteres.

6. Para disponibilizar as alterações aos usuários, na folha **Azure Information Protection**, clique em **Publicar**.

## Informações sobre as condições internas

Durante o período de preview, você pode selecionar as seguintes condições:

- [Código SWIFT](#swift-code )

- [Número do Cartão de Crédito](#credit-card-number )

- [Número do banco ABA](#aba-routing-number )

- [SSN (Número do Seguro Social dos EUA)](#usa-social-security-number-ssn)

- [IBAN (Número de Conta Bancária Internacional)](#international-banking-account-number-iban)


### Código SWIFT

Corresponder a este tipo de informação quando o conteúdo incluir o seguinte:  

1. Uma das seguintes frases: **swift**, **swiftnumber**, **swiftroutingnumber** 

2. Um código Swift, em um padrão formatado:  

    a. Quatro letras (código do banco)  

    b. Duas letras (código do país)  

    c. Duas letras ou dígitos (código de localização)  

    d. Opcional, três letras ou dígitos (código da agência)  


Exemplos de teste:

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### Número do Cartão de Crédito

Corresponder a este tipo de informação quando o conteúdo incluir o seguinte:  

- Um número de cartão de crédito válido, em um padrão formatado ou não formatado, aprovado na [verificação de luhn](https://wikipedia.org/wiki/Luhn_algorithm). Este tipo de informação detecta cartões de todas as principais marcas globais, incluindo Visa, MasterCard, Discover Card, American Express e Diners.

    - **Formatado**:
    
        - 16 dígitos: (dddd-dddd-dddd-dddd)  
        
    - **Não formatado**:
    
        - (dddddddddddddddd)  


Exemplos de teste:

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### Número do banco ABA

Corresponder a este tipo de informação quando o conteúdo incluir o seguinte:  

1. Pelo menos uma das seguintes frases: **aba**, **rtn**, **número do banco** 

2. Um número do banco ABA, que inclui 9 dígitos que podem estar em um padrão formatado ou não formatado: 

    - **Formatado**: 
        
        a. Quatro dígitos, começando com 0, 1, 2, 3, 6, 7 ou 8 
        
        b. Um hífen 
        
        c. Quatro dígitos 
        
        d. Um hífen 
        
        e. Um dígito 
        
        Exemplo: 3456-9876-1 ABA 
        
    - **Não formatado**: 
        
        Nove dígitos consecutivos, começando com 0, 1, 2, 3, 6, 7 ou 8 
        
        Exemplo: 345698761 RTN 
 

Exemplos de teste:

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### SSN (Número do Seguro Social dos EUA)

Corresponder a este tipo de informação quando o conteúdo incluir o seguinte:  

1. Pelo menos uma das seguintes frases: **ssn**, **seguro social**, **ssid**, **ss#** 

2. Um número do seguro social: nove dígitos, que podem estar em um padrão formatado ou não formatado:

    - **Formatado**: 
    
        - Nove dígitos no seguinte formato: ddd-dd-dddd ou ddd dd dddd 
        
    - **Não formatado**: 
    
        - Nove dígitos no seguinte formato: ddddddddd 


Exemplos de teste:

- **SSN 123-45-6789**

- **SS# 123456789** 


----

### IBAN (Número de Conta Bancária Internacional)

Corresponder a este tipo de informação quando o conteúdo incluir o seguinte:  

1. A seguinte frase: **IBAN** 

2. Um número IBAN: começa com um código de país (duas letras), em seguida, os dígitos de verificação (dois dígitos) e, em seguida, o número bban (até 30 dígitos, incluindo 30).


Exemplos de teste:

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## Próximas etapas

Para obter mais informações de como configurar a política do Azure Information Protection, use os links na seção [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configurando a política da organização).  






<!--HONumber=Aug16_HO2-->


