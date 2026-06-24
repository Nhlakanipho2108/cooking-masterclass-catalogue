# cooking-masterclass-catalogue
A Vue 3 + Vite app that presents a modern catalogue of chef-led cooking classes.

The UI includes:

Responsive course cards
Availability filtering
Save-to-wishlist interactions with a live count
Warm editorial styling with custom CSS variables and typography
Stack
Vue 3 (<script setup> + Composition API)
Vite
CSS (no UI framework)
Prerequisites
Node.js ^22.18.0 or >=24.12.0
Setup
npm install
Development
npm run dev
Build and Preview
npm run build
npm run preview
Format Source
npm run format
Scripts
dev: runs the Vite development server
build: creates a production bundle
preview: serves the production build locally
format: formats src/ using oxfmt
Project Structure
src/
  App.vue
  main.js
  assets/
    base.css
    main.css
  components/
    SiteHeader.vue
    CourseCard.vue
Functional Notes
Course data is currently hardcoded in App.vue.
Filtering is handled by a computed visibleCourses value.
Wishlist state is tracked by course IDs in wishlistIds.
CourseCard.vue emits a save event, and App.vue owns the state update.
Sold out courses cannot be saved, and saved courses are disabled in the UI.
Next Enhancements
Persist wishlist state in local storage
Move course data to an API or static JSON
Add automated tests for filtering and save behavior
Add view routing for course details
