## Javascript array método find

![Javascript array método find](https://cdn.hashnode.com/res/hashnode/image/upload/v1660207349425/8lW6Nz4BU.png)

El método **find pertenece al objeto Array,** fue introducido en **[ECMAScript 2015 (ES6)](http://www.ecma-international.org/ecma-262/6.0/)**, actualmente ya soportado por todos los navegadores modernos.

Como su nombre indica, **busca un elemento dentro de un array** y retorna el primero que cumpla con la condición especificada en la **función callback**.

Sintaxis del método Array.find()
--------------------------------

    const result = array.find((currentValue, index, array) => {...},thisValue)

La constante _result_ contendrá el **valor de elemento encontrado** o `undefined` si no encuentra ningún elemento

**El método find en javascript recibe 2 parámetros**, el primero es una función que **se ejecuta con cada item del array**. El segundo es el valor de `this` que se utilizará dentro de la función (opcional).

### Parámetros del método find

*   **`function`**: función que se ejecuta con cada elemento del Array hasta que alguno de los elementos es encontrado.
*   **`currentValue`**: Elemento actual del Array. (_opcional_)
*   `**index**`: Es el índice del elemento actual, dentro del Array. (_opcional_)
*   **`array`:** Array original sobre el que se hace la búsqueda. (_opcional_)
*   **`thisValue`**: si pasa un valor se utilizará como él `this` dentro de  la función, es decir, permite cambiar el contexto del `this` interno de la función. (_opcional_)

### Return value

Retorna **el valor del primer elemento** de la matriz, **que cumple la condición de búsqueda** implementada en la función callback. De lo contrario retorna `undefined`

Dentro de la función se debe implementar la lógica de búsqueda y siempre retornar un valor que será evaluado como un booleano (true o false)

Como utilizar el método find
----------------------------

Para los siguientes ejemplos utilizaremos el siguiente Array de usuarios

    const users = [
      {
        id: 1,
        name: "Leanne Graham",
        username: "Bret",
      },
      {
        id: 2,
        name: "Ervin Howell",
        username: "Antonette",
      },
      {
        id: 3,
        name: "Clementine Bauch",
        username: "Samantha",
      },
      {
        id: 4,
        name: "Patricia Lebsack",
        username: "Karianne",
      },
    ];

Como es un Array de objetos, podemos buscar un usuario basado en cualquiera de sus propiedades.

**Buscamos el usuario con ID 7**

    const user = users.find(user => user.id === 7);

En este caso, `user` será `undefined` porque no existe un usuario con `id === 7`

**Combinando con el método includes() del Objeto string**

Para hacer búsquedas más avanzadas, podemos combinar con los métodos existentes para el trabajo con `string` que nos brinda javascript.

Por ejemplo, podemos buscar un usuario **que su nombre incluya el valor \`Bauch\`** utilizando el método **String.includes()**

    const user = users(user => user.name.includes('Bauch');

En este caso el método find, **retornará el primer usuario que en la propiedad `name` incluya el valor** `**Bauch**`

> Siempre es cnveniente verificar el valor resultante antes de utilizarlo, ya que este puede ser `undefined`.

    if(user) {
        // existe, puedo usarlo sin problemas
    }

Implementación del método find con un bucle for
-----------------------------------------------

Si no existiera este método, tendríamos que hacer esta búsqueda utilizando un bucle. Este es un ejemplo de como podríamos implementarlo.

    let user; // Por defecto es undefined
    
    for (let i = 0; i < users.length; i++) {
      const item = users[i];
      if (item.name.includes('Bauch')) {
        user = item;
        break;
      }
    }

Como podemos ver, el método find nos brinda una forma amigable de hacer una búsqueda dentro de un Array de cualquier tipo en javascript.

Conclusión
----------

Como hemos podido ver, el método find del objeto Array es muy simple de utilizar y es una ayuda enorme a la hora de hacer búsquedas y comprobar la existencia de valores en los Array de javascript.

¡Espero que haya sido de utilidad!