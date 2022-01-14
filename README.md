<h1 align="center">Ignite Módulo 2 desafio 1: Criando um hook de carrinho de compras</h1>
<img src="https://i.ibb.co/q0VvtmY/cover-reactjs.png" alt="Imagem cover do curso Ignite trilha ReactJS da Rocketseat">

> Segundo desafio do curso Ignite trilha ReactJS da Rocketseat - Modulo 1.

## 💻 Sobre o desafio

Essa será uma aplicação onde o principal objetivo é criar um hook de carrinho de compras. Tendo acesso a duas páginas, um componente e um hook para implementar as funcionalidades pedidas nesse desafio:

- Adicionar um novo produto ao carrinho;
- Remover um produto do carrinho;
- Alterar a quantidade de um produto no carrinho;
- Cálculo dos preços sub-total e total do carrinho;
- Validação de estoque;
- Exibição de mensagens de erro;

### O que deve ser feito

- **components/Header/index.tsx**
<img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F71a7f217-c1bb-426a-8fcc-dfb65db6bb7a%2FUntitled.png?table=block&id=acdec457-aedb-4c92-a020-ee3387283f85&spaceId=08f749ff-d06d-49a8-a488-9846e081b224&width=2000&userId=b6441968-cb3d-42b2-845e-abf10c27a091&cache=v2">
Você deve receber o array cart do hook useCart e mostrar em tela a quantidade de produtos distintos adicionados ao carrinho. Dessa forma, se o carrinho possui 4 unidades do item A e 1 unidade do item B o valor a ser mostrado é 2 itens.

- **pages/Home/index.tsx**
<img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3d320e3c-a052-4f72-994e-aa69617ee85c%2FUntitled.png?table=block&id=c553563e-e14f-4b4d-9f80-b44d96c771b8&spaceId=08f749ff-d06d-49a8-a488-9846e081b224&width=2000&userId=b6441968-cb3d-42b2-845e-abf10c27a091&cache=v2">
Você deve renderizar os produtos buscados da fake API em tela com as informações de título, imagem, preço e quantidade adicionada ao carrinho. Por fim, é preciso implementar a funcionalidade de adicionar o produto escolhido ao carrinho ao clicar no botão `ADICIONAR AO CARRINHO`.
   
   - **cartItemsAmount**: Deve possuir as informações da quantidade de cada produto no carrinho. Sugerimos criar um objeto utilizando reduce onde a chave representa o id do produto e o valor a quantidade do produto no carrinho. Exemplo: se você possuir no carrinho um produto de id 1 e quantidade 4 e outro produto de id 2 e quantidade 3, o objeto ficaria assim:

```javascript
  {
    1: 4,
    2: 3
  }
```

   - **loadProducts**: Deve buscar os produtos da Fake API e formatar o preço utilizando o helper `utils/format`;
   - handleAddProduct: Deve adicionar o produto escolhido ao carrinho.

- **pages/Cart/index.tsx**
<img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa34120df-4046-4a84-8133-6eb987bceac6%2FUntitled.png?table=block&id=4e3c96e5-f7a7-4e1a-9fa9-34d99494047b&spaceId=08f749ff-d06d-49a8-a488-9846e081b224&width=2000&userId=b6441968-cb3d-42b2-845e-abf10c27a091&cache=v2">
Você deve renderizar uma tabela com a imagem, título, preço unitário, quantidade de unidades e preço subtotal de cada produto no carrinho. Além disso, também é preciso renderizar o preço total do carrinho. Por fim, é preciso implementar as funcionalidades dos botões de decrementar, incrementar e remover o produto do carinho.

Nesse arquivo, temos cinco pontos importantes a serem implementados:

   - **cartFormatted**: Deve formatar o carrinho adicionando os campos `priceFormatted` (preço do produto) e `subTotal` (preço do produto multiplicado pela quantidade) ambos devidamente formatados com o `utils/format`;
   - **total:** Deve possuir a informação do valor total do carrinho devidamente formatado com o `utils/format`;
   - **handleProductIncrement**: Deve aumentar em 1 unidade a quantidade do produto escolhido ao carrinho;
   - **handleProductDecrement**: Deve diminuir em 1 unidade a quantidade do produto escolhido ao carrinho, onde o valor mínimo é 1 (nesse caso o botão deve estar desativado);
   - **handleRemoveProduct**: Deve remover o produto escolhido do carrinho.


- **hooks/useCart.tsx**

