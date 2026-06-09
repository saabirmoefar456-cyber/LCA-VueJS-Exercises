<template>
<div
  class="card"
  :class="{
    'card--featured': ticket.featured,
    'card--favourited': ticket.isFavourited,
  }"
>
  <div v-if="ticket.featured" class="featured-badge">⭐ Featured</div>

  <div class="card-header" :class="`tier--${ticket.name.toLowerCase()}`">
    <span class="tier-icon">{{ tierIcon }}</span>
    <h2 class="tier-name">{{ ticket.name }}</h2>
    <p class="tier-price">R {{ ticket.price }}</p>
    <p class="tier-description">{{ ticket.description }}</p>
  </div>

  <div class="card-body">
    <ul class="benefits-list">
      <li v-for="(benefit, index) in ticket.benefits" :key="index">
        ✓ {{ benefit }}
      </li>
    </ul>
  </div>

  <div class="card-footer">
    <button class="notify-btn">🎟 Notify Me</button>
    <button
      class="fav-btn"
      :class="{ 'fav-btn--active': ticket.isFavourited }"
      @click="emit('favourite', ticket.id)"
    >
      {{ ticket.isFavourited ? '♥' : '♡' }}
      {{ ticket.isFavourited ? 'Saved' : 'Save' }}
    </button>
  </div>
</div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
ticket: {
  type: Object,
  required: true,
},
})

const emit = defineEmits(['favourite'])

const tierIcon = computed(() => {
if (props.ticket.name === 'Bronze') return '🥉'
if (props.ticket.name === 'Silver') return '🥈'
if (props.ticket.name === 'Gold') return '🥇'
return '🎟'
})
</script>

<style scoped>
.card {
background: #ffffff;
border-radius: 20px;
overflow: hidden;
box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
display: flex;
flex-direction: column;
border: 2px solid transparent;
transition: transform 0.22s ease, box-shadow 0.22s ease;
position: relative;
}

.card:hover {
transform: translateY(-5px);
box-shadow: 0 16px 32px rgba(0, 0, 0, 0.12);
}

.card--featured {
border-color: #f5c842;
box-shadow: 0 4px 24px rgba(245, 200, 66, 0.25);
transform: scale(1.03);
}

.card--featured:hover {
transform: scale(1.03) translateY(-5px);
}

.card--favourited {
border-color: #e05c8a;
}

.featured-badge {
position: absolute;
top: 14px;
right: 14px;
background: #f5c842;
color: #1a1a2e;
font-size: 11px;
font-weight: 700;
padding: 4px 12px;
border-radius: 50px;
text-transform: uppercase;
letter-spacing: 0.5px;
}

.card-header {
padding: 32px 24px 24px;
text-align: center;
color: #fff;
}

.tier--bronze {
background: linear-gradient(135deg, #a0674a, #cd7f32);
}

.tier--silver {
background: linear-gradient(135deg, #6e7f8d, #a8b8c8);
}

.tier--gold {
background: linear-gradient(135deg, #b8860b, #f5c842);
}

.tier-icon {
font-size: 48px;
display: block;
margin-bottom: 8px;
}

.tier-name {
font-size: 24px;
font-weight: 800;
margin-bottom: 6px;
}

.tier-price {
font-size: 32px;
font-weight: 900;
margin-bottom: 8px;
}

.tier-description {
font-size: 13px;
opacity: 0.85;
line-height: 1.5;
}

.card-body {
padding: 24px;
flex: 1;
}

.benefits-list {
list-style: none;
display: flex;
flex-direction: column;
gap: 10px;
}

.benefits-list li {
font-size: 14px;
color: #444;
display: flex;
align-items: flex-start;
gap: 8px;
line-height: 1.4;
}

.card-footer {
padding: 16px 24px;
border-top: 1px solid #f0f0f0;
display: flex;
gap: 10px;
}

.notify-btn {
flex: 1;
padding: 10px;
border-radius: 50px;
border: none;
background: #1a1a2e;
color: #fff;
font-size: 13px;
font-weight: 600;
cursor: pointer;
transition: background 0.2s;
}

.notify-btn:hover {
background: #2d2d4e;
}

.fav-btn {
padding: 10px 16px;
border-radius: 50px;
border: 2px solid #e05c8a;
background: transparent;
color: #e05c8a;
font-size: 13px;
font-weight: 600;
cursor: pointer;
transition: all 0.2s;
}

.fav-btn:hover {
background: #e05c8a;
color: #fff;
}

.fav-btn--active {
background: #e05c8a;
color: #fff;
}

.dark .card {
background: #1e1e2e;
}

.dark .benefits-list li {
color: #ccc;
}

.dark .card-footer {
border-color: #2a2a3e;
}
</style>