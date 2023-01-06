# Proyecto react con TypeScript

En este tutorial continuaremos utilizando el proyecto configurado en el tutorial anterior. En este tutorial agregaremos lo necesario para poder utilizar **TypeScript en un proyecto react** creado con create react app.

Este tutorial está basado en un proyecto creado con create react app, si es una aplicación que no utiliza esta herramienta, la configuración es diferente.

## Agregar TypeScript en create react app

Lo primero es instalar `TypeScript` y los `@types` de las dependencias de react.

```bash
npm install -D typescript @types/node @types/react @types/react-dom @types/jest
```

Una vez instalada las dependencias, podemos **renombrar los archivos** `.jsx`a `.tsx`, reiniciamos el servidor de desarrollo para aplicar los cambios.

Al ejecutar nuevamente la aplicación `npm start`, si no hay ningún problema, se genera de de forma automática el archivo `tsconfig.json`con la configuración predeterminada de nuestro proyecto para TypeScript.

```json
// tsconfig.json

{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "preserve"
  },
  "include": [
    "src"
  ]
}
```

Gracias a create react app, esto es todo lo necesario para iniciar a **trabajar con TypeScript en una aplicación react**.

## Generar un proyecto react con TypeScript y create react app

En la última versión de create react app, ya tenemos la opción de generar un nuevo proyecto con typeScript desde el primer momento, utilizando el siguiente comando:

```bash
npx create-react-app my-new-app --typescript

# o si tienes instalada la herramienta en el sistema

npm  create-react-app my-new-app --typescript
```

Este comando nos genera nuestro proyecto con todos los archivos `.tsx`y **TypeScript** ya configurado

```bash
/my-new-app
  ├── README.md
  ├── package-lock.json
  ├── package.json
  ├── public
  |  ├── favicon.ico
  |  ├── index.html
  |  └── manifest.json
  ├── src
  |  ├── App.css
  |  ├── App.test.tsx
  |  ├── App.tsx
  |  ├── index.css
  |  ├── index.tsx
  |  ├── logo.svg
  |  ├── react-app-env.d.ts
  |  └── serviceWorker.ts
  └── tsconfig.json
```

## Ejemplo componente funcional o sin estado (State less component) con TypeScript

Anteriormente ya instalamos los `@types` que nos dan acceso a los tipos de react, esto los utilizaremos para crear componentes tipados.

He modificado el archivo `App.tsx`, vamos tipar este componente utilizando el tipo `FunctionComponent`, además de tipar sus propiedades utilizando una **Interfaz de TypeScript**.

```js
import React, { FunctionComponent } from 'react';

import './App.scss';

interface IAppProps {
  title?: string
}

const App: FunctionComponent<IAppProps> = (props) => {
  return (
    <div className="App">
      <header className="App-header">
        <h2>{props.title}</h2>
      </header>
    </div>
  );
}

App.defaultProps = {
  title: 'REACT WITH TYPESCRIPT'
}

export default App;
```

## Ejemplo componente de clase con TypeScript

En este caso, podemos tipar tanto, las propiedades como el estado del componente, vamos a ver el componente anterior utilizando una clase.

```js
import React, { Component } from 'react';

import './App.scss';

interface IAppProps {
  title?: string
}

interface IAppState { };

class App extends Component<IAppProps, IAppState> {
  static defaultProps: IAppProps = {
    title: 'REACT WITH TYPESCRIPT'
  }

  render() {
    return (
      <div className="App" >
        <header className="App-header">
          <h2>{this.props.title}</h2>
        </header>
      </div>
    );
  }
}

export default App;
```

## Ejemplo React hooks con TypeScript

Desde la version `16.8` react a incluido los llamados **Hooks**, que tienen como objetivo sustituir las funcionalidades para la que normalmente utilizábamos componentes de clase. Al igual que en los componentes, TypeScript nos puede ayudar a tipar los datos en los Hooks.

Un ejemplo de un componente funcional, **utilizando TypeScript y el Hook** `useState`

```js
// components/Counter

import React, { FunctionComponent, useState } from 'react';

interface ICounterProps {
  title?: string
}

interface ICounterState {
  count: number
}

const initialState: ICounterState = {
  count: 0
}

/**
 * Counter component
 * @param props ICounterProps 
 */
const Counter: FunctionComponent<ICounterProps> = (props) => {
  const [state, setState] = useState<ICounterState>(initialState);

  return (
    <div className="Counter">
      <h2 className="Counter__result">{state.count}</h2>
      <button
        className="Counter__btn Counter__btn--minus"
        type="button"
        onClick={() => setState({ count: state.count - 1 })}
      >-</button>
      <button
        className="Counter__btn Counter__btn--plus"
        type="button"
        onClick={() => setState({ count: state.count + 1 })}
      >+</button>
    </div>
  );
};

export default Counter;
```

Como puedes notar, seguimos aprovechando el tipado de datos, tanto creando **Hook** como **Componentes**.

El tema de los [Hooks](https://reactjs.org/docs/hooks-intro.html) es bastante amplio, intentaré abordar este tema en otro tutorial más adelante.

## Conclusión

Gracias a TypeScript añadimos a JavaScript el potencial de un lenguage de programación tipado.

Hemos visto unos ejemplos de como utilizar **TypeScript** en nuestros componentes o Hooks. No sólo podemos utilizarlos en estos caso, ahora tenemos a nuestra disposición la creación de [distintos tipos de datos](https://www.typescriptlang.org/docs/handbook/basic-types.html) que seguro nos ayudarán mucho en el desarrollo de nuestra aplicación.

Hasta este punto ya tenemos nuetra aplicación configurada para utilizar TypeScript

Espero te haya servido esta breve **configuración de TypeScript en react**.