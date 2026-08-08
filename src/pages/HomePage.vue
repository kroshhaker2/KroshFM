<template>
  <div class="radio-page">
    <div id="toast" class="toast" :class="{ show: toastVisible }">
      Ссылка на поток скопирована!
    </div>

    <header>
      <div class="container header-content">
        <a href="#" class="logo">
          <div class="logo-icon">
            <svg
                width="20"
                height="20"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2.5"
                stroke-linecap="round"
                stroke-linejoin="round"
            >
              <circle cx="12" cy="12" r="2" />
              <path d="M16.24 7.76a6 6 0 0 1 0 8.49" />
              <path d="M19.07 4.93a10 10 0 0 1 0 14.14" />
              <path d="M7.76 16.24a6 6 0 0 1 0-8.49" />
              <path d="M4.93 19.07a10 10 0 0 1 0-14.14" />
            </svg>
          </div>

          kroshhaker // radio
        </a>

        <nav>
          <a href="#" class="active">Главная</a>
          <a href="#streams">Потоки</a>
          <a href="#how-it-works">Интеграция</a>

          <span class="live-badge">
            <span class="live-dot"></span>
            {{ streams.length }} Потока Online
          </span>
        </nav>

        <button class="btn btn-primary" @click="openDashboard">
          <svg
              width="16"
              height="16"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
          >
            <path d="M15 3h4a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2h-4" />
            <polyline points="10 17 15 12 10 7" />
            <line x1="15" y1="12" x2="3" y2="12" />
          </svg>

          Панель управления
        </button>
      </div>
    </header>

    <main class="container">
      <!-- Hero -->
      <section class="hero">
        <div>
          <h1 class="hero-title">
            Персональный
            <span>HTTP-стриминг</span>
            для Lavaplayer
          </h1>

          <p class="hero-subtitle">
            Превращайте плейлисты Spotify в стабильный аудиопоток с
            автоматическим поиском треков на YouTube и DSP-обработкой звука в
            реальном времени.
          </p>

          <div class="hero-actions">
            <a href="#streams" class="btn btn-primary">
              <svg
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
              >
                <polygon points="5 3 19 12 5 21 5 3" />
              </svg>

              Слушать онлайн
            </a>

            <button
                class="btn btn-outline"
                @click="copyUrl('https://radio.kroshhaker.dev/stream/main')"
            >
              <svg
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
              >
                <rect x="9" y="9" width="13" height="13" rx="2" />
                <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1" />
              </svg>

              Скопировать URL
            </button>
          </div>
        </div>

        <!-- Player -->
        <div class="hero-player">
          <div class="player-header">
            <span class="player-status">
              ● Live Stream: Main Station
            </span>

            <span class="player-quality">
              320 kbps / Opus
            </span>
          </div>

          <div class="track-info-container">
            <div class="album-art">
              🎵
            </div>

            <div class="track-details">
              <div id="now-playing-title" class="track-title">
                {{ currentTrack.title }}
              </div>

              <div id="now-playing-artist" class="track-artist">
                {{ currentTrack.artist }}
              </div>

              <div class="source-tag">
                <svg
                    width="12"
                    height="12"
                    viewBox="0 0 24 24"
                    fill="currentColor"
                >
                  <path
                      d="M12 0C5.376 0 0 5.376 0 12s5.376 12 12 12 12-5.376 12-12S18.624 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.12-.779-.18-.899-.54-.12-.42.18-.78.54-.9 4.56-1.02 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141 C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C13.56 8.28 7.56 8.1 4.08 9.18c-.6.18-1.2-.18-1.38-.72-.18-.6.18-1.2.72-1.38 4.02-1.2 10.68-1.02 15.3 1.74.54.3.72 1.02.42 1.56-.24.54-.96.72-1.5.42z"
                  />
                </svg>

                Spotify Playlist Source
              </div>
            </div>
          </div>

          <div class="visualizer">
            <div
                v-for="index in 8"
                :key="index"
                class="bar"
            ></div>
          </div>

          <div class="player-controls">
            <button
                class="play-btn"
                :class="{ playing: isPlaying }"
                @click="togglePlay"
            >
              <svg
                  v-if="!isPlaying"
                  width="20"
                  height="20"
                  viewBox="0 0 24 24"
                  fill="currentColor"
              >
                <polygon points="5 3 19 12 5 21 5 3" />
              </svg>

              <svg
                  v-else
                  width="20"
                  height="20"
                  viewBox="0 0 24 24"
                  fill="currentColor"
              >
                <rect x="6" y="4" width="4" height="16" />
                <rect x="14" y="4" width="4" height="16" />
              </svg>
            </button>

            <div class="url-box">
              radio.kroshhaker.dev/stream/main
            </div>
          </div>
        </div>
      </section>

      <!-- Streams -->
      <section id="streams">
        <div class="section-header">
          <div>
            <h2 class="section-title">
              Доступные потоки
            </h2>

            <p class="section-desc">
              Выберите подходящую волну или используйте прямую ссылку для вашего
              бота
            </p>
          </div>
        </div>

        <div class="streams-grid">
          <div
              v-for="stream in streams"
              :key="stream.id"
              class="stream-card"
          >
            <div class="card-top">
              <div>
                <div class="stream-name">
                  #{{ stream.id }} {{ stream.name }}
                </div>

                <span
                    class="stream-status"
                    :class="{ offline: !stream.online }"
                >
                  ●
                  {{ stream.online ? 'Трансляция активна' : 'Трансляция неактивна' }}
                </span>
              </div>

              <span class="codec-badge">
                {{ stream.codec }}
              </span>
            </div>

            <div class="current-track-box">
              <div class="mini-art">
                {{ stream.icon }}
              </div>

              <div>
                <div class="mini-track-title">
                  {{ stream.track.title }}
                </div>

                <div class="mini-track-artist">
                  {{ stream.track.artist }}
                </div>
              </div>
            </div>

            <div class="dsp-tags">
              <span
                  v-for="tag in stream.tags"
                  :key="tag.text"
                  class="tag"
                  :class="`tag-${tag.type}`"
              >
                {{ tag.text }}
              </span>
            </div>

            <div class="card-actions">
              <button
                  class="btn btn-outline"
                  style="flex: 1"
                  @click="copyUrl(stream.url)"
              >
                Скопировать URL
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- How it works -->
      <section id="how-it-works" class="how-it-works">
        <h2
            class="section-title"
            style="text-align: center"
        >
          Как это работает?
        </h2>

        <p
            class="section-desc"
            style="text-align: center; margin-bottom: 20px"
        >
          Запустите свой поток за 3 простых шага
        </p>

        <div class="steps-grid">
          <div class="step-card">
            <div class="step-number">01</div>

            <div class="step-title">
              Укажите Spotify Playlist
            </div>

            <div class="step-desc">
              Вставьте ссылку на любой публичный плейлист Spotify. Система сама
              регулярно синхронизирует список треков.
            </div>
          </div>

          <div class="step-card">
            <div class="step-number">02</div>

            <div class="step-title">
              Настройте DSP и Поиск
            </div>

            <div class="step-desc">
              Автоматический поиск лучшей аудиоверсии на YouTube. Примените
              басс-буст, Nightcore или нормализацию звука.
            </div>
          </div>

          <div class="step-card">
            <div class="step-number">03</div>

            <div class="step-title">
              Вставьте ссылку в Lavaplayer
            </div>

            <div class="step-desc">
              Передайте полученный HTTP URL в ваш Discord бот через метод
              `playerManager.loadItem(...)`.
            </div>
          </div>
        </div>

        <!-- Code -->
        <div class="code-section">
          <div>
            <h3
                style="font-size: 1.3rem; margin-bottom: 12px"
            >
              Быстрое подключение к Lavaplayer
            </h3>

            <p
                style="
                color: var(--text-secondary);
                font-size: 0.95rem;
              "
            >
              Прямая трансляция отдается по стандартному HTTP-протоколу, что
              гарантирует мгновенное воспроизведение без лишней нагрузки на ваш
              сервер бота.
            </p>
          </div>

          <div class="code-box">
            <span class="code-comment">
              // Java / Lavaplayer example
            </span>

            playerManager.<span class="code-keyword">loadItem</span>(
            <span class="code-string">
              "https://radio.kroshhaker.dev/stream/main"
            </span>,
            <span class="code-keyword">new</span>
            AudioLoadResultHandler() { ... } );
          </div>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer>
      <div class="container footer-content">
        <div class="footer-main">
          <div class="footer-brand">
            <span>radio.kroshhaker.dev</span>
          </div>

          <div class="footer-credits">
            <span class="credit-badge">
              ✨ UI Design by <strong>Gemini</strong>
            </span>

            <span class="credit-badge">
              ⚙️ Backend & Architecture by
              <strong>kroshhaker</strong>
            </span>

            <a
                href="https://github.com/kroshhaker2"
                target="_blank"
                rel="noopener noreferrer"
                class="github-link"
            >
              <svg
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="currentColor"
              >
                <path
                    d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"
                />
              </svg>

              @kroshhaker2
            </a>
          </div>
        </div>

        <div class="footer-bottom">
          <div>
            &copy; 2026 Kroshhaker. All rights reserved.
          </div>

          <div style="display: flex; gap: 20px">
            <span>
              Статус:
              <strong style="color: var(--accent-green)">
                100% Operational
              </strong>
            </span>

            <span>
              Задержка:
              <strong>~12ms</strong>
            </span>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

