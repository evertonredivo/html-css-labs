# Aula Completa: Fundamentos HTML e CSS para Interface de Login

## 📚 Índice
1. [Estrutura HTML Semântica](#1-estrutura-html-semântica)
2. [Box Model e Layout](#2-box-model-e-layout)
3. [Flexbox](#3-flexbox)
4. [Posicionamento CSS](#4-posicionamento-css)
5. [Variáveis CSS (Custom Properties)](#5-variáveis-css-custom-properties)
6. [Gradientes](#6-gradientes)
7. [Glass Morphism](#7-glass-morphism)
8. [Pseudo-elementos e Pseudo-classes](#8-pseudo-elementos-e-pseudo-classes)
9. [Transições e Animações](#9-transições-e-animações)
10. [Metodologia BEM](#10-metodologia-bem)
11. [Responsividade](#11-responsividade)
12. [Acessibilidade](#12-acessibilidade)

---

## 1. Estrutura HTML Semântica

### O que é HTML Semântico?
HTML semântico usa tags que descrevem o **significado** do conteúdo, não apenas sua aparência.

### Tags Semânticas vs Não-Semânticas

```html
<!-- ❌ NÃO SEMÂNTICO -->
<div class="header">
  <div class="title">Login</div>
</div>

<!-- ✅ SEMÂNTICO -->
<header class="login-card__header">
  <h1 class="login-card__title">Login</h1>
</header>
```

### Principais Tags Semânticas

| Tag | Significado | Uso |
|-----|-------------|-----|
| `<header>` | Cabeçalho | Topo de uma seção ou página |
| `<main>` | Conteúdo principal | Conteúdo único da página |
| `<section>` | Seção temática | Agrupa conteúdo relacionado |
| `<article>` | Conteúdo independente | Conteúdo que faz sentido sozinho |
| `<footer>` | Rodapé | Parte final de uma seção |
| `<nav>` | Navegação | Links de navegação |

### Exemplo Prático
```html
<main class="login-screen">
  <!-- main = conteúdo principal da página -->
  
  <div class="login-container">
    <div class="login-card">
      
      <header class="login-card__header">
        <!-- header = cabeçalho do card -->
        <h1>Login</h1>
      </header>
      
      <form class="login-form">
        <!-- form = formulário -->
      </form>
      
      <footer class="login-card__footer">
        <!-- footer = rodapé do card -->
      </footer>
      
    </div>
  </div>
</main>
```

---

## 2. Box Model e Layout

### O que é o Box Model?
Todo elemento HTML é uma **caixa** composta por 4 camadas:

```
┌─────────────────────────────────┐
│         MARGIN (margem)         │
│  ┌───────────────────────────┐  │
│  │    BORDER (borda)         │  │
│  │  ┌─────────────────────┐  │  │
│  │  │  PADDING (espaço)   │  │  │
│  │  │  ┌───────────────┐  │  │  │
│  │  │  │   CONTENT     │  │  │  │
│  │  │  │  (conteúdo)   │  │  │  │
│  │  │  └───────────────┘  │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

### Exemplo Prático
```css
.login-card {
  /* CONTENT: 380px de largura */
  width: 380px;
  
  /* PADDING: espaço interno de 32px em todos os lados */
  padding: 32px;
  
  /* BORDER: borda de 1px */
  border: 1px solid rgba(255, 255, 255, 0.3);
  
  /* MARGIN: não definida (0 por padrão) */
}
```

### Box-Sizing
```css
/* Por padrão, width NÃO inclui padding e border */
.box-default {
  width: 300px;      /* apenas conteúdo */
  padding: 20px;     /* +20px cada lado = +40px */
  border: 5px;       /* +5px cada lado = +10px */
  /* Largura total = 350px (300 + 40 + 10) */
}

/* Com box-sizing: border-box, width INCLUI tudo */
.box-border-box {
  box-sizing: border-box;
  width: 300px;      /* total incluindo padding e border */
  padding: 20px;
  border: 5px;
  /* Largura total = 300px (já incluído) */
}
```

**No nosso código usamos:**
```css
* {
  box-sizing: border-box; /* Aplica a TODOS os elementos */
}
```

---

## 3. Flexbox

### O que é Flexbox?
Sistema de layout **unidimensional** (linha OU coluna) que facilita o alinhamento e distribuição de elementos.

### Conceitos Fundamentais

```
FLEX CONTAINER (pai)
┌─────────────────────────────────┐
│  ┌────┐  ┌────┐  ┌────┐        │
│  │ 1  │  │ 2  │  │ 3  │ ← FLEX │
│  └────┘  └────┘  └────┘   ITEMS│
└─────────────────────────────────┘
```

### Propriedades do Container (pai)

```css
.flex-container {
  display: flex;
  
  /* Direção dos itens */
  flex-direction: row;        /* ← → (padrão) */
  flex-direction: column;     /* ↑ ↓ */
  
  /* Alinhamento horizontal (no eixo principal) */
  justify-content: flex-start;   /* ←--- */
  justify-content: center;       /* --←→-- */
  justify-content: flex-end;     /* ---→ */
  justify-content: space-between; /* ←--→ */
  
  /* Alinhamento vertical (no eixo transversal) */
  align-items: flex-start;    /* topo */
  align-items: center;        /* centro */
  align-items: flex-end;      /* base */
  
  /* Quebra de linha */
  flex-wrap: nowrap;  /* não quebra (padrão) */
  flex-wrap: wrap;    /* quebra linha */
}
```

### Exemplo Prático do Nosso Código

```css
/* Centralizar o card na tela */
.login-screen {
  display: flex;
  justify-content: center;  /* centraliza horizontalmente */
  align-items: center;      /* centraliza verticalmente */
  min-height: 100vh;        /* altura da tela toda */
}

/* Organizar inputs em coluna */
.login-form {
  display: flex;
  flex-direction: column;   /* empilha elementos */
  gap: 14px;                /* espaço entre elementos */
}

/* Botões sociais em linha */
.social-login {
  display: flex;
  justify-content: center;  /* centraliza */
  gap: 12px;                /* espaço entre botões */
}
```

### Visualização Prática

```css
/* Login Screen - Centraliza tudo */
┌─────────────────────────────────┐
│                                 │
│         ┌─────────┐             │
│         │  CARD   │   ← Centro  │
│         └─────────┘             │
│                                 │
└─────────────────────────────────┘

/* Login Form - Coluna */
┌─────────────┐
│   Email     │
│ [________]  │
│             │
│  Password   │
│ [________]  │
│             │
│  [Button]   │
└─────────────┘

/* Social Buttons - Linha */
┌─────────────────┐
│  [G] [GH] [F]  │ ← Lado a lado
└─────────────────┘
```

---

## 4. Posicionamento CSS

### Tipos de Posicionamento

```css
/* 1. STATIC (padrão) - fluxo normal do documento */
.elemento {
  position: static;
}

/* 2. RELATIVE - relativo à sua posição original */
.elemento {
  position: relative;
  top: 10px;     /* move 10px para baixo */
  left: 20px;    /* move 20px para direita */
}

/* 3. ABSOLUTE - relativo ao pai com position */
.elemento {
  position: absolute;
  top: 0;        /* cola no topo do pai */
  right: 0;      /* cola na direita do pai */
}

/* 4. FIXED - relativo à janela do navegador */
.elemento {
  position: fixed;
  top: 0;        /* cola no topo da tela */
  left: 0;       /* cola na esquerda da tela */
}

/* 5. STICKY - híbrido entre relative e fixed */
.elemento {
  position: sticky;
  top: 0;        /* gruda quando rolar */
}
```

### Exemplo no Nosso Código

```css
/* Container relativo */
.login-screen {
  position: relative;  /* cria contexto para filhos absolute */
}

/* Background absoluto - preenche todo o pai */
.background-shapes {
  position: absolute;
  inset: 0;  /* equivale a: top:0, right:0, bottom:0, left:0 */
}
```

### Visualização

```
RELATIVE CONTAINER
┌─────────────────────────────────┐
│  position: relative             │
│                                 │
│  ┌─────────────────────────┐   │
│  │ position: absolute      │   │
│  │ inset: 0                │   │
│  │ (preenche tudo)         │   │
│  └─────────────────────────┘   │
└─────────────────────────────────┘
```

### Z-Index (Profundidade)

```css
/* Quanto maior o z-index, mais na frente */
.background-shapes {
  z-index: 0;  /* fundo */
}

.login-container {
  z-index: 1;  /* frente */
}
```

```
Vista lateral:
           ┌─────┐ z-index: 1 (frente)
          ┌─────┐  z-index: 0 (fundo)
         └─────┘
    (tela do usuário)
```

---

## 5. Variáveis CSS (Custom Properties)

### O que são Variáveis CSS?
Permitem **reutilizar valores** e criar um **sistema de design** consistente.

### Sintaxe Básica

```css
/* 1. DEFINIR variáveis no :root */
:root {
  --cor-principal: #0b5fd7;
  --espacamento: 16px;
}

/* 2. USAR variáveis com var() */
.botao {
  background: var(--cor-principal);
  padding: var(--espacamento);
}
```

### Exemplo Completo do Nosso Código

```css
:root {
  /* Cores */
  --color-primary: #0b5fd7;
  --color-primary-dark: #0a3f8f;
  
  /* Espaçamentos */
  --spacing-sm: 10px;
  --spacing-md: 14px;
  --spacing-lg: 22px;
  
  /* Border radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  
  /* Sombras */
  --shadow-lg: 0 25px 60px rgba(0, 0, 0, 0.25);
}

/* Usando as variáveis */
.btn--primary {
  background: var(--color-primary-dark);
  padding: var(--spacing-sm);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-lg);
}
```

### Vantagens

✅ **Manutenção fácil**: Muda em um lugar, aplica em todos
✅ **Consistência**: Mesmos valores em todo o projeto
✅ **Legibilidade**: Nomes descritivos
✅ **Temas**: Fácil criar modo escuro/claro

### Exemplo de Tema

```css
/* Tema claro */
:root {
  --bg-color: white;
  --text-color: black;
}

/* Tema escuro */
[data-theme="dark"] {
  --bg-color: black;
  --text-color: white;
}

/* Uso automático */
body {
  background: var(--bg-color);
  color: var(--text-color);
}
```

---

## 6. Gradientes

### O que são Gradientes?
Transições suaves entre duas ou mais cores.

### Tipos de Gradientes

#### 1. Linear Gradient (Linear)

```css
/* Sintaxe básica */
background: linear-gradient(direção, cor1, cor2);

/* Exemplos */
.exemplo1 {
  /* De cima para baixo (padrão) */
  background: linear-gradient(red, blue);
}

.exemplo2 {
  /* Da esquerda para direita */
  background: linear-gradient(to right, red, blue);
}

.exemplo3 {
  /* Diagonal */
  background: linear-gradient(135deg, red, blue);
}

.exemplo4 {
  /* Múltiplas cores */
  background: linear-gradient(red, yellow, green, blue);
}

.exemplo5 {
  /* Com posições específicas */
  background: linear-gradient(
    red 0%,      /* começa vermelho */
    yellow 50%,  /* meio amarelo */
    blue 100%    /* termina azul */
  );
}
```

#### Visualização Linear Gradient

```
to bottom (padrão):     to right:          135deg (diagonal):
┌──────┐               ┌────────────┐      ┌──────────┐
│ RED  │               │R  Y  G  B  │      │R        B│
│      │               │E  E  R  L  │      │ E      L │
│YELLOW│               │D  L  E  U  │      │  D    U  │
│      │               │   L  E  E  │      │   ╲  ╱   │
│ BLUE │               │   O  N     │      │    YG    │
└──────┘               └────────────┘      └──────────┘
```

#### 2. Radial Gradient (Radial)

```css
/* Sintaxe básica */
background: radial-gradient(forma at posição, cor1, cor2);

/* Exemplos */
.exemplo1 {
  /* Centro (padrão) */
  background: radial-gradient(red, blue);
}

.exemplo2 {
  /* Círculo no canto superior esquerdo */
  background: radial-gradient(
    circle at 20% 30%,
    red,
    blue
  );
}

.exemplo3 {
  /* Com transparência */
  background: radial-gradient(
    circle at center,
    rgba(255, 0, 0, 0.5),
    transparent
  );
}
```

#### Visualização Radial Gradient

```
circle at center:       circle at 20% 30%:
┌────────────┐         ┌────────────┐
│     ●●●    │         │ ●●●        │
│   ●●●●●●   │         │●●●●●       │
│  ●●●●●●●●  │         │ ●●●        │
│   ●●●●●●   │         │            │
│     ●●●    │         │            │
└────────────┘         └────────────┘
   (centro)             (topo esq.)
```

### Nosso Código: Gradientes Usados

```css
/* 1. Fundo da tela - Linear Gradient */
.login-screen {
  background: linear-gradient(
    135deg,                    /* diagonal */
    #9ad1ff,                   /* azul claro */
    #7bb8ff                    /* azul médio */
  );
}

/* 2. Card principal - Linear Gradient */
.login-container {
  background: linear-gradient(
    135deg,
    var(--color-primary-dark),  /* azul escuro */
    var(--color-primary)        /* azul médio */
  );
}

/* 3. Background shapes - Radial Gradient */
.background-shapes {
  background:
    radial-gradient(
      circle at 20% 30%,
      rgba(255, 255, 255, 0.3),
      transparent 50%
    ),
    radial-gradient(
      circle at 80% 70%,
      rgba(200, 220, 255, 0.25),
      transparent 60%
    );
}
```

### Múltiplos Backgrounds

```css
/* Pode empilhar múltiplos gradientes */
.elemento {
  background:
    radial-gradient(...),  /* frente */
    radial-gradient(...),  /* meio */
    linear-gradient(...);  /* fundo */
}
```

---

## 7. Glass Morphism

### O que é Glass Morphism?
Efeito visual que simula **vidro fosco** usando:
- Fundo semi-transparente
- Blur (desfoque)
- Borda sutil

### Componentes do Efeito

```css
.glass {
  /* 1. Fundo semi-transparente */
  background: rgba(255, 255, 255, 0.18);
  
  /* 2. Blur do fundo */
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);  /* Safari */
  
  /* 3. Borda sutil */
  border: 1px solid rgba(255, 255, 255, 0.3);
  
  /* 4. Bordas arredondadas */
  border-radius: 20px;
}
```

### Visualização do Efeito

```
SEM Glass Morphism:
┌─────────────┐
│   OPACO     │
│   SÓLIDO    │
└─────────────┘

COM Glass Morphism:
┌─────────────┐
│░░ DESFOCADO│░  ← Blur
│░░ FUNDO    │░  ← Semi-transparente
│░░ VISÍVEL  │░  ← Borda sutil
└─────────────┘
```

### Diferença: background vs backdrop-filter

```css
/* BACKGROUND (cor do próprio elemento) */
.elemento {
  background: rgba(255, 255, 255, 0.5);
  /* O ELEMENTO fica semi-transparente */
}

/* BACKDROP-FILTER (desfoca o que está ATRÁS) */
.elemento {
  backdrop-filter: blur(10px);
  /* O FUNDO fica desfocado */
}
```

### Exemplo Prático

```css
/* Card com Glass Morphism */
.login-card {
  /* Semi-transparente */
  background: rgba(255, 255, 255, 0.18);
  
  /* Desfoca o que está atrás */
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  
  /* Borda sutil */
  border: 1px solid rgba(255, 255, 255, 0.3);
  
  /* Arredondado */
  border-radius: 20px;
}
```

### RGBA - Cores com Transparência

```css
/* RGB (Red, Green, Blue) */
color: rgb(255, 0, 0);  /* vermelho */

/* RGBA (Red, Green, Blue, Alpha) */
color: rgba(255, 0, 0, 0.5);
/*       R    G   B   A
         |    |   |   |
       vermelho  |   |
            verde |   |
               azul   |
          transparência (0-1)
*/

/* Exemplos de Alpha */
rgba(255, 255, 255, 0)    /* totalmente transparente */
rgba(255, 255, 255, 0.5)  /* 50% transparente */
rgba(255, 255, 255, 1)    /* totalmente opaco */
```

---

## 8. Pseudo-elementos e Pseudo-classes

### Pseudo-classes (Estados)
Aplicam estilos baseados no **estado** do elemento.

```css
/* :hover - quando o mouse passa por cima */
.botao:hover {
  background: blue;
}

/* :focus - quando o elemento está focado */
.input:focus {
  border: 2px solid blue;
}

/* :active - quando está sendo clicado */
.botao:active {
  transform: scale(0.95);
}

/* :first-child - primeiro filho */
.lista li:first-child {
  font-weight: bold;
}

/* :last-child - último filho */
.lista li:last-child {
  border-bottom: none;
}

/* :nth-child(n) - enésimo filho */
.lista li:nth-child(2) {  /* segundo item */
  color: red;
}

.lista li:nth-child(odd) {  /* ímpares: 1, 3, 5... */
  background: #f0f0f0;
}

.lista li:nth-child(even) {  /* pares: 2, 4, 6... */
  background: white;
}
```

### Exemplo do Nosso Código

```css
/* Hover nos inputs */
.form-input:hover:not(:focus) {
  background: #ffffff;
}

/* Focus nos inputs */
.form-input:focus {
  border-color: var(--color-primary-light);
  box-shadow: 0 0 0 3px rgba(140, 200, 255, 0.2);
}

/* Hover no botão */
.btn--primary:hover {
  background: #052f6b;
  transform: translateY(-1px);
}

/* Active no botão */
.btn--primary:active {
  transform: translateY(0);
}
```

### Pseudo-elementos (Partes do Elemento)
Criam elementos **virtuais** que não existem no HTML.

```css
/* ::before - cria elemento ANTES do conteúdo */
.elemento::before {
  content: "→ ";  /* obrigatório */
  color: blue;
}

/* ::after - cria elemento DEPOIS do conteúdo */
.elemento::after {
  content: " ←";  /* obrigatório */
  color: red;
}

/* ::first-line - primeira linha de texto */
p::first-line {
  font-weight: bold;
}

/* ::first-letter - primeira letra */
p::first-letter {
  font-size: 2em;
}

/* ::placeholder - placeholder de input */
input::placeholder {
  color: #999;
}
```

### Visualização

```html
<div class="box">Conteúdo</div>
```

```css
.box::before {
  content: "ANTES";
}

.box::after {
  content: "DEPOIS";
}
```

Resultado visual:
```
[ANTES] Conteúdo [DEPOIS]
```

### Pseudo-elemento ::before para Overlay

```css
/* Criar camada sobre elemento */
.elemento {
  position: relative;
}

.elemento::before {
  content: '';
  position: absolute;
  inset: 0;  /* cobre tudo */
  background: rgba(0, 0, 0, 0.5);
  z-index: -1;
}
```

---

## 9. Transições e Animações

### Transições (Mudanças Suaves)

```css
/* Sintaxe básica */
transition: propriedade duração timing-function delay;

/* Exemplos */
.botao {
  background: blue;
  transition: background 0.3s ease;
}

.botao:hover {
  background: red;
  /* Muda suavemente em 0.3s */
}
```

### Propriedades da Transition

```css
.elemento {
  /* Propriedade específica */
  transition: background 0.3s;
  
  /* Múltiplas propriedades */
  transition: 
    background 0.3s,
    transform 0.2s,
    box-shadow 0.3s;
  
  /* Todas as propriedades */
  transition: all 0.3s ease;
}
```

### Timing Functions (Curvas de Animação)

```css
/* LINEAR - velocidade constante */
transition: all 0.3s linear;

/* EASE (padrão) - começa devagar, acelera, termina devagar */
transition: all 0.3s ease;

/* EASE-IN - começa devagar */
transition: all 0.3s ease-in;

/* EASE-OUT - termina devagar */
transition: all 0.3s ease-out;

/* EASE-IN-OUT - começa e termina devagar */
transition: all 0.3s ease-in-out;

/* CUBIC-BEZIER - curva personalizada */
transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
```

### Visualização das Curvas

```
linear:      ──────────  (constante)

ease:        ╱────╲      (suave nos extremos)

ease-in:     ╱──────     (acelera)

ease-out:    ──────╲     (desacelera)
```

### Nosso Código: Transições

```css
/* Variáveis de transição */
:root {
  --transition-fast: 0.15s ease;
  --transition-normal: 0.3s ease;
}

/* Input com transição */
.form-input {
  transition: all var(--transition-fast);
}

.form-input:focus {
  border-color: blue;
  box-shadow: 0 0 0 3px rgba(0, 100, 255, 0.2);
  /* Muda suavemente */
}

/* Botão com transição */
.btn {
  transition: all var(--transition-fast);
}

.btn--primary:hover {
  transform: translateY(-1px);
  box-shadow: 0 8px 18px rgba(0, 0, 0, 0.2);
  /* Eleva suavemente */
}
```

### Transform (Transformações)

```css
/* TRANSLATE - move o elemento */
transform: translateX(10px);    /* move para direita */
transform: translateY(-10px);   /* move para cima */
transform: translate(10px, -10px); /* move X e Y */

/* SCALE - aumenta/diminui */
transform: scale(1.5);     /* 150% do tamanho */
transform: scale(0.8);     /* 80% do tamanho */

/* ROTATE - rotaciona */
transform: rotate(45deg);  /* 45 graus */
transform: rotate(-90deg); /* -90 graus */

/* SKEW - inclina */
transform: skew(20deg);    /* inclina */

/* MÚLTIPLAS transformações */
transform: translateY(-5px) scale(1.1) rotate(5deg);
```

### Exemplo Prático: Hover com Transform

```css
.card {
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);  /* levanta 10px */
}
```

---

## 10. Metodologia BEM

### O que é BEM?
**B**lock **E**lement **M**odifier - metodologia para nomear classes CSS.

### Estrutura BEM

```
block__element--modifier
  │      │        │
  │      │        └─ Variação do elemento
  │      └────────── Parte do bloco
  └───────────────── Componente principal
```

### Regras

1. **Block** (Bloco): Componente independente
2. **Element** (Elemento): Parte do bloco (usa `__`)
3. **Modifier** (Modificador): Variação (usa `--`)

### Exemplo Sem BEM (Confuso)

```html
<div class="card">
  <div class="header">
    <h1 class="title">Título</h1>
  </div>
  <button class="button primary">Botão</button>
</div>
```

```css
.card .header .title { }  /* Específico demais */
.button.primary { }        /* Ambíguo */
```

### Exemplo Com BEM (Claro)

```html
<div class="card">
  <div class="card__header">
    <h1 class="card__title">Título</h1>
  </div>
  <button class="card__button card__button--primary">Botão</button>
</div>
```

```css
.card { }                    /* Bloco */
.card__header { }            /* Elemento do card */
.card__title { }             /* Elemento do card */
.card__button { }            /* Elemento do card */
.card__button--primary { }   /* Modificador do button */
```

### Nosso Código com BEM

```html
<!-- BLOCK: login-card -->
<div class="login-card">
  
  <!-- ELEMENT: login-card__header -->
  <header class="login-card__header">
    <h1 class="login-card__title">Login</h1>
  </header>
  
  <!-- ELEMENT: login-card__footer -->
  <footer class="login-card__footer">
    <!-- ... -->
  </footer>
  
</div>

<!-- BLOCK: btn -->
<button class="btn btn--primary">Sign in</button>
<!--           │       │
           BLOCK  MODIFIER
-->
```

```css
/* BLOCK */
.login-card { }

/* ELEMENTS */
.login-card__header { }
.login-card__title { }
.login-card__footer { }

/* BLOCK com MODIFIER */
.btn { }
.btn--primary { }
.btn--secondary { }
```

### Vantagens do BEM

✅ **Clareza**: Nome descreve função e hierarquia
✅ **Reutilização**: Blocos são independentes
✅ **Escalabilidade**: Fácil manter projetos grandes
✅ **Sem conflitos**: Nomes únicos e específicos

### Exemplo Completo

```html
<article class="product-card">
  <header class="product-card__header">
    <img class="product-card__image" src="...">
    <span class="product-card__badge product-card__badge--sale">Sale</span>
  </header>
  
  <div class="product-card__body">
    <h2 class="product-card__title">Nome do Produto</h2>
    <p class="product-card__price">R$ 99,90</p>
  </div>
  
  <footer class="product-card__footer">
    <button class="product-card__button product-card__button--buy">
      Comprar
    </button>
  </footer>
</article>
```

---

## 11. Responsividade

### O que é Responsividade?
Design que **se adapta** a diferentes tamanhos de tela.

### Mobile First vs Desktop First

```css
/* MOBILE FIRST - começa mobile, expande para desktop */
.elemento {
  width: 100%;  /* mobile (padrão) */
}

@media (min-width: 768px) {
  .elemento {
    width: 50%;  /* tablet e acima */
  }
}

@media (min-width: 1200px) {
  .elemento {
    width: 33%;  /* desktop */
  }
}

/* DESKTOP FIRST - começa desktop, adapta para mobile */
.elemento {
  width: 33%;  /* desktop (padrão) */
}

@media (max-width: 1200px) {
  .elemento {
    width: 50%;  /* tablet e abaixo */
  }
}

@media (max-width: 768px) {
  .elemento {
    width: 100%;  /* mobile */
  }
}
```

### Breakpoints Comuns

```css
/* Extra Small - Smartphones */
@media (max-width: 575px) { }

/* Small - Tablets portrait */
@media (min-width: 576px) and (max-width: 767px) { }

/* Medium - Tablets landscape */
@media (min-width: 768px) and (max-width: 991px) { }

/* Large - Desktops */
@media (min-width: 992px) and (max-width: 1199px) { }

/* Extra Large - Large desktops */
@media (min-width: 1200px) { }
```

### Unidades Responsivas

```css
/* FIXAS (não mudam) */
.elemento {
  width: 300px;   /* pixels fixos */
  width: 2cm;     /* centímetros */
}

/* RELATIVAS (se adaptam) */
.elemento {
  width: 50%;        /* 50% do pai */
  width: 50vw;       /* 50% da viewport (largura da tela) */
  width: 50vh;       /* 50% da altura da tela */
  
  font-size: 1em;    /* relativo ao font-size do pai */
  font-size: 1rem;   /* relativo ao font-size do html */
  font-size: 2vw;    /* 2% da largura da tela */
}
```

### Nosso Código: Responsividade

```css
/* Base - Mobile */
.login-container {
  width: 90%;        /* 90% da tela */
  max-width: 900px;  /* máximo 900px */
  padding: 40px 20px;
}

.login-card {
  width: 100%;
  max-width: 380px;
}

/* Tablet */
@media (max-width: 768px) {
  :root {
    font-size: 14px;  /* reduz tamanho base */
  }
  
  .login-container {
    min-height: auto;  /* remove altura mínima */
  }
  
  .login-card {
    padding: 24px;  /* reduz padding */
  }
}

/* Mobile */
@media (max-width: 480px) {
  .login-screen {
    padding: 16px;  /* menos espaço */
  }
  
  .social-login__btn {
    width: 40px;   /* botões menores */
    height: 40px;
  }
}
```

### Viewport Meta Tag

```html
<!-- ESSENCIAL para responsividade funcionar -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<!--                             │                    │
                          largura = tela     zoom inicial = 100%
-->
```

### Técnicas Responsivas

```css
/* 1. MAX-WIDTH - limita crescimento */
.container {
  width: 100%;
  max-width: 1200px;  /* não cresce mais que isso */
}

/* 2. MIN e MAX combinados */
.elemento {
  width: 80%;
  min-width: 300px;   /* mínimo 300px */
  max-width: 800px;   /* máximo 800px */
}

/* 3. CLAMP - limita entre min e max */
.texto {
  font-size: clamp(14px, 2vw, 24px);
  /*             │     │    │
               min  ideal  max
  */
}

/* 4. ASPECT-RATIO - mantém proporção */
.video {
  width: 100%;
  aspect-ratio: 16 / 9;  /* sempre 16:9 */
}
```

---

## 12. Acessibilidade

### O que é Acessibilidade Web?
Tornar sites **usáveis por todos**, incluindo pessoas com deficiências.

### Princípios Fundamentais (WCAG)

1. **Perceptível**: Usuários podem perceber o conteúdo
2. **Operável**: Usuários podem usar a interface
3. **Compreensível**: Informação é clara
4. **Robusto**: Funciona em diferentes tecnologias

### HTML Semântico para Acessibilidade

```html
<!-- ❌ RUIM - sem significado -->
<div onclick="enviar()">Enviar</div>

<!-- ✅ BOM - semântico e acessível -->
<button type="submit">Enviar</button>

<!-- ❌ RUIM - imagem sem descrição -->
<img src="logo.png">

<!-- ✅ BOM - com texto alternativo -->
<img src="logo.png" alt="Logo da Empresa XYZ">

<!-- ❌ RUIM - link genérico -->
<a href="#">Clique aqui</a>

<!-- ✅ BOM - link descritivo -->
<a href="/produtos">Ver todos os produtos</a>
```

### Labels em Formulários

```html
<!-- ❌ RUIM - sem label -->
<input type="email" placeholder="Email">

<!-- ✅ BOM - com label associado -->
<label for="email">Email</label>
<input type="email" id="email" placeholder="seu@email.com">

<!-- ✅ ALTERNATIVA - label envolvendo -->
<label>
  Email
  <input type="email" placeholder="seu@email.com">
</label>
```

### ARIA (Accessible Rich Internet Applications)

```html
<!-- aria-label - rótulo invisível -->
<button aria-label="Fechar modal">
  <span>×</span>
</button>

<!-- aria-labelledby - referencia outro elemento -->
<h2 id="titulo-modal">Confirmar ação</h2>
<div aria-labelledby="titulo-modal">
  Você tem certeza?
</div>

<!-- aria-describedby - descrição adicional -->
<input 
  type="password" 
  aria-describedby="senha-regras"
>
<span id="senha-regras">Mínimo 8 caracteres</span>

<!-- aria-hidden - esconde de leitores de tela -->
<span aria-hidden="true">★</span>
<span class="visually-hidden">5 estrelas</span>
```

### Roles (Papéis)

```html
<!-- role="" define o papel do elemento -->
<div role="navigation">
  <a href="/">Home</a>
  <a href="/sobre">Sobre</a>
</div>

<!-- Melhor usar tags semânticas -->
<nav>
  <a href="/">Home</a>
  <a href="/sobre">Sobre</a>
</nav>
```

### Nosso Código: Acessibilidade

```html
<!-- Labels associados aos inputs -->
<label for="email" class="form-label">Email</label>
<input 
  type="email" 
  id="email"
  name="email"
  required
  autocomplete="email"
>

<!-- Botões com aria-label -->
<button 
  type="button" 
  class="social-login__btn" 
  aria-label="Login with Google"
>
  <svg>...</svg>
</button>

<!-- Background decorativo escondido -->
<div class="background-shapes" aria-hidden="true"></div>
```

### Navegação por Teclado

```css
/* Indicador de foco visível */
.btn:focus-visible,
.form-input:focus-visible {
  outline: 2px solid var(--color-primary-light);
  outline-offset: 2px;
}

/* Remove outline apenas para mouse */
.btn:focus:not(:focus-visible) {
  outline: none;
}
```

### Contraste de Cores

```css
/* ❌ RUIM - baixo contraste */
.texto {
  color: #999;           /* cinza claro */
  background: #eee;      /* cinza mais claro */
  /* Difícil de ler */
}

/* ✅ BOM - alto contraste */
.texto {
  color: #333;           /* cinza escuro */
  background: #fff;      /* branco */
  /* Fácil de ler */
}
```

**Razão de contraste mínima:**
- Texto normal: 4.5:1
- Texto grande: 3:1

### Classe Visually Hidden

```css
/* Esconde visualmente mas mantém para leitores de tela */
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

```html
<!-- Uso -->
<button aria-label="Adicionar ao carrinho">
  <span class="visually-hidden">Adicionar ao carrinho</span>
  <span aria-hidden="true">🛒</span>
</button>
```

### Prefers Reduced Motion

```css
/* Respeita preferência de animação do sistema */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Autocomplete

```html
<!-- Ajuda preenchimento automático -->
<input 
  type="email" 
  autocomplete="email"
>

<input 
  type="password" 
  autocomplete="current-password"
>

<input 
  type="text" 
  autocomplete="given-name"  <!-- primeiro nome -->
>

<input 
  type="text" 
  autocomplete="family-name"  <!-- sobrenome -->
>
```

### Checklist de Acessibilidade

✅ Usar HTML semântico (`<header>`, `<nav>`, `<main>`, etc.)
✅ Labels em todos os inputs
✅ Textos alternativos em imagens
✅ Contraste adequado de cores (4.5:1)
✅ Navegação por teclado funcional
✅ Estados de foco visíveis
✅ ARIA onde necessário
✅ Respeitar `prefers-reduced-motion`
✅ Autocomplete em formulários
✅ Evitar `<div>` e `<span>` para elementos interativos

---

## 📝 Exercícios Práticos

### Exercício 1: Flexbox
Crie um layout com 3 cards lado a lado que se empilham em telas pequenas.

### Exercício 2: Glass Morphism
Adicione efeito glass em um card sobre uma imagem de fundo.

### Exercício 3: BEM
Converta estas classes para BEM:
```css
.card { }
.card .header { }
.card .header .title { }
.card .button.primary { }
```

### Exercício 4: Responsividade
Faça um menu horizontal virar hamburguer em mobile.

### Exercício 5: Acessibilidade
Adicione acessibilidade completa a este formulário:
```html
<input type="text" placeholder="Nome">
<input type="email" placeholder="Email">
<button>Enviar</button>
```

---

## 🎯 Resumo dos Conceitos-Chave

| Conceito | Uso | Exemplo |
|----------|-----|---------|
| **Flexbox** | Layout unidimensional | `display: flex` |
| **Grid** | Layout bidimensional | `display: grid` |
| **Position** | Posicionamento preciso | `position: absolute` |
| **Variáveis CSS** | Reutilizar valores | `var(--cor)` |
| **Gradientes** | Transições de cor | `linear-gradient()` |
| **Glass Morphism** | Efeito vidro | `backdrop-filter: blur()` |
| **BEM** | Nomenclatura | `block__element--modifier` |
| **Media Queries** | Responsividade | `@media (max-width: 768px)` |
| **ARIA** | Acessibilidade | `aria-label="..."` |
| **Transições** | Animações suaves | `transition: all 0.3s` |

---

## 🔗 Recursos Adicionais

- **MDN Web Docs**: https://developer.mozilla.org
- **CSS Tricks**: https://css-tricks.com
- **Can I Use**: https://caniuse.com
- **Flexbox Froggy**: https://flexboxfroggy.com (jogo para aprender Flexbox)
- **Grid Garden**: https://cssgridgarden.com (jogo para aprender Grid)
- **BEM**: https://getbem.com
- **WCAG**: https://www.w3.org/WAI/WCAG21/quickref

---

## ✅ Próximos Passos

1. Pratique cada conceito individualmente
2. Combine conceitos em projetos pequenos
3. Estude código de sites profissionais (DevTools)
4. Participe de desafios (Frontend Mentor, CSS Battle)
5. Construa projetos pessoais aplicando tudo

**Boa sorte nos estudos! 🚀**
