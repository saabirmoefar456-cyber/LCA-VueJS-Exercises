<template>
<header class="header">
  <div class="header-inner">
    <div class="header-text">
      <h1 class="header-title">🍢 Cape Town Food Fest 2026</h1>
      <p class="header-subtitle">
        Two days of incredible food, live music, and community — 14 & 15 August, Green Point Park
      </p>
    </div>
    <button class="dark-toggle" @click="emit('toggle-dark')">
      {{ isDark ? '☀️ Light' : '🌙 Dark' }}
    </button>
  </div>
</header>
</template>

<script setup>
defineProps({
isDark: {
  type: Boolean,
  default: false,
},
})

const emit = defineEmits(['toggle-dark'])
</script>

<style scoped>
.header {
background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
padding: 48px 24px 40px;
text-align: center;
position: relative;
}

.header-inner {
max-width: 1100px;
margin: 0 auto;
display: flex;
flex-direction: column;
align-items: center;
gap: 16px;
}

.header-title {
font-size: 36px;
font-weight: 800;
color: #ffffff;
letter-spacing: -0.5px;
margin-bottom: 10px;
}

.header-subtitle {
font-size: 16px;
color: rgba(255, 255, 255, 0.65);
max-width: 520px;
line-height: 1.6;
}

.dark-toggle {
margin-top: 8px;
padding: 8px 20px;
border-radius: 50px;
border: 1px solid rgba(255, 255, 255, 0.25);
background: rgba(255, 255, 255, 0.08);
color: #fff;
font-size: 13px;
font-weight: 500;
cursor: pointer;
transition: background 0.2s;
}

.dark-toggle:hover {
background: rgba(255, 255, 255, 0.15);
}

@media (max-width: 600px) {
.header-title {
  font-size: 24px;
}
}
</style>