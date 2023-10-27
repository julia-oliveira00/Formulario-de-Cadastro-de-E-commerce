<h1 align="center">Formulario de Cadastro</h1>
<p align="center">Um site de Cadastro E-commerce que puxa o endereço pelo cep inserido usando <code>json</code> e <code>strictmode</code></p>

<h1 align="center">Introdução</h1>
![](img/Captura%20de%20tela%202023-10-27%20091603.png)
<p align="center">Assim que você inserir o email será direcionado para a segunda página</p>

![](img/Captura%20de%20tela%202023-10-27%20091727.png)
<p align="center">Neste momento seram adicionadas as demais informações juntamente com o CEP que se digitado corretamente preencherá o restante das informações</p>

___

<h3 align="center">Em que casos o site não retorna as informações esperadas?</h3>

* Caso o usuário clique em cadastrar ou na tecla enter a vizualização das informações previamente não será possivel.
* Caso o cep esteja errado, incompleto ou eceder o numero de caracteres o site emitira um aviso e o site não retornará as informações.

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

<h1 align="center">Referencias utilizadas</h1>

![https://www.boticario.com.br/autenticacao/login?nextPath=%2Fminha-conta%2F](img/Captura%20de%20tela%202023-10-27%20092514.png)