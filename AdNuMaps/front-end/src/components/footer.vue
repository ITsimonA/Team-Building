<script setup>
import { ref, computed } from 'vue'

const search = ref('')

const directory = [
  {
    category: 'Gates',
    places: ['2nd Gate', '3rd Gate', 'Main Gate'],
  },
  {
    category: 'Academic',
    places: [
      'Adriatico',
      'Arrupe',
      'Bio Lab',
      'Bonoan',
      'Burns',
      'College Reading Center',
      'Dolan',
      'Engineering Building',
      'Entrepreneur Bldg',
      "James O'Brien Library",
      'Madrigal Bldg',
      'Phelan',
      'Richie Fernando Hall',
      'Santos',
      'SHS Bldg',
    ],
  },
  {
    category: 'Administration',
    places: [
      'ACLC',
      'Administration Building',
      'H.E. Bldg',
      'Physical Plant Admin',
      'Triumph Office',
      'Xavier Hall (OSA / SSG)',
    ],
  },
  {
    category: 'Dining',
    places: ['Bonoan Cafeteria', 'Coko Cafe', 'IGP Cafe'],
  },
  {
    category: 'Sports & Recreation',
    places: [
      'Alingal Multi-purpose Hall',
      'Covered Courts',
      'Eco Garden',
      'Football Field',
      'Ignatius Park',
      'Tennis Court',
    ],
  },
  {
    category: 'Student Life',
    places: ['Faber Center', 'Jesuit Residence', 'M.R.', 'University Gym', 'University Press'],
  },
  {
    category: 'Religious',
    places: ['Christ the King Church'],
  },
]

const filteredDirectory = computed(() => {
  const query = search.value.trim().toLowerCase()
  if (!query) return directory

  return directory
    .map((group) => ({
      category: group.category,
      places: group.places.filter((place) => place.toLowerCase().includes(query)),
    }))
    .filter((group) => group.places.length > 0)
})

const markedPlace = ref(null)

function markPlace(place) {
  markedPlace.value = place
  // TODO: hook this up to the map (e.g. emit event, set pin, etc.)
}
</script>

<template>
  <section class="directory-section">
    <div class="directory-card">
      <div class="directory-header">
        <h2 class="directory-title">
          <span class="pin-icon">📍</span>
          Campus directory
        </h2>
        <span class="directory-hint">Tap a place to mark it</span>
      </div>

      <input
        v-model="search"
        type="text"
        class="search-input"
        placeholder="Search buildings..."
      />

      <div class="directory-list">
        <template v-for="group in filteredDirectory" :key="group.category">
          <div class="category-header">{{ group.category.toUpperCase() }}</div>
          <button
            v-for="place in group.places"
            :key="place"
            type="button"
            class="place-item"
            :class="{ active: markedPlace === place }"
            @click="markPlace(place)"
          >
            <span class="place-dot" />
            {{ place }}
          </button>
        </template>

        <p v-if="filteredDirectory.length === 0" class="no-results">
          No matching places found.
        </p>
      </div>
    </div>

    <p class="disclaimer">
      Distances are approximate, scaled from the published campus map — use them as a general
      guide, not a survey.
    </p>
  </section>
</template>

<style scoped>
.directory-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 1.25rem 1.5rem;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.directory-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(15, 23, 42, 0.08);
  padding: 1.5rem;
  width: 80rem;
  max-width: 100%;
  box-sizing: border-box;
}

.directory-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.9rem;
}

.directory-title {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 1.05rem;
  font-weight: 700;
  color: #0f172a;
  margin: 0;
}

.pin-icon {
  font-size: 1rem;
}

.directory-hint {
  font-size: 0.8rem;
  color: #94a3b8;
}

.search-input {
  width: 100%;
  box-sizing: border-box;
  padding: 0.6rem 0.85rem;
  border-radius: 8px;
  border: 1px solid #e2e8f0;
  background: #f8fafc;
  font-size: 0.9rem;
  color: #334155;
  margin-bottom: 0.75rem;
  outline: none;
  transition: border-color 0.15s ease;
}

.search-input:focus {
  border-color: #94a3b8;
}

.search-input::placeholder {
  color: #94a3b8;
}

.directory-list {
  max-height: 18rem;
  overflow-y: auto;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
}

.category-header {
  position: sticky;
  top: 0;
  background: #eaf2fb;
  color: #64748b;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  padding: 0.5rem 1rem;
  z-index: 1;
}

.place-item {
  display: flex;
  align-items: center;
  gap: 0.55rem;
  width: 100%;
  box-sizing: border-box;
  background: none;
  border: none;
  border-bottom: 1px solid #f1f5f9;
  padding: 0.65rem 1rem;
  font-size: 0.88rem;
  color: #1e293b;
  text-align: left;
  cursor: pointer;
  transition: background 0.12s ease;
}

.place-item:hover {
  background: #f8fafc;
}

.place-item.active {
  background: #eaf2fb;
  color: #0f172a;
  font-weight: 600;
}

.place-item:last-child {
  border-bottom: none;
}

.place-dot {
  width: 0.4rem;
  height: 0.4rem;
  border-radius: 50%;
  background: #0f172a;
  flex-shrink: 0;
}

.no-results {
  padding: 1rem;
  text-align: center;
  color: #94a3b8;
  font-size: 0.85rem;
}

/* scrollbar styling to match design */
.directory-list::-webkit-scrollbar {
  width: 8px;
}

.directory-list::-webkit-scrollbar-track {
  background: transparent;
}

.directory-list::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 4px;
}

.disclaimer {
  margin-top: 0.85rem;
  font-size: 0.78rem;
  color: #94a3b8;
  text-align: center;
}
</style>