interface StreamTag {
  text: string
  type: 'bass' | 'norm' | 'nightcore'
}

interface Track {
  title: string
  artist: string
}

interface Stream {
  id: number
  name: string
  online: boolean
  codec: string
  icon: string
  url: string
  track: Track
  tags: StreamTag[]
}

const toastVisible = ref(false)
const isPlaying = ref(false)

const streams: Stream[] = [
  {
    id: 1,
    name: 'Main Radio',
    online: true,
    codec: '320kbps MP3',
    icon: '🎧',
    url: 'https://radio.kroshhaker.dev/stream/main',
    track: {
      title: 'Midnight City',
      artist: 'M83',
    },
    tags: [
      {
        text: 'Bass Boost +3dB',
        type: 'bass',
      },
      {
        text: 'Volume Normalizer',
        type: 'norm',
      },
    ],
  },
  {
    id: 2,
    name: 'Lo-Fi Chill Beats',
    online: true,
    codec: '128kbps Opus',
    icon: '☕',
    url: 'https://radio.kroshhaker.dev/stream/lofi',
    track: {
      title: 'Coffee & Raindrops',
      artist: 'Chillhop Music',
    },
    tags: [
      {
        text: 'Volume Normalizer',
        type: 'norm',
      },
    ],
  },
  {
    id: 3,
    name: 'Nightcore Remix Drive',
    online: true,
    codec: '256kbps MP3',
    icon: '⚡',
    url: 'https://radio.kroshhaker.dev/stream/nightcore',
    track: {
      title: 'Rockefeller Street',
      artist: 'Nightcore Mix',
    },
    tags: [
      {
        text: 'Speed 1.25x / Pitch Up',
        type: 'nightcore',
      },
      {
        text: 'Bass Boost',
        type: 'bass',
      },
    ],
  },
]

