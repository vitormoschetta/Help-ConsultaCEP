
#### Formulário:

```
<div class="row">
    <div class="row col-12"
        <section class="col col-md-6">
            Cep
            <input type="text" asp-for="Cep" maxlength="9" class="form-control required" onblur="pesquisacep(this.value)" />
        </section>
    </div>

    <div class="row col-12">
        <section class="col col-md-8">
            Rua
            <input type="text" asp-for="Rua" maxlength="150" class="form-control required" />
        </section>
        <section class="col col-md-4">
            Número
            <input type="text" asp-for="Numero" class="form-control" />
        </section>
    </div>

    <div class="row col-12">
        <section class="col col-md-6">
            Complemento
            <input type="text" asp-for="Complemento" maxlength="75" class="form-control" />
        </section>
        <section class="col col-md-6">
            Bairro
            <input type="text" asp-for="Bairro" maxlength="100" class="form-control required" />
        </section>
    </div>

    <div class="row col-12">
        <section class="col col-md-9">
            Cidade
            <input type="text" asp-for="Cidade" maxlength="100" class="form-control required" />
        </section>
        <section class="col col-3">
            UF
            <select asp-for="Uf" maxlength="2" class="custom-select custom-select-sm  required" asp-items="ViewBag.UfId"></select>
        </section>
    </div>
</div>

```


#### Função JavaScript

```
function pesquisacep(valor) 
{
    //Nova variável "cep" somente com dígitos.
    var cep = valor.replace(/\D/g, '');

    //Verifica se campo cep possui valor informado.
    if (cep != "") {

        //Expressão regular para validar o CEP.
        var validacep = /^[0-9]{8}$/;

        //Valida o formato do CEP.
        if(validacep.test(cep)) {
            //Preenche os campos com "..." enquanto consulta webservice.
            document.getElementById('Rua').value="...";
            document.getElementById('Bairro').value="...";
            document.getElementById('Cidade').value="...";
            document.getElementById('Uf').value="...";

            //Cria um elemento javascript.
            var script = document.createElement('script');

            //Sincroniza com o callback.
            script.src = 'https://viacep.com.br/ws/'+ cep + '/json/?callback=meu_callback';

            //Insere script no documento e carrega o conteúdo.
            document.body.appendChild(script);

        } //end if.
        else {
            //cep é inválido.
            limpa_formulário_cep();
            alert("Formato de CEP inválido.");
        }
    } //end if.
    else {
        //cep sem valor, limpa formulário.
        limpa_formulário_cep();
    }
};
```
