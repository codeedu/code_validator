# Code Validator for CPF and CNPJ
>Validador de CPF e CNPJ da Code Education com propósitos educacionais. 

## Como usar
- Você pode instalar via terminal usando Composer:
  
  ```composer 
  composer require codeedu/code_validator:0.0.2 
  ```
  
## Usando com Laravel

Após a instalação, dentro do método **```boot()```** da classe **```AppServiceProvider```** escreva:

```php
public function boot()
{
    \Validator::extend('cpf', function ($attibute, $value, $parameters, $validator) {
        return (new Cpf())->isValid($value); //Para validar CPF.
    });
        
    \Validator::extend('cnpj', function ($attibute, $value, $parameters, $validator) {
        return (new Cpf())->isValid($value); //Para validar CNPJ.
    });
}

```
Lembre-se de importar as classes **```Cpf()```** e **```Cnpj()```**:

```php
<?php

namespace App\Providers;

use Code\Validator\Cpf;   // Importando validador Cpf.
use Code\Validator\Cnpjf; // Importando validador Cnpj.

use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    public function boot()
    {
        // Seu código aqui.
    }

    public function register()
    {
        //
    }
}
```

Logo após já conseguimos usar **```cpf```** e **```cnpj```** como atributo de validação dentro de **```validate()```** como no método ```store()``` abaixo: 

```php
public function store(Request $request)
{
    $validatedData = $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
        'cpf'  => 'required|cpf',  // Validando cpf
        'cnpj' => 'required|cnpj', // Validando cnpj
        
    ]);

    // O post no blog é válido.
}
```

## Créditos
* [codeedu](https://github.com/codeedu)
* [argentinaluiz](https://github.com/argentinaluiz)