const currentTrack = computed<Track>(() => ({
  title: 'Midnight City (Cyberpunk Mix)',
  artist: 'M83 / YouTube Match',
}))

let toastTimeout: ReturnType<typeof setTimeout> | undefined

async function copyUrl(url: string): Promise<void> {
  try {
    await navigator.clipboard.writeText(url)

    toastVisible.value = true

    if (toastTimeout) {
      clearTimeout(toastTimeout)
    }

    toastTimeout = setTimeout(() => {
      toastVisible.value = false
    }, 2500)
  } catch (error) {
    console.error('Failed to copy:', error)
  }
}

function togglePlay(): void {
  isPlaying.value = !isPlaying.value
}

function openDashboard(): void {
  alert('Переход в панель управления...')
}
</script>

<style scoped>
.radio-page {
  --bg-dark: #0a0c10;
  --bg-card: #121620;
  --bg-card-hover: #1a202c;

  --accent-green: #1db954;
  --accent-cyan: #00f3ff;
  --accent-purple: #9d4edd;
  --accent-pink: #ff007f;

  --text-primary: #f0f4f8;
  --text-secondary: #8c9ba8;
  --border-color: rgba(255, 255, 255, 0.08);

  --glow-green: rgba(29, 185, 84, 0.25);
  --glow-cyan: rgba(0, 243, 255, 0.2);

  min-height: 100vh;
  background-color: var(--bg-dark);
  color: var(--text-primary);
  line-height: 1.6;
  overflow-x: hidden;

  background-image:
      radial-gradient(
          circle at 15% 20%,
          rgba(157, 78, 221, 0.12) 0%,
          transparent 40%
      ),
      radial-gradient(
          circle at 85% 60%,
          rgba(0, 243, 255, 0.08) 0%,
          transparent 40%
      ),
      radial-gradient(
          circle at 50% 90%,
          rgba(29, 185, 84, 0.1) 0%,
          transparent 50%
      );

  font-family:
      -apple-system,
      BlinkMacSystemFont,
      "Segoe UI",
      Roboto,
      Helvetica,
      Arial,
      sans-serif;
}

