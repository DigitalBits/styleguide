# DigitalBits JavaScript Style Guide 

*A nossa abordagem de JavaScript*


## <a name='table-of-contents'>Índice</a>

  1. [Tipos](#types)
  1. [Objetos](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Funções](#functions)
  1. [Propriedades](#properties)
  1. [Variáveis](#variables)
  1. [Expressões Condicionais & Comparações](#comparison-operators--equality)
  1. [Blocos](#blocks)
  1. [Espaços em branco](#whitespace)
  1. [Vírgulas](#commas)
  1. [Ponto e vírgulas](#semicolons)
  1. [Casting & Coerção de Tipos](#type-casting--coercion)
  1. [Convenções de nomenclatura](#naming-conventions)
  1. [Métodos Acessores](#accessors)
  1. [jQuery](#jquery)


## <a name='types'>Tipos</a>

  - **Primitivos**: Quando você acessa um tipo primitivo você lida diretamente com seu valor. `string`, `number`, `boolean`, `null`, `undefined`

    ```javascript
    var numbers = 1;
    var integers = numbers;

    integers = 9;

    console.log(numbers, integers); // => 1, 9
    ```
  - **Complexos**: Quando você acessa um tipo complexo você lida com a referência para seu valor. `object`, `array`, `function`

    ```javascript
    var numbers = [1, 2];
    var integers = numbers;

    integers[0] = 9;

    console.log(numbers[0], integers[0]); // => 9, 9
    ```

**[⬆ voltar ao topo](#table-of-contents)**

## <a name='objects'>Objetos</a>

  - Use a sintaxe literal para criação de objetos.

    ```javascript
    // ruim
    var item = new Object();

    // bom
    var item = {};
    ```

  - Não use [palavras reservadas](http://es5.github.io/#x7.6.1) como chaves.

    ```javascript
    // ruim
    var superman = {
      default: { clark: 'kent' },
      private: true
    };

    // bom
    var superman = {
      defaults: { clark: 'kent' },
      hidden: true
    };
    ```

  - Use sinônimos legíveis no lugar de palavras reservadas.

    ```javascript
    // ruim
    var superman = {
      class: 'alien'
    };

    // ruim
    var superman = {
      klass: 'alien'
    };

    // bom
    var superman = {
      type: 'alien'
    };
    ```

**[⬆ voltar ao topo](#table-of-contents)**

## <a name='arrays'>Arrays</a>

  - Use a sintaxe literal para a criação de Arrays.

    ```javascript
    // ruim
    var items = new Array();

    // bom
    var items = [];
    ```

  - Use Array.push() ao inves de atribuir um item diretamente ao array.

    ```javascript
    var someStack = [];


    // ruim
    someStack[someStack.length] = 'abracadabra';

    // bom
    someStack.push('abracadabra');
    ```

  - Quando precisar copiar um Array utilize Array.slice().

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // ruim
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // bom
    itemsCopy = items.slice();
    ```

 - Para converter um objeto similar a um array para array, utilize Object.keys() + Array.map().

    ```javascript
    var cars = {
        porsche: 134,
        ferrari: 70,
        lamborghini: 35
    }
    
    // bom: quando apenas as propriedades são importantes
    cars = Object.keys(cars);
    
    // bom: quando o conteúdo também for necessário
    cars = Object.keys(cars).map(function(key) {
        return {
            model: key,
            amount: cars[key]
        };
    });
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='strings'>Strings</a>

  - Use aspas simples `''` para strings

    ```javascript
    // ruim
    var name = "Elon Musk";

    // bom
    var name = 'Elon Musk';

    // ruim
    var fullName = "Elon " + lastName;

    // bom
    var fullName = 'Elon ' + lastName;
    ```

  - Strings maiores que 80 caracteres devem ser escritas em múltiplas linhas e usar concatenação.

    ```javascript
    // ruim
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // ruim
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // bom
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

  - Quando for construir uma string programaticamente, use sempre concatenação de strings.     

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='functions'>Funções</a>

  - Ao declarar Funções sempre use funções nomeadas:

    ```javascript
    // ruim, função anônima
    var anonymous = function() {
      return true;
    };

    // bom, função nomeada
    function named() {
      return true;
    };
    ```

  - Nunca declare uma função em um escopo que não seja de uma função (ou seja, dentro de if, while, etc). A ECMA-262 define um `bloco` como uma lista de instruções. A declaração de uma função não é uma instrução. [Leia em ECMA-262's](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // ruim
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }
    ```
    
- Nunca nomeie um parâmetro como `arguments`. Isso sobrescrevá o objeto `arguments` que é passado para cada função.

    ```javascript
    // evite as funções imediatamente invocada (IIFE)
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    
    // em vez disso, declare e chame em seguida.
    function greetings() {
        console.log('Welcome to the Internet. Please follow me.');
    }

    greetings();
    ```
    
- Nunca nomeie um parâmetro como `arguments`. Isso sobrescrevá o objeto `arguments` que é passado para cada função.

    ```javascript
    // ruim
    function nope(name, options, arguments) {
      // ...outras implementações...
    }

    // bom
    function yup(name, options, args) {
      // ...outras implementações...
    }
    ```

**[⬆ voltar ao topo](#table-of-contents)**



## <a name='properties'>Propriedades </a>

  - Use ponto `.` para acessar propriedades.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    // ruim
    var isJedi = luke['jedi'];

    // bom
    var isJedi = luke.jedi;
    ```

  - Use colchetes `[]` para acessar propriedades através de uma variável.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='variables'>Variáveis</a>

  - Sempre use `var` para declarar variáveis. Não fazer isso irá resultar em variáveis globais. Devemos evitar poluir o namespace global.

    ```javascript
    // ruim
    superPower = new SuperPower();

    // bom
    var superPower = new SuperPower();
    ```

  - Sempre use a declaração `var`, inclusive para múltiplas variáveis, sempre declarando uma variável em cada linha.

    ```javascript
    // ruim
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bom
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';    
    ```

  - Declare as variáveis que você não vai estipular valor primeiro, se possível seguindo um ordem crescente do tamanho de caracteres por linha.

    ```javascript
    // ruim
    var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // ruim
    var i, items = getItems();
    var dragonball;
    var goSportsTeam = true;
    var len;

    // bom
    var i;
    var length;
    var dragonball;
    var items = getItems();
    var goSportsTeam = true;
    ```

  - Defina variáveis no topo do escopo onde ela se encontra.

    ```javascript
    // ruim
    function() {
      test();

      //..outras implementações..

      var name = getName();

      return name;
    }

    // bom
    function() {
      var name = getName();

      //..outras implementações..

      test();

      return name;
    }
    ```

**[⬆ voltar ao topo](#table-of-contents)**



## <a name='comparison-operators--equality'>Expressões Condicionais & Comparações</a>

  - Use `===` e `!==` ao invés de `==` e `!=`.
  - Expressões condicionais são interpretadas usando coerção de tipos e seguem as seguintes regras:

    + **Objeto** equivale a **true**
    + **Undefined** equivale a **false**
    + **Null** equivale a **false**
    + **Booleans** equivalem a **o valor do boolean**
    + **Numbers** equivalem a **false** se **+0, -0, or NaN**, se não **true**
    + **Strings** equivalem a **false** se são vazias `''`, se não **true**

    ```javascript
    if ([0]) {
      // true
      // Um array é um objeto, objetos equivalem a `true`.
    }
    ```

 - Use atalhos. (Para mais informações veja [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) por Angus Croll)

    ```javascript
    // ruim
    if (name !== '') {
      // ...outras implementações...
    }

    // bom
    if (name) {
      // ...outras implementações...
    }

    // ruim
    if (collection.length > 0) {
      // ...outras implementações...
    }

    // bom
    if (collection.length) {
      // ...outras implementações...
    }
    ```


**[⬆ voltar ao topo](#table-of-contents)**


## <a name='blocks'>Blocos</a>

  - Sempre use chaves para todos os blocos, inclusive quando houver apenas uma linha.

    ```javascript
    // ruim
    if (test)
      return false;

    // ruim
    if (test) return false;

    // bom
    if (test) {
      return false;
    }

    // ruim
    function() { return false; }

    // bom
    function() {
      return false;
    }
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='whitespace'>Espaços em branco</a>

  - Use tabs com 4 espaços

    ```javascript
    // ruim
    function() {
    ∙∙var name;
    }

    // ruim
    function() {
    ∙var name;
    }

    // bom
    function() {
    ∙∙∙∙var name;
    }
    ```

  - Coloque um espaço antes da chave que abre o escopo da função.

    ```javascript
    // ruim
    function test(){
      console.log('test');
    }

    // bom
    function test() {
      console.log('test');
    }

    // ruim
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });

    // bom
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });
    ```

  - Coloque 1 espaço antes do parênteses de abertura de comandos de controle (`if`, `while` etc.). Não coloque espaços antes da lista de argumentos em chamadas e declarações de funções.

    ```javascript
    // ruim
    if(isJedi) {
      fight ();
    }

    // bom
    if (isJedi) {
      fight();
    }

    // ruim
    function fight () {
      console.log ('Swooosh!');
    }

    // bom
    function fight() {
      console.log('Swooosh!');
    }
    ```

  - Colocar espaço entre operadores.

    ```javascript
    // ruim
    var x=y+5;

    // bom
    var x = y + 5;
    ```

  - Coloque uma linha em branco no final do arquivo.

  - Deixar uma linha em branco depois de blocos e antes da próxima declaração

    ```javascript
    // ruim
    if (foo) {
      return bar;
    }
    return baz;

    // bom
    if (foo) {
      return bar;
    }

    return baz;

    // ruim
    var obj = {
      foo: function() {
      },
      bar: function() {
      }
    };
    return obj;

    // bom
    var obj = {
      foo: function() {
      },
      bar: function() {
      }
    };

    return obj;
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='commas'>Vírgulas</a>

  - Leading commas: **Não.**

    ```javascript
    // ruim
    var story = [
        once
      , upon
      , aTime
    ];

    // bom
    var story = [once, upon, aTime];

    // ruim
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // bom
    var hero = {
      firstName: 'Bob',
      lastName: 'Parr',
      heroName: 'Mr. Incredible',
      superPower: 'strength'
    };
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='semicolons'>Ponto e vírgula</a>

  - **Sempre.**

    ```javascript
    // ruim
    var name = 'Skywalker'
    return name
    

    // bom
    var name = 'Skywalker';
    return name;


    ```

    [Leia mais](http://stackoverflow.com/a/7365214/1712802).

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='type-casting--coercion'>Casting & Coerção de tipos</a>

  - Faça coerção de tipos no inicio da expressão.

  - Strings:

    ```javascript
    var reviewScore = 9;

    // ruim
    var totalScore = reviewScore + '';

    // bom
    var totalScore = '' + reviewScore;

    // ruim
    var totalScore = '' + reviewScore + ' total score';

    // bom
    var totalScore = reviewScore + ' total score';
    ```

  - Inteiros: use `~~` em vez de `parseInt`. A principal vantagem é que valores não-númericos serão retornados como `0` em vez de `NaN`.
    
    ```javascript
    var inputValue = '4';

    // ruim
    var val = new Number(inputValue);


    // ruim
    var val = inputValue >> 0;

    // ruim
    var val = parseInt(inputValue);

    // ruim
    var val = Number(inputValue);

    // bom
    var val = ~~inputValue;
    ```


  - **Nota:** O operador ~~ retorna valores inteiros de 32-bit ([fonte](http://es5.github.io/#x11.7)). O que pode levar a um comportamento inesperado para valores inteiros maiores que 32 bits. O maior valor Integer signed 32-bit é 2.147.483.647,

    ```javascript
    ~~'2147483647' //=> 2147483647
    ~~'2147483648' //=> -2147483648
    ~~'2147483649' //=> -2147483647
    ```

  - Booleans: use `!!`

    ```javascript
    var age = 0;

    // ruim
    var hasAge = new Boolean(age);

    // ruim
    var hasAge = Boolean(age);

    // bom
    var hasAge = !!age;
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='naming-conventions'>Convenções de nomenclatura</a>

  - Não use apenas um caracter, seja descritivo.

    ```javascript
    // ruim
    function q() {
      // ...outras implementações...
    }

    // bom
    function query() {
      // ...outras implementações...
    }
    ```

  - Use camelCase quando for nomear objetos, funções e instâncias.

    ```javascript
    // ruim
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    function c() {}
    var u = new user({
      name: 'Bob Parr'
    });

    // bom
    var thisIsMyObject = {};
    function thisIsMyFunction() {}
    var user = new User({
      name: 'Bob Parr'
    });
    ```

  - Use PascalCase quando for nomear módulos, libs ou classes.

    ```javascript
    // ruim
    var utils = require('./utils');
    var userModel = require('../models/user');

    // bom
    var Utils = require('./utils');
    var UserModel = require('../models/user');
    ```

  - Use um underscore `_` para colunas de banco de dados e propriedades que são transportadas via HTTP (REST Payload).

    ```javascript
    // ruim
    res.json({
      status: 'success',
      data: {
        name: 'Lucas',
        motherName: 'Maria',
        fatherName: 'Pedro'
      }
    });

    // bom
    res.json({
      status: 'success',
      data: {
        name: 'Lucas',
        mother_name: 'Maria',
        father_name: 'Pedro'
      }
    });
    ```



  - **Nota:** IE8 ou inferior mostra alguns problemas com funções nomeadas. Veja [http://kangax.github.io/nfe/](http://kangax.github.io/nfe/) para mais informações.

  - Se seu arquivos exporta apenas uma classes, o nome do arquivo deve conter exatamento o nome da classe.

    ```javascript
    // conteúdo do arquivo
    class CheckBox {
      // ...
    }
    module.exports = CheckBox;

    // em outro arquivo
    // ruim
    var CheckBox = require('./checkBox');

    // ruim
    var CheckBox = require('./check_box');

    // bom
    var CheckBox = require('./CheckBox');
    ```

**[⬆ voltar ao topo](#table-of-contents)**


## <a name='accessors'>Métodos Acessores</a>

  - Métodos acessores de propriedades não são obrigatórios.
  - Se você vai criar métodos acessores utilize getVal() e setVal('hello')

    ```javascript
    // ruim
    dragon.age();

    // bom
    dragon.getAge();

    // ruim
    dragon.age(25);

    // bom
    dragon.setAge(25);
    ```

  - Se a propriedade é um boolean, use isVal() ou hasVal()

    ```javascript
    // ruim
    if (!dragon.age()) {
      // something
    }

    // bom
    if (!dragon.hasAge()) {
      // something
    }
    ```


**[⬆ voltar ao topo](#table-of-contents)**



## <a name='jquery'>jQuery</a>

  - Use `jQuery` em vez de `$`.

    ```javascript
    // ruim
    $('.sidebar').click();

    // bom
    jQuery('.sidebar').click();
    ```


**[⬆ voltar ao topo](#table-of-contents)**

