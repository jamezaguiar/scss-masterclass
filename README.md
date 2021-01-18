# Sintaxe SCSS

## Partials

- Código SCSS contendo parte de uma estilização
- O arquivo é criado com \_ na frente
  - Ex: `_name.scss`

## Import

- Podemos importar código SCSS vindo de outro arquivo, um _partial_
- Ex: `@import 'name'`

## Variáveis

- Podemos criar variáveis para armazenar certos valores
  ```scss
  $text-color: white;
  ```
- Variáveis em SCSS respeitam o escopo no qual elas foram declaradas. [Ver Encadeamento](#Encadeamento)

## Encadeamento

- Podemos encadear código no SCSS, por exemplo
  - Temos uma `div` com um `h1` dentro
    ```html
    <div>
      <h1>Some Text!</h1>
    </div>
    ```
    No SCSS podemos:
    ```scss
    div: {
      h1: {
        color: $text-color;
      }
    }
    ```

## Mixin e Include

- Podemos criar blocos de código SCSS que pode ser reutilizado com `@mixin`

  ```scss
  @mixin box-shadow($color) {
    // ...
    box-shadow: 3px 3px 4px -2px $color;
    // ...
  }

  .container {
    @include box-shadow(rgba(0, 0, 0, 0.6));
  }
  ```

  Todo código que estiver dentro do `mixin` _box-shadow_ será aplicado no `.container`

## If, If Else e Else

- Para criar condicionais:
  ```scss
  @mixin text-effect($type) {
    @if $type == danger {
      color: red;
    } @else if $type == alert {
      color: yellow;
    } @else {
      color: black;
    }
  }
  ```

## For e Each

- Imagine que temos o seguinte código HTML:
  ```html
  <div class="container">
    <p class="text-1">Something</p>
    <p class="text-2">Something</p>
    <p class="text-3">Something</p>
    <p class="text-4">Something</p>
    <p class="text-5">Something</p>
  </div>
  ```
- No nosso SCSS, podemos estilizar estes elementos de acordo com o número dentro da classe, usando um laço de repetição:

  ```scss
  @for $i from 1 through 5 {
    .text-#{$i} {
      font-size: 15px * $i;
    }
  }
  ```

- Também podemos criar coleções dentro do código e percorrer usando `each`:

  ```scss
  $colors: (
    color1: blue,
    color2: red,
    color3: yellow
  );

  @each $key, $color in $colors {
    .#{$color}-text {
      color: $color;
    }
  }
  ```

## Funções

- Podemos usar funções que já existem dentro do SCSS

  ```scss
  p {
    color: lighten($color, 25); // Clarear texto
    color: darken($color, 25); // Escurecer texto
  }
  ```

## Herança

- Podemos fazer com que elementos herdem propriedades de outros, exemplo:

  ```scss
  .flex {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  body {
    @extend .flex;
    flex-direction: column;
  }
  ```

## Referência

- Usamos & para referenciar o elemento do escopo atual

  ```scss
  p {
    color: red;
    cursor: pointer;

    &:hover {
      color: blue;
    }
  }
  ```
