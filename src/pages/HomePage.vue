<script setup lang="ts">
</script>

<template>
  <main class="home">
    <section class="hero">
      <div class="hero__content">
        <span class="hero__label">WELCOME</span>

        <h1>
          Your project starts here.
        </h1>

        <p>
          Современное Vue-приложение на TypeScript, готовое к дальнейшей разработке.
        </p>

        <div class="hero__actions">
          <button class="button button--primary">
            Начать
          </button>

          <button class="button button--secondary">
            Узнать больше
          </button>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.home {
  min-height: 100vh;
  background: #0a0a0a;
  color: #fff;
}

.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 32px;
}

.hero__content {
  width: 100%;
  max-width: 900px;
  text-align: center;
}

.hero__label {
  display: inline-block;
  margin-bottom: 20px;
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.2em;
  color: #888;
}

h1 {
  margin: 0;
  font-size: clamp(48px, 8vw, 96px);
  line-height: 0.95;
  letter-spacing: -0.05em;
}

p {
  max-width: 600px;
  margin: 32px auto 0;
  color: #999;
  font-size: 18px;
  line-height: 1.6;
}

.hero__actions {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 40px;
}

.button {
  padding: 14px 24px;
  border: 1px solid transparent;
  border-radius: 10px;
  font: inherit;
  font-weight: 600;
  cursor: pointer;
  transition: 0.2s ease;
}

.button--primary {
  background: #fff;
  color: #000;
}

.button--primary:hover {
  background: #ddd;
}

.button--secondary {
  border-color: #333;
  background: #111;
  color: #fff;
}

.button--secondary:hover {
  background: #181818;
}

@media (max-width: 600px) {
  .hero {
    padding: 24px;
  }

  .hero__actions {
    flex-direction: column;
  }

  .button {
    width: 100%;
  }
}
</style>