/* ================================
   Reset
================================ */

.radio-page *,
.radio-page *::before,
.radio-page *::after {
  box-sizing: border-box;
}

.radio-page a {
  color: inherit;
}

.radio-page button,
.radio-page input,
.radio-page textarea,
.radio-page select {
  font: inherit;
}

/* ================================
   Container
================================ */

.radio-page .container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

/* ================================
   Header
================================ */

.radio-page header {
  position: sticky;
  top: 0;
  z-index: 100;

  border-bottom: 1px solid var(--border-color);

  background: rgba(10, 12, 16, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}

.radio-page .header-content {
  display: flex;
  align-items: center;
  justify-content: space-between;

  height: 72px;
}

.radio-page .logo {
  display: flex;
  align-items: center;
  gap: 12px;

  color: var(--text-primary);
  font-size: 1.25rem;
  font-weight: 700;
  letter-spacing: -0.5px;
  text-decoration: none;
}

.radio-page .logo-icon {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 36px;
  height: 36px;

  background: linear-gradient(
      135deg,
      var(--accent-purple),
      var(--accent-cyan)
  );

  border-radius: 10px;

  box-shadow: 0 0 15px rgba(157, 78, 221, 0.4);
}

/* ================================
   Navigation
================================ */

.radio-page nav {
  display: flex;
  align-items: center;
  gap: 32px;
}

.radio-page nav a {
  color: var(--text-secondary);
  font-size: 0.95rem;
  font-weight: 500;
  text-decoration: none;

  transition: color 0.2s ease;
}

.radio-page nav a:hover,
.radio-page nav a.active {
  color: var(--text-primary);
}

/* ================================
   Live Badge
================================ */

.radio-page .live-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;

  padding: 2px 10px;

  color: var(--accent-green);
  background: rgba(29, 185, 84, 0.15);

  border: 1px solid rgba(29, 185, 84, 0.3);
  border-radius: 20px;

  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

.radio-page .live-dot {
  width: 6px;
  height: 6px;

  background-color: var(--accent-green);
  border-radius: 50%;

  animation: radio-pulse 1.5s infinite;
}

@keyframes radio-pulse {
  0% {
    transform: scale(0.95);
    box-shadow: 0 0 0 0 rgba(29, 185, 84, 0.7);
  }

  70% {
    transform: scale(1);
    box-shadow: 0 0 0 6px rgba(29, 185, 84, 0);
  }

  100% {
    transform: scale(0.95);
    box-shadow: 0 0 0 0 rgba(29, 185, 84, 0);
  }
}

/* ================================
   Buttons
================================ */

.radio-page .btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;

  padding: 10px 20px;

  border: none;
  border-radius: 8px;

  font-size: 0.9rem;
  font-weight: 600;

  cursor: pointer;

  text-decoration: none;

  transition:
      transform 0.2s ease,
      background 0.2s ease,
      border-color 0.2s ease,
      box-shadow 0.2s ease;
}

.radio-page .btn-primary {
  color: #000;

  background: linear-gradient(
      135deg,
      var(--accent-green),
      #14833b
  );

  box-shadow: 0 4px 20px var(--glow-green);
}

