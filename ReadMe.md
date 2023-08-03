#   REACT

<details>

<summary
><strong
> React Redux 
<br
/>
Redux é uma biblioteca JavaScript de código aberto para gerenciar o estado do aplicativo. É mais comumente usado com bibliotecas como React ou Angular para criar interfaces de usuário. Semelhante (e inspirado) pela arquitetura Flux do Facebook, foi criado por Dan Abramov e Andrew Clark.
</summary>

<br
/>

## Primeiro passo

#### If you use npm:

``` .
npm install @reduxjs/toolkit react-redux
```

#### Or if you use Yarn:

``` .
yarn add @reduxjs/toolkit react-redux
```

### Criar uma Store

Crie um arquivo `store.js` ou `Store/index.js` para isso:

``` .
import { configureStore } from '@reduxjs/toolkit';

import rootReducer from './reducers'; // Crie os seus reducers em './reducers'

const store = configureStore({
  reducer: rootReducer,
});

export default store;

```

#### Observação

<p
> Uma "Store" é o centro do Redux, onde o estado global do aplicativo é mantido. Você precisa criar uma store que conterá o estado e o reducer (caso ainda não tenha definido).
</p>

## Segundo passo

<p
> Reducers são funções que especificam como o estado do aplicativo muda em resposta a uma ação. Você pode criar um ou mais reducers que são combinados no rootReducer, que será utilizado na criação da store. Crie uma pasta reducers na mesma pasta em que criou o arquivo store.js e crie seus reducers lá.

> Exemplo de um reducer básico (counterReducer.js):
</p>

### Criar o Reducers

<!-- /src/provider/ThemeProvider.js -->
<p
>

``` .
  const initialState = {
    count: 0,
  };

  const counterReducer = (state = initialState, action) => {
    switch (action.type) {
    case 'INCREMENT':
      return { ...state, count: state.count + 1 };
    case 'DECREMENT':
      return { ...state, count: state.count - 1 };
    default:
      return state;
  }
};

export default counterReducer;
```

</p>

<!-- <h4
> Observação </h4>

<p
> No código acima, estamos utilizando a prop children de forma que o componente ThemeProvider encapsule todos os componentes-filho. Isso significa que os componentes aninhados serão embrulhados pelo ThemeContext.Provider e poderão acessar os dados do Context.
</p> -->

## Terceiro passo

### Combinar reducers:

<p
> Se você tiver vários reducers, precisará combiná-los usando a função combineReducers do Redux. Isso permite que você crie um único rootReducer que será passado à função createStore.

> Exemplo de rootReducer.js:
</p>

<p
>

``` .
import { combineReducers } from 'redux';
import counterReducer from './counterReducer';

const rootReducer = combineReducers({
  counter: counterReducer,
  // Adicione outros reducers aqui, se houver
});

export default rootReducer;
```

</p>

## Quarto passo

### Conectar o Redux à aplicação React:

<p
> Agora, você precisa conectar o Redux à sua aplicação React para que os componentes possam acessar o estado global e despachar ações para alterá-lo. Isso é feito usando o componente Provider do react-redux. No arquivo `index.js` ou `main.tsx` (ou outro arquivo raiz da sua aplicação),  importe o Provider, configure a store e envolva o componente raiz da sua aplicação com ele:

</p>

<p
>

``` .
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store'; // Importe a store que você criou anteriormente
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

```

</p>

## Quinto passo

### Utilizar o estado global e despachar ações:

<p
> Agora você pode utilizar o estado global em seus componentes e despachar ações para alterá-lo. Para fazer isso, utilize os hooks useSelector e useDispatch fornecidos pelo react-redux. Importe-os e utilize-os nos componentes onde você deseja acessar ou atualizar o estado global.

> Exemplo de um componente que usa o estado global:

</p>

<p
>

``` .
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';

const CounterComponent = () => {
  const count = useSelector(state => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>Decrement</button>
    </div>
  );
};

export default CounterComponent;

```

</p>

</details>
