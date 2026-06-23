<script setup>
import { computed } from 'vue'

const props = defineProps({
  course: {
    type: Object,
    required: true,
  },
  saved: {
    type: Boolean,
    required: true,
  },
})

const emit = defineEmits(['save'])

const priceLabel = computed(() =>
  new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'ZAR',
  }).format(props.course.price),
)

const levelClass = computed(() => `level-${props.course.level.toLowerCase()}`)

const save = () => {
  if (!props.course.available || props.saved) {
    return
  }

  emit('save', props.course.id)
}
</script>

<template>
  <article class="course-card" :class="{ soldout: !course.available }">
    <header class="card-head">
      <p class="level-pill" :class="levelClass">{{ course.level }}</p>
      <span v-if="!course.available" class="status sold">Sold Out</span>
      <span v-else class="status live">Available</span>
    </header>

    <h2>{{ course.title }}</h2>
    <p class="chef">with {{ course.chef }}</p>
    <p class="price">{{ priceLabel }}</p>

    <button class="save-btn" :disabled="saved || !course.available" type="button" @click="save">
      {{ saved ? 'Saved' : !course.available ? 'Unavailable' : 'Save to Wishlist' }}
    </button>
  </article>
</template>

<style scoped>
.course-card {
  border: 1px solid var(--border-soft);
  border-radius: 14px;
  background: #fff;
  padding: 1rem;
  display: grid;
  gap: 0.75rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  animation: rise-in 0.35s ease;
}

.course-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 12px 25px rgba(92, 54, 31, 0.14);
}

.card-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.5rem;
}

.level-pill {
  border-radius: 999px;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.2rem 0.7rem;
}

.level-beginner {
  color: #18683a;
  background: #ddf5e4;
}

.level-intermediate {
  color: #8a5200;
  background: #ffe9ca;
}

.level-advanced {
  color: #7b1f13;
  background: #ffd8d2;
}

.status {
  font-size: 0.8rem;
  font-weight: 600;
}

.live {
  color: var(--success);
}

.sold {
  color: var(--danger);
}

h2 {
  font-family: 'Fraunces', Georgia, serif;
  font-size: 1.15rem;
  line-height: 1.25;
}

.chef {
  color: var(--ink-2);
}

.price {
  font-weight: 700;
  font-size: 1.1rem;
}

.save-btn {
  border: none;
  border-radius: 10px;
  padding: 0.6rem 0.8rem;
  cursor: pointer;
  font-weight: 700;
  background: var(--brand);
  color: #fff;
  transition: background-color 0.2s ease;
}

.save-btn:hover:enabled {
  background: var(--brand-deep);
}

.save-btn:disabled {
  cursor: not-allowed;
  opacity: 0.65;
}

.soldout {
  opacity: 0.9;
}

@keyframes rise-in {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