.radio-page .btn-primary:hover {
  transform: translateY(-1px);

  box-shadow: 0 6px 24px rgba(29, 185, 84, 0.4);
}

.radio-page .btn-outline {
  color: var(--text-primary);

  background: rgba(255, 255, 255, 0.05);

  border: 1px solid var(--border-color);
}

.radio-page .btn-outline:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.2);
}

/* ================================
   Hero
================================ */

.radio-page .hero {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  align-items: center;
  gap: 48px;

  padding: 80px 0 60px;
}

.radio-page .hero-title {
  margin-bottom: 20px;

  font-size: 3rem;
  font-weight: 800;
  line-height: 1.15;

  background: linear-gradient(
      180deg,
      #ffffff 0%,
      #a0aec0 100%
  );

  -webkit-background-clip: text;
  background-clip: text;

  -webkit-text-fill-color: transparent;
}

.radio-page .hero-title span {
  background: linear-gradient(
      135deg,
      var(--accent-cyan),
      var(--accent-purple)
  );

  -webkit-background-clip: text;
  background-clip: text;

  -webkit-text-fill-color: transparent;
}

.radio-page .hero-subtitle {
  max-width: 540px;

  margin-bottom: 32px;

  color: var(--text-secondary);
  font-size: 1.15rem;
}

.radio-page .hero-actions {
  display: flex;
  gap: 16px;

  margin-bottom: 40px;
}

/* ================================
   Player
================================ */

.radio-page .hero-player {
  position: relative;

  padding: 24px;

  background: var(--bg-card);

  border: 1px solid var(--border-color);
  border-radius: 20px;

  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);

  overflow: hidden;
}

.radio-page .hero-player::before {
  content: "";

  position: absolute;
  top: 0;
  left: 0;
  right: 0;

  height: 4px;

  background: linear-gradient(
      90deg,
      var(--accent-purple),
      var(--accent-cyan),
      var(--accent-green)
  );
}

.radio-page .player-header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  margin-bottom: 20px;
}

.radio-page .player-status {
  color: var(--accent-cyan);

  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.radio-page .player-quality {
  color: var(--text-secondary);
  font-size: 0.8rem;
}

/* ================================
   Track
================================ */

.radio-page .track-info-container {
  display: flex;
  align-items: center;
  gap: 16px;

  margin-bottom: 24px;
}

.radio-page .album-art {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 80px;
  height: 80px;

  flex-shrink: 0;

  background: linear-gradient(
      45deg,
      #1e293b,
      #334155
  );

  border-radius: 12px;

  font-size: 2rem;

  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
}

.radio-page .track-details {
  min-width: 0;
  overflow: hidden;
}

.radio-page .track-title {
  margin-bottom: 4px;

  overflow: hidden;

  font-size: 1.1rem;
  font-weight: 700;

  text-overflow: ellipsis;
  white-space: nowrap;
}

.radio-page .track-artist {
  color: var(--text-secondary);
  font-size: 0.9rem;
}

.radio-page .source-tag {
  display: inline-flex;
  align-items: center;
  gap: 6px;

  margin-top: 8px;
  padding: 2px 8px;

  color: var(--accent-green);
  background: rgba(29, 185, 84, 0.1);

  border-radius: 4px;

  font-size: 0.75rem;
}

/* ================================
   Visualizer
================================ */

.radio-page .visualizer {
  display: flex;
  align-items: flex-end;
  gap: 4px;

  height: 36px;

  margin-bottom: 24px;
  padding: 0 10px;
}

.radio-page .bar {
  flex: 1;

  height: 15%;

  background: linear-gradient(
      180deg,
      var(--accent-cyan),
      var(--accent-purple)
  );

  border-radius: 2px;

  animation: radio-bounce 1.2s ease-in-out infinite alternate;
}

.radio-page .bar:nth-child(1) {
  animation-delay: 0.1s;
}

.radio-page .bar:nth-child(2) {
  animation-delay: 0.4s;
}

.radio-page .bar:nth-child(3) {
  animation-delay: 0.2s;
}

.radio-page .bar:nth-child(4) {
  animation-delay: 0.6s;
}

.radio-page .bar:nth-child(5) {
  animation-delay: 0.3s;
}

.radio-page .bar:nth-child(6) {
  animation-delay: 0.5s;
}

.radio-page .bar:nth-child(7) {
  animation-delay: 0.2s;
}

.radio-page .bar:nth-child(8) {
  animation-delay: 0.7s;
}

@keyframes radio-bounce {
  0% {
    height: 15%;
  }

  100% {
    height: 95%;
  }
}

/* ================================
   Player Controls
================================ */

.radio-page .player-controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;

  padding: 12px 16px;

  background: rgba(0, 0, 0, 0.2);

  border-radius: 12px;
}

