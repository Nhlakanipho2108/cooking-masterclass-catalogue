<script setup>
import { computed, ref } from 'vue'
import CourseCard from './components/CourseCard.vue'
import SiteHeader from './components/SiteHeader.vue'

const courses = [
  {
    id: 1,
    title: 'Knife Skills Essentials',
    chef: 'Chef Marco Bellini',
    level: 'Beginner',
    price: 49,
    available: true,
  },
  {
    id: 2,
    title: 'Rustic Italian Pasta',
    chef: 'Chef Elena Rossi',
    level: 'Intermediate',
    price: 89,
    available: true,
  },
  {
    id: 3,
    title: 'French Sauces Mastery',
    chef: 'Chef Andre Laurent',
    level: 'Advanced',
    price: 120,
    available: false,
  },
  {
    id: 4,
    title: 'Plant-Based Flavor Lab',
    chef: 'Chef Nia Carter',
    level: 'Intermediate',
    price: 75,
    available: true,
  },
  {
    id: 5,
    title: 'Pastry and Plating Studio',
    chef: 'Chef Lucie Moreau',
    level: 'Advanced',
    price: 140,
    available: false,
  },
  {
    id: 6,
    title: 'Weekend Brunch Classics',
    chef: 'Chef Miles Harper',
    level: 'Beginner',
    price: 55,
    available: true,
  },
]

const wishlistIds = ref([])
const showAvailableOnly = ref(false)

const visibleCourses = computed(() => {
  if (!showAvailableOnly.value) {
    return courses
  }

  return courses.filter((course) => course.available)
})

const wishlistCount = computed(() => wishlistIds.value.length)

const toggleAvailableOnly = () => {
  showAvailableOnly.value = !showAvailableOnly.value
}

const isSaved = (id) => wishlistIds.value.includes(id)

const saveCourse = (id) => {
  if (wishlistIds.value.includes(id)) {
    return
  }

  wishlistIds.value = [...wishlistIds.value, id]
}
</script>

<template>
  <div class="page-shell">
    <SiteHeader :wishlist-count="wishlistCount" />

    <main class="catalogue">
      <section class="catalogue-controls">
        <h1>Cooking Masterclass Catalogue</h1>
        <button class="filter-button" type="button" @click="toggleAvailableOnly">
          {{ showAvailableOnly ? 'Showing Available Only' : 'Show Available Only' }}
        </button>
      </section>

      <section class="card-grid" aria-label="Course catalogue">
        <CourseCard
          v-for="course in visibleCourses"
          :key="course.id"
          :course="course"
          :saved="isSaved(course.id)"
          @save="saveCourse"
        />
      </section>
    </main>
  </div>
</template>
