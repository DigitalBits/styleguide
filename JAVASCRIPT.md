# DigitalBits JavaScript Style Guide 

*A nossa abordagem de JavaScript*


## <a name='table-of-contents'>Índice</a>

  1. [Tipos](#types)
  1. [Objetos](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Funções](#functions)
  1. [Propriedades](#properties)


## <a name='types'>Tipos</a>

  - **Primitivos**: Quando você acessa um tipo primitivo você lida diretamente com seu valor.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var numbers = 1;
    var integers = numbers;

    integers = 9;

    console.log(numbers, integers); // => 1, 9
    ```
  - **Complexos**: Quando você acessa um tipo complexo você lida com a referência para seu valor.

    + `object`
    + `array`
    + `function`

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

