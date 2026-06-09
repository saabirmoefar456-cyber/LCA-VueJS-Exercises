<template>
<div class="app" :class="{ dark: isDark }">
  <AppHeader :is-dark="isDark" @toggle-dark="isDark = !isDark" />

  <main class="main">
    <div class="container">
      <div class="tickets-grid">
        <TicketCard
          v-for="ticket in tickets"
          :key="ticket.id"
          :ticket="ticket"
          @favourite="toggleFavourite"
        />
      </div>
    </div>
  </main>

  <footer class="footer">
    <p>© 2026 Cape Town Food Fest · All rights reserved</p>
  </footer>
</div>
</template>

<script setup>
import { ref } from 'vue'
import AppHeader from './components/AppHeader.vue'
import TicketCard from './components/TicketCard.vue'
import { tickets as rawTickets } from './data/tickets.js'

const isDark = ref(false)

const tickets = ref(rawTickets.map(t => ({ ...t, isFavourited: false })))

function toggleFavourite(id) {
const ticket = tickets.value.find(t => t.id === id)
if (ticket) ticket.isFavourited = !ticket.isFavourited
}
</script>

<style>
*, *::before, *::after {
box-sizing: border-box;
margin: 0;
padding: 0;
}

body {
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
min-height: 100vh;
}

.app {
min-height: 100vh;
background: #f7f5f2;
color: #1a1a2e;
transition: background 0.3s, color 0.3s;
}

.app.dark {
background: #0f0f1a;
color: #f0f0f0;
}

.main {
padding: 48px 0 60px;
}

.container {
max-width: 1100px;
margin: 0 auto;
padding: 0 24px;
}

.tickets-grid {
display: grid;
grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
gap: 28px;
align-items: start;
}

.footer {
background: #1a1a2e;
color: rgba(255, 255, 255, 0.4);
text-align: center;
padding: 20px;
font-size: 13px;
}

@media (max-width: 600px) {
.tickets-grid {
  grid-template-columns: 1fr;
}
}
</style>