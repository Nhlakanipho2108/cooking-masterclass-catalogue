<script setup>
defineProps({
  wishlistCount: {
    type: Number,
    required: true,
  },
})
</script>

<template>
  <header class="site-header">
    <div>
      <p class="eyebrow">Cooking Masterclass</p>
      <p class="subheading">Explore chef-led classes and save your favorites.</p>
    </div>

    <div class="wishlist-badge" aria-live="polite" aria-label="Wishlist item count">
      Wishlist: <strong>{{ wishlistCount }}</strong>
    </div>
  </header>
</template>

<style scoped>
.site-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.1rem;
  background: linear-gradient(135deg, #fff 0%, #ffe9cd 100%);
  border: 1px solid var(--border-soft);
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(120, 63, 24, 0.08);
  animation: fade-slide-in 0.45s ease;
}

.eyebrow {
  text-transform: uppercase;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  font-weight: 700;
  color: var(--ink-2);
}

.subheading {
  color: var(--ink-2);
}

.wishlist-badge {
  white-space: nowrap;
  border-radius: 999px;
  background: var(--ink-1);
  color: #fff;
  padding: 0.4rem 0.85rem;
  font-weight: 500;
  animation: pulse 0.35s ease;
}

@keyframes fade-slide-in {
  from {
    opacity: 0;
    transform: translateY(-8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0% {
    transform: scale(0.92);
  }
  100% {
    transform: scale(1);
  }
}

@media (max-width: 640px) {
  .site-header {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
