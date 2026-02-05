Código refatorado por Claude.AI, aplicando boas práticas, organização e melhorias na estrutura:

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Página de login segura">
  <title>Login | Sua Aplicação</title>

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

  <!-- Stylesheet -->
  <link rel="stylesheet" href="template.css">
</head>
<body>
  <main class="login-screen">
    <!-- Background decorativo -->
    <div class="background-shapes" aria-hidden="true"></div>

    <!-- Container principal -->
    <div class="login-container">
      <div class="login-card">
        <!-- Cabeçalho -->
        <header class="login-card__header">
          <div class="logo" aria-label="Logo da empresa">Your Logo</div>
          <h1 class="login-card__title">Login</h1>
        </header>

        <!-- Formulário de login -->
        <form class="login-form" method="POST" action="/login" novalidate>
          <div class="form-group">
            <label for="email" class="form-label">Email</label>
            <input 
              type="email" 
              id="email" 
              name="email"
              class="form-input" 
              placeholder="username@gmail.com"
              required
              autocomplete="email"
            >
          </div>

          <div class="form-group">
            <label for="password" class="form-label">Password</label>
            <input 
              type="password" 
              id="password" 
              name="password"
              class="form-input" 
              placeholder="Enter your password"
              required
              autocomplete="current-password"
            >
          </div>

          <a href="/forgot-password" class="forgot-password">Forgot password?</a>

          <button type="submit" class="btn btn--primary">Sign in</button>
        </form>

        <!-- Footer com opções sociais -->
        <footer class="login-card__footer">
          <span class="divider">or continue with</span>

          <div class="social-login">
            <button type="button" class="social-login__btn social-login__btn--google" aria-label="Login with Google">
              <svg width="18" height="18" viewBox="0 0 18 18" fill="currentColor">
                <path d="M9 3.48c1.69 0 2.83.73 3.48 1.34l2.54-2.48C13.46.89 11.43 0 9 0 5.48 0 2.44 2.02.96 4.96l2.91 2.26C4.6 5.05 6.62 3.48 9 3.48z"/>
              </svg>
            </button>
            <button type="button" class="social-login__btn social-login__btn--github" aria-label="Login with GitHub">
              <svg width="18" height="18" viewBox="0 0 16 16" fill="currentColor">
                <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/>
              </svg>
            </button>
            <button type="button" class="social-login__btn social-login__btn--facebook" aria-label="Login with Facebook">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
              </svg>
            </button>
          </div>

          <p class="signup-prompt">
            Don't have an account?
            <a href="/register" class="signup-prompt__link">Register for free</a>
          </p>
        </footer>
      </div>
    </div>
  </main>
</body>
</html>
```

```css
/* ============================================
   RESET E CONFIGURAÇÕES BASE
   ============================================ */
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 16px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  min-height: 100vh;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  line-height: 1.6;
}

/* ============================================
   VARIÁVEIS CSS
   ============================================ */
:root {
  /* Cores principais */
  --color-primary: #0b5fd7;
  --color-primary-dark: #0a3f8f;
  --color-primary-light: #8cc8ff;
  
  /* Cores de fundo */
  --color-bg-gradient-start: #9ad1ff;
  --color-bg-gradient-end: #7bb8ff;
  
  /* Glass morphism */
  --glass-bg: rgba(255, 255, 255, 0.18);
  --glass-border: rgba(255, 255, 255, 0.3);
  --glass-blur: 14px;
  
  /* Sombras */
  --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 8px 18px rgba(0, 0, 0, 0.2);
  --shadow-lg: 0 25px 60px rgba(0, 0, 0, 0.25);
  
  /* Border radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 20px;
  --radius-xl: 28px;
  
  /* Espaçamentos */
  --spacing-xs: 6px;
  --spacing-sm: 10px;
  --spacing-md: 14px;
  --spacing-lg: 22px;
  --spacing-xl: 32px;
  
  /* Transições */
  --transition-fast: 0.15s ease;
  --transition-normal: 0.3s ease;
}

/* ============================================
   LAYOUT PRINCIPAL
   ============================================ */
.login-screen {
  min-height: 100vh;
  background: linear-gradient(
    135deg,
    var(--color-bg-gradient-start),
    var(--color-bg-gradient-end)
  );
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding: 20px;
}

/* ============================================
   BACKGROUND DECORATIVO
   ============================================ */
.background-shapes {
  position: absolute;
  inset: 0;
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
  z-index: 0;
  pointer-events: none;
}

/* ============================================
   CONTAINER E CARD
   ============================================ */
.login-container {
  width: 100%;
  max-width: 900px;
  background: linear-gradient(
    135deg,
    var(--color-primary-dark),
    var(--color-primary)
  );
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-lg);
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  z-index: 1;
  min-height: 420px;
  padding: 40px 20px;
}

