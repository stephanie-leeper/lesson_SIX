<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'

type LinkItem = {
  label: string
  href: string
  icon: string
}

const links: LinkItem[] = [
  {
    label: 'LinkedIn',
    href: 'https://www.linkedin.com/in/stephanieleeper',
    icon: 'in',
  },
  {
    label: 'Instagram',
    href: 'https://www.instagram.com/stephanieleeper',
    icon: 'ig',
  },
  {
    label: 'Email',
    href: 'mailto:stephanie.leeper@slalom.com',
    icon: '@',
  },
]

const isDark = ref(false)

function applyTheme(dark: boolean) {
  document.documentElement.classList.toggle('dark', dark)
}

function toggleTheme() {
  isDark.value = !isDark.value
}

onMounted(() => {
  const stored = localStorage.getItem('theme')
  if (stored) {
    isDark.value = stored === 'dark'
  }
  applyTheme(isDark.value)
})

watch(isDark, (dark) => {
  applyTheme(dark)
  localStorage.setItem('theme', dark ? 'dark' : 'light')
})
</script>

<template>
  <main class="card">
    <button
      class="theme-toggle"
      type="button"
      :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
      @click="toggleTheme"
    >
      {{ isDark ? '☀' : '☾' }}
    </button>

    <div class="avatar" aria-hidden="true">SL</div>

    <h1 class="name">Stephanie Leeper</h1>
    <p class="tagline">Designer, builder, lifelong learner.</p>

    <ul class="links">
      <li v-for="link in links" :key="link.label">
        <a class="link-btn" :href="link.href" target="_blank" rel="noopener noreferrer">
          <span class="icon">{{ link.icon }}</span>
          <span class="label">{{ link.label }}</span>
        </a>
      </li>
    </ul>
  </main>
</template>

<style scoped>
.card {
  position: relative;
  width: 100%;
  max-width: 480px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 2.5rem 1.75rem 2rem;
  box-shadow: var(--shadow);
  text-align: center;
  transition: background 0.3s ease, border-color 0.3s ease;
}

.theme-toggle {
  position: absolute;
  top: 1rem;
  right: 1rem;
  width: 2.25rem;
  height: 2.25rem;
  border-radius: 50%;
  border: 1px solid var(--border);
  background: transparent;
  color: var(--text);
  font-size: 1rem;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background 0.2s ease, transform 0.2s ease, color 0.2s ease;
}

.theme-toggle:hover {
  background: var(--bg);
  transform: rotate(15deg);
}

.avatar {
  width: 110px;
  height: 110px;
  margin: 0 auto 1.25rem;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent), #94a3b8);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 2rem;
  letter-spacing: 0.05em;
  box-shadow: var(--shadow);
}

.name {
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: 0.01em;
}

.tagline {
  margin-top: 0.4rem;
  color: var(--muted);
  font-size: 0.95rem;
}

.links {
  list-style: none;
  margin-top: 1.75rem;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.link-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.85rem 1rem;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: var(--surface);
  color: var(--text);
  text-decoration: none;
  font-weight: 500;
  font-size: 1rem;
  transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease,
    color 0.2s ease, box-shadow 0.2s ease;
}

.link-btn:hover {
  transform: translateY(-2px);
  border-color: var(--accent);
  background: var(--accent);
  color: #fff;
  box-shadow: var(--shadow);
}

.link-btn:hover .icon {
  background: rgba(255, 255, 255, 0.2);
  color: #fff;
}

.icon {
  width: 2rem;
  height: 2rem;
  border-radius: 8px;
  background: var(--bg);
  color: var(--accent);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 0.9rem;
  text-transform: lowercase;
  transition: background 0.2s ease, color 0.2s ease;
}

.label {
  flex: 1;
  text-align: left;
}

@media (max-width: 480px) {
  .card {
    padding: 2rem 1.25rem 1.5rem;
    border-radius: 16px;
  }

  .avatar {
    width: 96px;
    height: 96px;
    font-size: 1.75rem;
  }
}
</style>
