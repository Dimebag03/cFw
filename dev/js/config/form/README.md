﻿# Formulários

Existem várias funções para validação de formulários.

- debugando ajax

```
seurl.com.br?debug=true
```

### Usando no boilerplate

* Após criar seu arquivo, insira dentro do `asp:Content` referente ao `<head>` a seguinte Meta Tag:

```
<asp:Content ID="head" ContentPlaceHolderID="head" Runat="Server">
    <meta id="jsPageID" data-value="cfw"/>
</asp:Content>
```

**obs:** você pode iniciar vários módulos, separado-os por vírgula;

```
<meta id="jsPageID" data-value="modulo1,modulo2,modulo3"/>
```

Ou, em seu arquivo JS, relativo a página:

```
define([
    'cfw'
],function(){
    //chame qual plugin desejar
});
```

### Usando em um projeto separado

* Instancie o script do **cFw** na página, antes de fechar o `</body>` com o seguinte código:

```
<script src="http://src.inf.br/cfw/cfw.min.js"></script>
```

### citystate

Inicia os elementos de Cidade/Estados em um formulário;

* iniciando os **estados** por atributos

```
<select data-list="states" data-list-group="1">
    <option>carregando...</option>
</select>
```

* iniciando os **cidades** por atributos

```
<select data-list="cities" data-list-group="1">
    <option>carregando...</option>
</select>
```

* iniciando com **Javascript**

```
cfw.citystate.init({
    filterStates: ['SC,PR,RS'],
    selectState: '#estado1',
    selectCity: '#cidade1',
    initState: 'Santa CaTaRiNa'
});
```
- opções do citystate:
  - **filterStates** : Lista somente os estados indicados;
  - **selectState** : ID ou CLASSE do elemento que receberá os Estados;
  - **selectCity** : ID ou CLASSE do elemento que receberá as Cidades;
  - **initState** : Nome do estado inicialmente selecionado ( nome por extenso ou sigla );

---

### mask

> Documentação Oficial [jQuery Mask](https://github.com/igorescobar/jQuery-Mask-Plugin)

* iniciando com **Javascript**

```
cfw.mask.init();
```

- options (opcional):

```
{
    element: $('.element'),
    mask: '00.000.000/0000-00',
    options: {
        reverse: true,
        selectOnFocus: true
    }
}
```

- opções do mask:
  - **element** : Elemento a ser aplicado a máscara, $('.elemento');
  - **mask** [string] :  com o modelo de máscara ( ex: '00.000.000/0000-00' );
  - **reverse** [bool] :  Preenchimento da máscara da direita para esquerda
  - **selectOnFocus** [bool] : Seleciona todo o valor do campo ao dar o focus

- Iniciando validação das Máscaras por atributos:
- **Datas**
 
```
<input id="abc" type="text" data-mask="date" placeholder="00/00/0000"/>
```

- **CEP**

```
<input type="text" data-mask="zip" placeholder="00000-000"/>
```

- **Dinheiro**

```
<input type="text" data-mask="money" placeholder="0.000,00"/>
```

- **CNPJ**

```
<input class="cnpj" type="text" placeholder="00.000.000/0000-00"/>
```

- **CPF**

```
<input class="cpf" type="text" placeholder="000.000.000-00"/>
```

- **Telefone**

```
<input type="text" class="telefone" placeholder="(00) 00000-0000"/>
```

- **Hora**

```
<input type="text" class="time" placeholder="00:00:00"/>
```

---


### zipCode

Validador de CEP, que também pode preencher o Estado e/ou Cidade apartir dele.

* validação básica

```
<input type="text" data-zipcode="zip"/>
```

**atributos adicionais**

- Grupo de elementos para Autopreenchimento: `data-zipcode-group`

```
<input type="text" data-zipcode="zip" data-zipcode-group="1"/>
```

- Autopreencher o **Endereço** baseado no CEP `data-zipcode="street"`

```
<input type="text" data-zipcode="street" data-zipcode-group="1" />
```

- Autopreencher o **Bairro** baseado no CEP `data-zipcode="district"`

```
<input type="text" data-zipcode="district" data-zipcode-group="1" />
```

- Autopreencher o **Estado** baseado no CEP `data-zipcode="state"`

```
<select data-zipcode="state" data-zipcode-group="1">
    <option>carregando...</option>
</select>
```

- Autopreencher o **Cidade** baseado no CEP `data-zipcode="city"`

```
<select data-zipcode="city" data-zipcode-group="1">
    <option>carregando...</option>
</select>
```

---

### submitForm

Atributo que informa o nome do formulário a ser enviado via Ajax.
- pode ser qualquer elemento

```
<form data-submitform="contato"></form>
````

---

### validateForm

O atributo **data-validate**, torna um elemento obrigatório para validação. Este atributo por sí só, já faz o elemento ser obrigatório.

- validar um campo, mas não torná-lo obrigatório, use o atributo `data-validate-optional`;

```
<input type="qualquer" data-validate-optional="true"/>
```

- posicionar o tooltip no wrapper do elemento;
```
<div class="col6">
    <label>
        <input data-validate-target="div"/>
    </label>
</div> 
```

- validar um `<form>`;

```
<form data-validate="form"></form>
````

- validar um campo do tipo **nome**;

```
<input type="text" data-validate="fullname"/>
````

- validar um campo do tipo **email**;

```
<input type="email" data-validate="email"/>
````

- validar um campo do tipo **cpf**;

```
<input type="text" data-validate="cpf"/>
````

- validar um campo do tipo **cnpj**;

```
<input type="text" data-validate="cnpj"/>
````

- validar um campo do tipo **url**;

```
<input type="text" data-validate="url"/>
````

- validar um campo do tipo **file**;

  > **obs:** os atributos podem ser combinados;

  - validação básica

    ```
    <input type="text" data-validate="file"/>
    ````

  - limitar tamanho de arquivo (em bytes)
    ```
    <input type="text" data-validate="url" data-validate-size="1024"/>
    ````

  - tipo de arquivos permitidos ( separados por vírgula )
    ```
    <input type="text" data-validate="url" data-validate-ext="jpg,rar,zip"/>
    ````    

- validar itens do tipo **checkbox**;

  > **obs:** é preciso do atributo `name`;

  - validação básica

    ```
    <input type="checkbox" name="test" data-validate="checkbox"/>
    ```

  - limitar a quantidade de checkbox marcados ( min, max )
  
    ```
    <input type="checkbox" name="test" data-validate="checkbox" data-validate-qtd="2,2"/>
    <input type="checkbox" name="test"/>
    <input type="checkbox" name="test"/>
    ```

- validar itens do tipo **radio**;

  > **obs:** é preciso do atributo `name`;

  - validação básica

    ```
    <input type="radio" name="test" data-validate="radio" value="sim"/>
    <input type="radio" name="test" data-validate="radio" value="não"/>
    ```

- comparar dois campos `data-validate-group`;

```
<input type="password" data-validate-group="senha"/>
<input type="password" data-validate-group="senha"/>

<input type="email" data-validate-group="email"/>
<input type="email" data-validate-group="email"/>
````
---

### validateFormData

Verifica a compatibilidade dos navegadores sobre o suporte a arquivos `<input type="file"\>`;

- iniciando a validação dos arquivos:

    ```
    cfw.validateformdata.init();
    ```` 

- Caso o [browser](https://whatbrowser.org/) não suporte, uma mensagem é impressa.