.login-card {
  width: 100%;
  max-width: 380px;
  padding: var(--spacing-xl);
  background: var(--glass-bg);
  backdrop-filter: blur(var(--glass-blur));
  -webkit-backdrop-filter: blur(var(--glass-blur));
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-lg);
  color: #ffffff;
}

/* ============================================
   HEADER
   ============================================ */
.login-card__header {
  margin-bottom: var(--spacing-lg);
}

.logo {
  font-size: 0.875rem;
  font-weight: 500;
  opacity: 0.85;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

.login-card__title {
  font-size: 1.875rem;
  font-weight: 700;
  margin-top: var(--spacing-sm);
  letter-spacing: -0.5px;
}

/* ============================================
   FORMULÁRIO
   ============================================ */
.login-form {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
}

.form-label {
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.3px;
  text-transform: uppercase;
  opacity: 0.9;
}

.form-input {
  width: 100%;
  padding: 11px 14px;
  border-radius: var(--radius-sm);
  border: 1px solid transparent;
  outline: none;
  font-size: 0.9375rem;
  font-family: inherit;
  background: rgba(255, 255, 255, 0.95);
  color: #333;
  transition: all var(--transition-fast);
}

.form-input::placeholder {
  color: #999;
}

.form-input:focus {
  border-color: var(--color-primary-light);
  box-shadow: 0 0 0 3px rgba(140, 200, 255, 0.2);
  background: #ffffff;
}

.form-input:hover:not(:focus) {
  background: #ffffff;
}

/* ============================================
   LINKS E BOTÕES
   ============================================ */
.forgot-password {
  font-size: 0.75rem;
  color: #e0ecff;
  text-decoration: none;
  align-self: flex-end;
  transition: color var(--transition-fast);
  font-weight: 500;
}

.forgot-password:hover {
  color: #ffffff;
  text-decoration: underline;
}

.btn {
  width: 100%;
  padding: 13px 16px;
  border-radius: var(--radius-md);
  border: none;
  font-size: 0.9375rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  transition: all var(--transition-fast);
  text-align: center;
}

.btn--primary {
  margin-top: var(--spacing-sm);
  background: var(--color-primary-dark);
  color: #ffffff;
}

.btn--primary:hover {
  background: #052f6b;
  transform: translateY(-1px);
  box-shadow: var(--shadow-md);
}

.btn--primary:active {
  transform: translateY(0);
}

/* ============================================
   FOOTER E SOCIAL LOGIN
   ============================================ */
.login-card__footer {
  margin-top: var(--spacing-lg);
  text-align: center;
}

.divider {
  display: block;
  font-size: 0.75rem;
  opacity: 0.8;
  margin-bottom: 14px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.social-login {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-bottom: 18px;
}

.social-login__btn {
  width: 44px;
  height: 44px;
  border-radius: var(--radius-sm);
  border: 1px solid rgba(255, 255, 255, 0.3);
  background: rgba(255, 255, 255, 0.1);
  color: #ffffff;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all var(--transition-fast);
}

.social-login__btn:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
}

.social-login__btn svg {
  width: 18px;
  height: 18px;
}

/* ============================================
   SIGNUP
   ============================================ */
.signup-prompt {
  font-size: 0.8125rem;
  opacity: 0.9;
}

.signup-prompt__link {
  color: #ffffff;
  font-weight: 600;
  text-decoration: none;
  transition: opacity var(--transition-fast);
}

.signup-prompt__link:hover {
  opacity: 0.8;
  text-decoration: underline;
}

/* ============================================
   RESPONSIVIDADE
   ============================================ */
@media (max-width: 768px) {
  :root {
    font-size: 14px;
  }
  
  .login-container {
    min-height: auto;
  }
  
  .login-card {
    padding: 24px;
  }
  
  .login-card__title {
    font-size: 1.5rem;
  }
}

@media (max-width: 480px) {
  .login-screen {
    padding: 16px;
  }
  
  .social-login__btn {
    width: 40px;
    height: 40px;
  }
}

/* ============================================
   ESTADOS DE ACESSIBILIDADE
   ============================================ */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

.btn:focus-visible,
.form-input:focus-visible,
.forgot-password:focus-visible,
.signup-prompt__link:focus-visible,
.social-login__btn:focus-visible {
  outline: 2px solid var(--color-primary-light);
  outline-offset: 2px;
}
```

**Melhorias implementadas:**

✅ **HTML Semântico**: Tags apropriadas e estrutura BEM
✅ **Acessibilidade**: Labels, ARIA, autocomplete, navegação por teclado
✅ **Variáveis CSS**: Sistema de design tokens reutilizáveis
✅ **Responsividade**: Media queries e unidades fluidas
✅ **Performance**: Preconnect de fonts, otimização de renders
✅ **Manutenibilidade**: Código organizado em seções comentadas
✅ **UX**: Estados hover, focus, active bem definidos
✅ **SEO**: Meta tags e estrutura semântica
