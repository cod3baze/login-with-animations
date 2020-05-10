# Animações

- Animações
  vão de um ponto ate o outro

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

---

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

---

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

---

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

---

- [x] fazer o form vibrar: campos vazios

```css
form.validate-error {
  animation: nono 200ms linear, fade paused;
  animation-iteration-count: 2;
}

@keyframes nono {
  0%,
  100% {
    transform: translateX(0);
  }

  35% {
    transform: translateX(-15%);
  }

  70% {
    transform: translateX(15%);
  }
}
```

```js
btnLogin.addEventListener("click", (event) => {
  event.preventDefault();

  const fields = [...document.querySelectorAll(".input-block input")];

  fields.forEach((field) => {
    if (field.value === "") {
      console.log(field);
      form.classList.add("validate-error");
    }
  });

  const formError = document.querySelector(".validate-error");
  if (formError) {
    formError.addEventListener("animationend", (event) => {
      if (event.animationName === "nono") {
        formError.classList.remove("validate-error");
      }
    });
  } else {
    form.classList.add("form-hide");
  }
});
btnLogin.addEventListener("click", (event) => {
  event.preventDefault();

  const fields = [...document.querySelectorAll(".input-block input")];

  fields.forEach((field) => {
    if (field.value === "") {
      console.log(field);
      form.classList.add("validate-error");
    }
  });

  const formError = document.querySelector(".validate-error");
  if (formError) {
    formError.addEventListener("animationend", (event) => {
      if (event.animationName === "nono") {
        formError.classList.remove("validate-error");
      }
    });
  } else {
    form.classList.add("form-hide");
  }
});
```

---

- [x] criar qudrados animados (que fiquem girando) que saem debaixa da tela

```css
/* SQUARES */
body {
  overflow: hidden;
}

.squares li {
  width: 40px;
  height: 40px;
  background-color: rgba(255, 255, 255, 0.15);
  display: block;
  position: absolute;
  bottom: -40px;
  animation: up 2s infinite alternate;
  /* animation-direction: reverse; */
  /*[reverte o (from) pata (to)]*/
}

@keyframes up {
  from {
    opacity: 0;
    transform: translateY(0);
  }

  50% {
    opacity: 1;
  }

  to {
    opacity: 0;
    transform: translateY(-800px) rotate(960deg);
  }
}
```

```js
const ulSquares = document.querySelector("ul.squares");

for (let i = 0; i < 11; i++) {
  const li = document.createElement("li");

  const random = (min, max) => Math.random() * (max - min) + min;

  const size = Math.floor(random(10, 120));
  const position = random(1, 90);
  const delay = random(5, 0.1);
  const duration = random(24, 12);

  li.style.width = `${size}px`;
  li.style.height = `${size}px`;
  li.style.bottom = `-${size}px`;

  li.style.left = `${position}%`;

  li.style.animationDelay = `${delay}s`;
  li.style.animationDuration = `${duration}s`;
  li.style.animationTimingFunction = `cubic-bezier(${Math.random()}, ${Math.random()}, ${Math.random()}, ${Math.random()})`;

  ulSquares.appendChild(li);
}
```

---

## References

[CSS Animation Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_ANIMATIONS/Using_CSS_animations)

[Animation Timing Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Animation-timing-function)

[Site para criar animações](https://animista.net/play/basic/scale-up)

[Site para criar cubic Bézier timing](https://matthewlein.com/tools/ceaser)

### Copyright

- By: Elias alexandre
