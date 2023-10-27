<h1 align="center">Formulario de Cadastro</h1>
<p align="center">Um site de Cadastro E-commerce que puxa o endereço pelo cep inserido usando <code>json</code> e <code>strictmode</code></p>

# Introdução


___

<h1 align="center">Códigos Java Script</h1>

```js
"use strict"; //Strict mode
// https://viacep.com.br/

//Função para limpar formulário
//Arrow function
const limparFormulario = () => {
    document.getElementById('rua').value = '';
    document.getElementById('bairro').value = '';
    document.getElementById('cidade').value = '';
    document.getElementById('estado').value = '';
}
```
```js
//verifica se CEP é válido
const eNumero = (numero) => /^[0-9]+$/.test(numero);
const cepValido = (cep) => cep.length == 8 && eNumero(cep);

//Responsável pelo preenchimento do formulário
const preencherFormulario = (endereco) => {
    document.getElementById('rua').value = endereco.logradouro;
    document.getElementById('bairro').value = endereco.bairro;
    document.getElementById('cidade').value = endereco.localidade;
    document.getElementById('estado').value = endereco.uf;
}
```
```js
//Função para o consumo de API da via cep
const pesquisaCep = async() => {
    limparFormulario();
    const url = `http://viacep.com.br/ws/${cep.value}/json/`;

    if (cepValido(cep.value)) {
        const dados = await fetch(url); //esperar
        const address = await dados.json(); //retornar dados no formato JSON

        if (address.hasOwnProperty("erro")) {
            alert("CEP não encontrado");
        } else {
            preencherFormulario(address);
        }
    } else {
        alert("CEP incorreto");
    }
}
```
```js
//Adiciona um evento DOM no input do CEP
document.getElementById('cep').addEventListener('focusout', pesquisaCep);
```
<h1 align="center">Tecnologias utilizadas</h1>

* <code>HTML5</code>
* <code>BOOTSTRAP 5.3.2</code>
* <code>JAVASCRIPT</code>