.radio-page .play-btn {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 44px;
  height: 44px;

  flex-shrink: 0;

  padding: 0;

  color: #000;
  background: var(--text-primary);

  border: none;
  border-radius: 50%;

  cursor: pointer;

  transition:
      transform 0.2s ease,
      background 0.2s ease;
}

.radio-page .play-btn:hover {
  transform: scale(1.08);
}

.radio-page .play-btn.playing {
  background: var(--accent-green);
}

.radio-page .url-box {
  display: flex;
  align-items: center;

  min-width: 0;
  max-width: 200px;

  padding: 6px 12px;

  overflow: hidden;

  color: var(--accent-cyan);
  background: rgba(255, 255, 255, 0.05);

  border: 1px solid var(--border-color);
  border-radius: 8px;

  font-family: monospace;
  font-size: 0.8rem;

  text-overflow: ellipsis;
  white-space: nowrap;
}

/* ================================
   Section Headers
================================ */

.radio-page .section-header {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;

  margin: 60px 0 32px;
}

.radio-page .section-title {
  font-size: 1.8rem;
  font-weight: 700;
}

.radio-page .section-desc {
  margin-top: 4px;

  color: var(--text-secondary);
  font-size: 0.95rem;
}

/* ================================
   Streams
================================ */

.radio-page .streams-grid {
  display: grid;
  grid-template-columns: repeat(
    auto-fill,
    minmax(350px, 1fr)
  );

  gap: 24px;
}

.radio-page .stream-card {
  position: relative;

  padding: 24px;

  background: var(--bg-card);

  border: 1px solid var(--border-color);
  border-radius: 16px;

  transition:
      transform 0.25s ease,
      border-color 0.25s ease,
      box-shadow 0.25s ease;
}

.radio-page .stream-card:hover {
  transform: translateY(-4px);

  border-color: rgba(255, 255, 255, 0.2);

  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.4);
}

.radio-page .card-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;

  margin-bottom: 16px;
}

.radio-page .stream-name {
  font-size: 1.2rem;
  font-weight: 700;
}

.radio-page .stream-status {
  display: inline-block;

  margin-top: 2px;

  color: var(--accent-green);

  font-size: 0.8rem;
}

.radio-page .stream-status.offline {
  color: var(--text-secondary);
}

.radio-page .codec-badge {
  flex-shrink: 0;

  padding: 4px 8px;

  color: var(--text-secondary);
  background: rgba(255, 255, 255, 0.08);

  border-radius: 6px;

  font-size: 0.75rem;
  font-weight: 600;
}

/* ================================
   Current Track
================================ */

.radio-page .current-track-box {
  display: flex;
  align-items: center;
  gap: 12px;

  margin-bottom: 20px;
  padding: 12px;

  background: rgba(0, 0, 0, 0.25);

  border-radius: 10px;
}

.radio-page .mini-art {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 42px;
  height: 42px;

  flex-shrink: 0;

  background: #2a324b;

  border-radius: 8px;

  font-size: 1.2rem;
}

.radio-page .mini-track-title {
  font-size: 0.85rem;
  font-weight: 600;
}

.radio-page .mini-track-artist {
  color: var(--text-secondary);
  font-size: 0.75rem;
}

/* ================================
   DSP Tags
================================ */

.radio-page .dsp-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;

  margin-bottom: 20px;
}

.radio-page .tag {
  padding: 4px 10px;

  border-radius: 12px;

  font-size: 0.75rem;
  font-weight: 600;
}

