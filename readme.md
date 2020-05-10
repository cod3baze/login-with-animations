# Animações

- animações
  animções vão de um ponto ate o outro

- [x] Fazer o formulário aparecer, suavemente, quando a página abrir.

```css
/* usando */
form {
  animation-name: fade;
  animation-duration: 800ms;
}

/* criando */
@keyframes fade {
  /* nome da animação */
  from {
    /* vai começãr */
    opacity: 0.9;
    transform: scale(0.9);
  }
  to {
    /* vai terminar */
    opacity: 1;
    transform: scale(1);
  }
}
```

- [x] Fazer os campos aparecerem da esquerda para direita, suavisando a entrada e fazendo-os entrar em momento distintos

```css
form .input-block:nth-child(1) {
  animation: move 500ms;
  animation-delay: 250ms; /* tempo de espera */
}

form .input-block:nth-child(2) {
  animation: move 500ms;
  animation-delay: 250ms; /* tempo de espera */
  animation-fill-mode: backwards; /* fai ficar na posição inicial : [from {}] */
}

@keyframes move {
  from {
    opacity: 0.9;
    transform: translateX(-35%);
  }
  to {
    opacity: 1;
    transform: translateX(0%);
  }
}
```

- [x] Quando clicar em login, fazer o formulário sair da tela, indo para baixo

```css
.form-hide {
  animation: down 500ms forwards;
}

@keyframes down {
  form {
    transform: translateY(0);
  }
  to {
    transform: translateY(100vh);
  }
}
```

```js
const btnLogin = document.querySelector(".btn-login");
const form = document.querySelector("form");

btnLogin.addEventListener("click", (event) => {
  event.preventDefault();
  form.classList.add("form-hide");
});

form.addEventListener("animationstart", (event) => {
  if (event.animationName === "down")
    document.querySelector("body").style.overflow = "hidden";
});

form.addEventListener("animationend", (event) => {
  if (event.animationName === "down") {
    form.style.display = "none";
    document.querySelector("body").style.overflow = "none";
  }
});
```

- [x] Adicionar umefeito diferente de timing para a saída do formuláio

- easy-out: saida vai ser rápida
- easy-in: entrada vai ser rápida

```css
.form-hide {
  animation: down 1.2s forwards;
  animation-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
}

@keyframes down {
  form {
    transform: translateY(0);
  }

  to {
    transform: translateY(100vh);
  }
}
```
