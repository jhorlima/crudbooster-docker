**CRUDBooster - Docker Compose**

_Lembre-se, este projeto requer as portas 80, 3306 e 6379 disponíveis. Se necessário, altere-as no docker-compose.yml_

1 - Clone este repositório para algum diretório:

```sh
git clone https://github.com/jhorlima/crudbooster-docker.git
```

2 - Dentro do diretório, execute:

```sh
docker-compose up -d
```

3 - Após criar os containers, crie um novo projeto Laravel:

```sh
docker-compose exec php composer create-project --prefer-dist laravel/laravel:5.7 ./
```

4 - Crie as chaves exclusivas da sua aplicação Laravel:

```sh
docker-compose exec php php artisan key:generate
```

5 - Abra o navegador, acesse **http://localhost/** e verifique se o Laravel funcionou corretamente.

6 - Agora vamos configurar o idioma e timezone do projeto, então abra o arquivo **app/config/app.php** e edite o **timezone** e **locale**:

```php

[
    /*
    |--------------------------------------------------------------------------
    | Application Timezone
    |--------------------------------------------------------------------------
    |
    | Here you may specify the default timezone for your application, which
    | will be used by the PHP date and date-time functions. We have gone
    | ahead and set this to a sensible default for you out of the box.
    |
    */
    
    'timezone' => 'America/Fortaleza',
    
    /*
    |--------------------------------------------------------------------------
    | Application Locale Configuration
    |--------------------------------------------------------------------------
    |
    | The application locale determines the default locale that will be used
    | by the translation service provider. You are free to set this value
    | to any of the locales which will be supported by the application.
    |
    */
    
    'locale' => 'pt_br',
]
```

Lista de timezone para o Laravel: http://php.net/manual/pt_BR/timezones.america.php

7 - Agora vamos baixar o CRUDBooster para o projeto:

```sh
docker-compose exec php composer require crocodicstudio/crudbooster
```

Tutorial do CRUDBooster: https://github.com/crocodic-studio/crudbooster/blob/master/docs/en/installation.md

8 - Seguindo o tutorial do CRUDBooster, adicione a seguinte classe ao array "providers" no arquivo **app/config/app.php**:

```php
crocodicstudio\crudbooster\CRUDBoosterServiceProvider::class,
```

Ficando assim: 

```php
[
    /*
    |--------------------------------------------------------------------------
    | Autoloaded Service Providers
    |--------------------------------------------------------------------------
    |
    | The service providers listed here will be automatically loaded on the
    | request to your application. Feel free to add your own services to
    | this array to grant expanded functionality to your applications.
    |
    */

    'providers' => [
        /*** Outros providers  ***/
        
        /*
         * CRUDBooster Provider
         */
        crocodicstudio\crudbooster\CRUDBoosterServiceProvider::class,
    ],
]
```

9 - Agora excute o comando para configurar o CRUDBooster e siga os passos no console:

```sh
docker-compose exec php php artisan crudbooster:install
```

10 - Acesse **http://localhost/admin** e depois realize o login com 

- E-mail: admin@crudbooster.com
- Senha: 123456

11 - Pronto!