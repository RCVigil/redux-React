#   REACT

<details>
<strong>Check List Redux 
<br
/>

Esta Check List é para auxiliar a instalação correta do Redux.

## Antes de começar:
`[ ]` Pensar como será o formato de seu estado global.
`[ ]` Pensar quais actions serão necessárias em sua aplicação.

<br/>

### Instalação:
`[ ]` npm install –save redux react-redux;
`[ ]` npm install –save @redux-devtools/extension

<br/>

### Criar dentro do diretório src:
`[ ]` Diretório redux.

<br/>

### Criar dentro do diretório redux:
`[ ]` Diretório actions.
`[ ]` Diretório reducers.
`[ ]` Arquivo index.ts.

<br/>

### Criar dentro do diretório actions:
`[ ]` Arquivo index.ts.

<br/>

### Criar dentro do diretório reducers:
`[ ]` Arquivo index.ts.

<br/>

### Criar dentro do arquivo redux/index.ts:
`[ ]` Importar o createStore.
`[ ]` Configurar o Redux DevTools.
`[ ]` Importar o rootReducer.
`[ ]` Criar e exportar a store.

<br/>

### Dentro do arquivo redux/reducers/index.ts:
`[ ]` Criar estado inicial.
`[ ]` Criar função reducer com switch retornando apenas a opção default.
`[ ]` Criar rootReducer usando o combineReducers.
`[ ]` Exportar rootReducer.

<br/>

### No arquivo ./src/main.tsx:
`[ ]` Importar a store.
`[ ]` Importar o Provider para fornecer os estados a todos os componentes encapsulados pelo <App />.

  Exemplo:

  Na importação

  ``` .
  import { Provider } from 'react-redux';
  import store from './redux'
  ```

  <br/>

  No render

  ``` .
  <Provider store={ store } >
    <App />
  </Provider>
  ```

  <br/>

  ### No arquivo redux/actions/index.ts:
`[ ]` Criar e exportar os actionTypes.
Exemplo:

  ACTIONS TYPES

``` .
  export const ADD_EMAIL = 'ADD_EMAIL';
```

`[ ]` Criar e export os actions creators necessários.
Exemplo:

  ACTIONS CREATORS

``` .
  export const addEmail = (email) => ({
    type: ADD_EMAIL,
    email,
  })
```

### Nos reducers:
`[ ]` Criar os casos para cada action criada, retornando o devido estado atualizado.

### Nos componentes que irão ler o estado:
`[ ]` Importar o hook useSelector da biblioteca react-redux.
Exemplo:

  No import

``` .
  import { useSelector } from 'react-redux';
```

  No componente antes do Render

``` .
  const rootState = useSelector((state: RootState) => state);
```

### Nos componentes que modificarão o estado:
`[ ]` Importar o hook useDispatch da biblioteca react-redux.
Exemplo:

  No import

``` .
  import { useDispatch } from 'react-redux';
```

  No componente antes do Render

``` .
  const dispatch = useDispatch();
```

</details>

<br/>

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

Crie um arquivo `store.js` ou `Redux/index.js` para isso:

``` .
import { configureStore } from "@reduxjs/toolkit";

import rootReducer from "./rootReducer"; // Crie os seus reducers em './reducers'

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

</p>

### Criar o Reducers

<!-- /src/provider/ThemeProvider.js -->
<p
>

> Criar um arquivo com nome: openModalProdReducer.ts

``` .
import { AnyAction } from "redux";

const initialStateModal = {
  open: null,
};

const openModalProdReducer = (state = initialStateModal, action: AnyAction) => {
  switch (action.type) {
    case "OPEN_MODAL":
      return { ...state, open: action.payload };
    case "CLOSE_MODAL":
      return { ...state, open: null };
    default:
      return state;
  }
};

export default openModalProdReducer;
```

</p>

## Terceiro passo

### Combinar reducers:

<p
> Se você tiver vários reducers, precisará combiná-los usando a função combineReducers do Redux. Isso permite que você crie um único rootReducer que será passado à função createStore.

> Exemplo de rootReducer.ts:
</p>

<p
>

``` .
import { combineReducers } from "redux";
import openModalProdReducer from "./OpenModal/OpenModalProduction";

const rootReducer = combineReducers({
  modal: openModalProdReducer,
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
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.tsx";

import store from "../src/Redux/store.ts";
import { Provider } from "react-redux";

import "./index.css";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
);
```

</p>

## Quinto passo

### Gerar as Actions que serão usadas no Dispatch():

<p
> A action é um objeto ou uma função que envia uma ação ao reducer, o qual realizará uma alteração no estado global.

> Exemplo de um componente que retorna a lógica do estado, aqui separa estado por estado cada um deve ter o seu:

</p>

<p
>

``` .
export const openModal = (payload: any) => {
  return { type: "OPEN_MODAL", payload };
};

export const closeModal = () => {
  return { type: "CLOSE_MODAL" };
};
```

</p>

## Sexto passo

### Utilizar o estado global e despachar ações:

<p
> Agora você pode utilizar o estado global em seus componentes e despachar ações para alterá-lo. Para fazer isso, utilize os hooks useSelector e useDispatch fornecidos pelo react-redux. Importe-os e utilize-os nos componentes onde você deseja acessar ou atualizar o estado global.

> Exemplo de um componente que usa o estado global:

</p>

<p
>

``` .
import React from "react";
import { productionImages } from "../../../images/ImagesAndVideos/ImagesAndVideos";
import "./_production.sass";
import SummerModal from "../../modais/ModalBeer";

import { useSelector, useDispatch } from "react-redux";
import { openModal, closeModal } from "../../../Redux/modalActions"; // Importe os criadores de ação corretamente

const Production: React.FC = () => {
  const modalOpen = useSelector((state: any) => state.modal.open);
  const dispatch = useDispatch();

  const imageClick = (event: React.MouseEvent<HTMLDivElement>) => {
    const { accessKey } = event.currentTarget.dataset;
    if (accessKey) {
      dispatch(openModal(accessKey)); // Dispatch da ação 'openModal'
    }
  };

  const imagesVerify = productionImages.filter((img) => img.image !== "");

  const handleCloseModal = () => {
    dispatch(closeModal()); // Dispatch da ação 'closeModal'
  };

  return (
    <div id="firstDivProduction">
      {imagesVerify &&
        imagesVerify.map((img, index) => (
          <div
            key={`${img.id}-${index}`}
            className={`imagemProduction img-${img.id}-${index}`}
            onClick={imageClick}
            data-access-key={img.name}
          >
            <img
              className="imgProduction"
              src={img.image}
              alt={`Imagem da cerveja ${img.name}`}
            />
          </div>
        ))}
      {modalOpen && (
        <SummerModal
          beer={modalOpen}
          open={true}
          handleClose={handleCloseModal}
        />
      )}
    </div>
  );
};

export default Production;
```

</p>

</details>
