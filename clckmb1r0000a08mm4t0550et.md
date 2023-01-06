# Configurar Proyecto React con Create react app

El un tutorial anterior he el proceso para **configurar una aplicación react, desde cero**. En esta ocación utilizaremos [create react app](https://facebook.github.io/create-react-app/), una herramienta creada por los desarrolladores de react para facilitar el proceso de configuración inicial.

Para generar un proyecto con **create react app** podemos utilizar npm, instalando la herramienta de forma global en nuestro sistema. (actualmente no recomendado)

## Generar aplicación con create react app y npx

Para generar nuestra aplicación con `npx`ejecutamos el siguiente comando. `bash npx create-react-app create-react-app-tutorial`

Con esto ya generamos nuestra aplicación, lista para empezar a trabajar sin tener que configurar **webpack o babel** como lo hemos hecho en [el tutorial anterior](https://www.gpolanco.com/configurar-react-desde-cero-con-webpack-y-babel/), sólo te centras en el código de tus componentes para aplicación.

## Estructura de proyecto generado

Esta es la estructura generada por el comando ejecutado anteriormente

```bash
create-react-app-tutorial
  ├── README.md
  ├── package.json
  ├── public
  |  ├── favicon.ico
  |  ├── index.html
  |  └── manifest.json
  └── src
     ├── App.css
     ├── App.js
     ├── App.test.js
     ├── index.css
     ├── index.js
     ├── logo.svg
     └── serviceWorker.js
```

Tenemos dos directorios y el archivo `package.json` en el root de la aplicación. Puedes renombrar o eliminar todos los archivos, excepto `public/index.html` y `src/index.js`

Podemos eliminar o renombrar cualquiera de los archivos generados, excepto estos.

* **public/index.html** Es la plantilla unatilizada para renderizar nuestros componentes.
    
* **src/index.js** Es el punto de entrada para webpack.
    
* **package.json** archivo de configuración de npm.
    

Todo el código de nuestra aplicación debe estar ubicado en `src`, ya que, **es el directorio procesado por webpack**, np quiere decir que no puedes crear archivos fuera de este directorio, sólo que, webpack no procesará los archivos fuera de `src`.

## Reestrucurar nuestro directorio SRC

He modificado los siguientes puntos en la aplicación generada originalmente.

* Utilizaremos la extensión `.jsx` en vez de `.js` para los componentes.
    
* He creado el directorio `components` donde alojaremos todos los componentes de la aplicación.
    
* He creado el directorio `assets` donde guardaremos las imágenes y css no específicos de algún componente.
    
* Por ahora no utilizaremos test, con lo cual he eliminado los archivos `.test.js`
    

Así queda el directorio `src` actualmente.

```bash
src
   ├── assets
   |  ├── css
   |  |  └── index.css
   |  └── img
   |     └── logo.svg
   ├── components
   |  └── App
   |     ├── App.css
   |     └── index.jsx
   ├── index.jsx
   └── serviceWorker.js
```

## Configurar SCSS

Creacte react app soporta de forma predeterminada el pre-procesado de `scss`, sólo tenemos que instalar en nuestras dependencias de desarrollo el paquete `node-sass`

```bash
npm install node-sass --save-dev
```

Ahora, podemos renombrar nuestros archivos `.css` por `.scss`y actualizar las referencias en los distintos archivos.

Podemos renombrar el directorio `css` por `scss`. En este directorios crearemos los estilos comunes de la aplicación, por ejemplo el archivo de `variables`

Ahora así queda nuestro directorio `src`

```typescript
 src
   ├── assets
   |  ├── img
   |  |  └── logo.svg
   |  └── scss
   |     ├── _mixins.scss
   |     ├── _variables.scss
   |     └── index.scss
   ├── components
   |  └── App
   |     ├── App.scss
   |     └── index.jsx
   ├── index.jsx
   └── serviceWorker.js
```

Con la configuración actual, para importar el archivo de variables en alguno de nuestros componentes, tendríamos que utilizar la siguiente forma.

```scss
@import 'src/assets/scss/variables';
```

Tenemos la posibilidad de configurar una ruta relativa para los archivos dentro del directorio `assets/scss` utilizando el archivo `.env`y la variable de entorno `SASS_PATH` de la siguiente forma.

```bash
# .env

SASS_PATH=./src/assets/
```

Ahora con esta configuración podemos importar nuestros archivos `.scss` como si estuviésemos dentro del directorio `assets`.

```scss
// importa las variables en cualquier componente
@import 'scss/variables';
```

¿Y si necesitamos importar algún `.scss`desde el directorio `npm`? Para esto, podemos asignar más de un directorio en la variable `SASS_PATH`separando cada path con `:`.

```bash
# .env

SASS_PATH=./src/assets/:node_modules
```

Ahora ya podemos importar archivos `.scss`desde el directorio node\_modules utilizando `~`antes del directorio.

```scss
// Import Bootstrap and its default variables
@import '~bootstrap/scss/bootstrap.scss';
```

## Conclusión

Como has podido notar, todo es más sencillo utilizando [create react app](https://facebook.github.io/create-react-app/) ya que no necesitamos configurar [webpack](https://webpack.js.org/) y [babel](https://babeljs.io/), esta librería hace toda esta configuración por nosotros utilizando internamente el paquete [react-scripts](https://www.npmjs.com/package/react-scripts).

Puedes indagar en el código y ver la [configuración que utiliza create react app](https://github.com/facebook/create-react-app).

Este es un punto de partida para una aplicación reac, en el camino te encontrarás con otras necesidades que tendrás que ir resolviendo sobre la marcha.

En próximos tutoriales seguiremos avanzando utilizando un proyecto real.

Puedes descargar el proyecto desde el [Repositorio en github](https://github.com/gpolanco/Configurar-Proyecto-React-con-Create-react-app)