.radio-page .tag-bass {
  color: var(--accent-pink);
  background: rgba(255, 0, 127, 0.15);

  border: 1px solid rgba(255, 0, 127, 0.3);
}

.radio-page .tag-nightcore {
  color: var(--accent-purple);
  background: rgba(157, 78, 221, 0.15);

  border: 1px solid rgba(157, 78, 221, 0.3);
}

.radio-page .tag-norm {
  color: var(--accent-cyan);
  background: rgba(0, 243, 255, 0.15);

  border: 1px solid rgba(0, 243, 255, 0.3);
}

.radio-page .card-actions {
  display: flex;
  gap: 12px;
}

/* ================================
   How It Works
================================ */

.radio-page .how-it-works {
  margin-top: 80px;
  padding: 48px;

  background: linear-gradient(
      180deg,
      rgba(18, 22, 32, 0.6) 0%,
      rgba(10, 12, 16, 0.9) 100%
  );

  border: 1px solid var(--border-color);
  border-radius: 24px;
}

.radio-page .steps-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;

  margin-top: 40px;
}

.radio-page .step-card {
  position: relative;
}

.radio-page .step-number {
  position: absolute;
  top: -20px;
  left: 0;

  color: rgba(255, 255, 255, 0.05);

  font-size: 3rem;
  font-weight: 900;
  line-height: 1;
}

.radio-page .step-title {
  position: relative;
  z-index: 1;

  margin-bottom: 12px;

  font-size: 1.1rem;
  font-weight: 700;
}

.radio-page .step-desc {
  position: relative;
  z-index: 1;

  color: var(--text-secondary);

  font-size: 0.9rem;
}

/* ================================
   Code Section
================================ */

.radio-page .code-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 32px;

  margin-top: 60px;
}

.radio-page .code-box {
  padding: 20px;

  overflow-x: auto;

  color: #d1d5db;
  background: #060709;

  border: 1px solid var(--border-color);
  border-radius: 12px;

  font-family:
      "Consolas",
      "Fira Code",
      Monaco,
      monospace;

  font-size: 0.85rem;
  line-height: 1.7;
}

.radio-page .code-keyword {
  color: #f472b6;
}

.radio-page .code-string {
  color: #a7f3d0;
}

.radio-page .code-comment {
  color: #6b7280;
}

/* ================================
   Toast
================================ */

.radio-page .toast {
  position: fixed;
  right: 24px;
  bottom: 24px;
  z-index: 1000;

  padding: 12px 24px;

  color: #000;
  background: var(--accent-green);

  border-radius: 8px;

  font-size: 0.9rem;
  font-weight: 600;

  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);

  transform: translateY(100px);
  opacity: 0;

  pointer-events: none;

  transition:
      transform 0.3s cubic-bezier(0.68, -0.55, 0.27, 1.55),
      opacity 0.3s ease;
}

.radio-page .toast.show {
  transform: translateY(0);
  opacity: 1;
}

/* ================================
   Footer
================================ */

.radio-page footer {
  margin-top: 100px;
  padding: 48px 0;

  color: var(--text-secondary);

  background: rgba(6, 8, 12, 0.9);

  border-top: 1px solid var(--border-color);

  font-size: 0.9rem;
}

.radio-page .footer-content {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.radio-page .footer-main {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;

  flex-wrap: wrap;
}

.radio-page .footer-brand {
  display: flex;
  align-items: center;
  gap: 10px;

  color: var(--text-primary);

  font-weight: 700;
}

.radio-page .footer-credits {
  display: flex;
  align-items: center;
  gap: 16px;

  flex-wrap: wrap;
}

.radio-page .credit-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;

  padding: 6px 14px;

  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.04);

  border: 1px solid var(--border-color);
  border-radius: 20px;

  font-size: 0.85rem;
  text-decoration: none;

  transition:
      transform 0.2s ease,
      background 0.2s ease,
      border-color 0.2s ease;
}

.radio-page .credit-badge:hover {
  transform: translateY(-2px);

  background: rgba(255, 255, 255, 0.08);

  border-color: rgba(255, 255, 255, 0.25);
}