Apesar de não retornar diretamente nenhuma renderização de elementos na interface como os outros arquivos, esse é o coração do desafio. Ele é responsável por:
   - hook `useCart`;
   - context `CartProvider`;
   - manipular `localStorage`;
   - exibir `toasts`.
   
Então é aqui que você vai implementar as funcionalidades que serão utilizadas pelo restante do app. Os principais pontos são:
   - **cart:** Deve verificar se existe algum registro com o valor `@RocketShoes:cart` e retornar esse valor caso existir. Caso contrário, retornar um array vazio.
   - **addProduct:** Deve adicionar um produto ao carrinho. Porém, é preciso verificar algumas coisas:
     - O valor atualizado do carrinho deve ser perpetuado no **localStorage** utilizando o método `setItem`.
     - Caso o produto já exista no carrinho, não se deve adicionar um novo produto repetido, apenas incrementar em 1 unidade a quantidade;
     - Verificar se existe no estoque a quantidade desejada do produto. Caso contrário, utilizar o método `error` da **react-toastify** com a seguinte mensagem:
```jsx
  toast.error('Quantidade solicitada fora de estoque');
```
    
- Capturar utilizando `trycatch` os erros que ocorrerem ao longo do método e, no catch, utilizar o método `error` da **react-toastify** com a seguinte mensagem:

```jsx
  toast.error('Erro na adição do produto');
```

- **removeProduct:** Deve remover um produto do carrinho. Porém, é preciso verificar algumas coisas:
    - O valor atualizado do carrinho deve ser perpetuado no **localStorage** utilizando o método `setItem`.
    - Capturar utilizando `trycatch` os erros que ocorrerem ao longo do método e, no catch, utilizar o método `error` da **react-toastify** com a seguinte mensagem:
    
    ```jsx
    toast.error('Erro na remoção do produto');
    ```
    
- **updateProductAmount:** Deve atualizar a quantidade de um produto no carrinho. Porém, é preciso verificar algumas coisas:
    - O valor atualizado do carrinho deve ser perpetuado no **localStorage** utilizando o método `setItem`.
    - Se a quantidade do produto for menor ou igual a zero, sair da função **updateProductAmount** instantaneamente.
    - Verificar se existe no estoque a quantidade desejada do produto. Caso contrário, utilizar o método `error` da **react-toastify** com a seguinte mensagem:
    
```jsx
  toast.error('Quantidade solicitada fora de estoque');
```
    
- Capturar utilizando `trycatch` os erros que ocorrerem ao longo do método e, no catch, utilizar o método `error` da **react-toastify** com a seguinte mensagem:
    
```jsx
  toast.error('Erro na alteração de quantidade do produto');
```
    
    
### Como deve ficar a aplicação ao final?

Link para vídeo demonstrativo: <a href="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f166455c-a42f-4d25-8baa-a6686a3cb476/challenge.mp4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220112%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220112T223818Z&X-Amz-Expires=86400&X-Amz-Signature=f0b388a9c93454498ae8f0cd374251eeeead5cf616c18d2f4997f446deef7fa4&X-Amz-SignedHeaders=host&x-id=GetObject" target="_blank">Clique aqui</a>.

## 🧬 Técnologias utilizadas

Este projeto foi desenvolvido utilizando as seguintes tecnologias:


- [React](https://reactjs.org)
- [Json-server](https://www.npmjs.com/package/json-server)
- [TypeScript](https://www.typescriptlang.org/)
- localStorage API
- [React-Toastfy](https://github.com/fkhadra/react-toastify#readme)

## 💻 Pré-requisitos

Antes de começar, verifique se você atendeu aos seguintes requisitos:
* Você instalou a versão estável mais recente de [Node](https://nodejs.org/en/)
* Você instalou a versão mais recente de [Yarn](https://yarnpkg.com/)

## 🚀 Instalando

Clone o repositório:
```bash
$ git clone git@github.com:xDouglas90/ignite-react-mod2-challenge-1.git
```

- Entre na pasta do repositório clonado e no terminal:
```bash
$ yarn install ou npm install
$ yarn server ou npm run server
$ yarn start ou npm start
```


## ☕ Utilizando a aplicação

Agora basta abrir em um navegador: <a href="http://localhost:3000/" target="_blank">http://localhost:8080/</a>, para visualizar a aplicação funcionando.

Para visualizar o conteúdo da Fake API: <a href="http://localhost:3333/" target="_blank">http://localhost:3333/</a>

## 📝 License

Este projeto está sob a licença MIT. Veja mais detalhes no arquivo [LICENSE](https://github.com/xdouglas90/ignite-react-challenge-2/blob/main/LICENSE.md).