.radio-page .github-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;

  padding: 6px 14px;

  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.08);

  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 20px;

  font-weight: 600;
  text-decoration: none;

  transition:
      background 0.2s ease,
      border-color 0.2s ease,
      color 0.2s ease,
      box-shadow 0.2s ease;
}

.radio-page .github-link:hover {
  color: #fff;
  background: #24292e;

  border-color: var(--accent-cyan);

  box-shadow: 0 0 15px rgba(0, 243, 255, 0.3);
}

.radio-page .footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;

  padding-top: 20px;

  border-top: 1px solid rgba(255, 255, 255, 0.05);

  font-size: 0.8rem;
}

/* ================================
   Responsive
================================ */

@media (max-width: 900px) {
  .radio-page .header-content {
    height: auto;
    min-height: 72px;

    padding-top: 12px;
    padding-bottom: 12px;
  }

  .radio-page nav {
    gap: 16px;
  }

  .radio-page .hero {
    grid-template-columns: 1fr;

    padding-top: 60px;
  }

  .radio-page .steps-grid,
  .radio-page .code-section {
    grid-template-columns: 1fr;
  }

  .radio-page .footer-main,
  .radio-page .footer-bottom {
    align-items: flex-start;
    flex-direction: column;
    gap: 16px;
  }
}

@media (max-width: 700px) {
  .radio-page .container {
    padding: 0 16px;
  }

  .radio-page .header-content {
    flex-wrap: wrap;
    gap: 16px;
  }

  .radio-page nav {
    order: 3;

    width: 100%;

    justify-content: center;
    padding-bottom: 4px;

    overflow-x: auto;
  }

  .radio-page .header-content > .btn {
    padding: 8px 14px;
  }

  .radio-page .hero {
    gap: 32px;

    padding: 48px 0 40px;
  }

  .radio-page .hero-title {
    font-size: 2.25rem;
  }

  .radio-page .hero-subtitle {
    font-size: 1rem;
  }

  .radio-page .hero-actions {
    flex-direction: column;
  }

  .radio-page .hero-actions .btn {
    width: 100%;
  }

  .radio-page .streams-grid {
    grid-template-columns: 1fr;
  }

  .radio-page .how-it-works {
    padding: 32px 20px;
  }

  .radio-page .section-title {
    font-size: 1.5rem;
  }

  .radio-page .player-header {
    align-items: flex-start;
    flex-direction: column;
    gap: 6px;
  }

  .radio-page .player-controls {
    padding: 10px;
  }

  .radio-page .url-box {
    max-width: calc(100% - 56px);
  }

  .radio-page .footer-credits {
    align-items: flex-start;
    flex-direction: column;
  }
}

@media (max-width: 480px) {
  .radio-page .logo {
    font-size: 1rem;
  }

  .radio-page .logo-icon {
    width: 32px;
    height: 32px;
  }

  .radio-page .header-content > .btn {
    font-size: 0.8rem;
  }

  .radio-page nav {
    justify-content: flex-start;
  }

  .radio-page .live-badge {
    white-space: nowrap;
  }

  .radio-page .hero-title {
    font-size: 2rem;
  }

  .radio-page .hero-player {
    padding: 18px;
  }

  .radio-page .track-info-container {
    gap: 12px;
  }

  .radio-page .album-art {
    width: 64px;
    height: 64px;

    font-size: 1.5rem;
  }

  .radio-page .track-title {
    font-size: 1rem;
  }

  .radio-page .streams-grid {
    grid-template-columns: minmax(0, 1fr);
  }

  .radio-page .stream-card {
    padding: 18px;
  }

  .radio-page .card-top {
    flex-direction: column;
    gap: 8px;
  }

  .radio-page .codec-badge {
    align-self: flex-start;
  }

  .radio-page .how-it-works {
    margin-top: 56px;
    padding: 28px 18px;
  }

  .radio-page .code-section {
    margin-top: 40px;
  }

  .radio-page .footer-bottom {
    gap: 12px;
  }

  .radio-page .footer-bottom > div:last-child {
    display: flex;
    flex-direction: column;
    gap: 8px !important;
  }

  .radio-page .toast {
    right: 16px;
    bottom: 16px;
    left: 16px;

    text-align: center;
  }
}
</style>