<script setup>
import { ref } from 'vue'

const startLocation = ref('')
const endLocation = ref('')

const emit = defineEmits(['close'])

function swapLocations() {
  const temp = startLocation.value
  startLocation.value = endLocation.value
  endLocation.value = temp
}
</script>

<template>
  <header class="route-header">
    <div class="route-card">
      <div class="route-controls">
        <div class="field-group">
          <label for="start-location">Starting From</label>
          <div class="select-wrapper">
            <select id="start-location" v-model="startLocation">
              <option value="" disabled hidden>Choose a location...</option>
            </select>
            <svg class="chevron" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path
                fill-rule="evenodd"
                d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.94a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z"
                clip-rule="evenodd"
              />
            </svg>
          </div>
        </div>

        <button type="button" class="icon-button swap-button" aria-label="Swap locations" @click="swapLocations">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" aria-hidden="true">
            <path d="M7 7h11l-2.5-2.5M17 17H6l2.5 2.5" stroke-linecap="round" stroke-linejoin="round" />
          </svg>
        </button>

        <div class="field-group">
          <label for="end-location">Going To</label>
          <div class="select-wrapper">
            <select id="end-location" v-model="endLocation">
              <option value="" disabled hidden>Choose a location...</option>
            </select>
            <svg class="chevron" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path
                fill-rule="evenodd"
                d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.94a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z"
                clip-rule="evenodd"
              />
            </svg>
          </div>
        </div>

        <button type="button" class="icon-button close-button" aria-label="Close" @click="emit('close')">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.75" aria-hidden="true">
            <path d="M6 6l12 12M18 6L6 18" stroke-linecap="round" />
          </svg>
        </button>
      </div>

      <div class="divider" />

      <p class="tip">
        Tip: you can also tap any spot on the map below — first tap sets your start, second sets your
        destination.
      </p>
    </div>
  </header>
</template>

<style scoped>
.route-header {
  display: flex;
  justify-content: center;
  padding: 1.25rem;
  /* background-color: red; */
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.route-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(15, 23, 42, 0.08);
  padding: 1.25rem 1.5rem 1rem;
  width: 80rem;
}

.route-controls {
  display: flex;
  align-items: flex-end;
  gap: 0.75rem;
}

.field-group {
  flex: 1;
  min-width: 0;
}

.field-group label {
  display: block;
  margin-bottom: 0.4rem;
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #94a3b8;
}

.select-wrapper {
  position: relative;
}

.select-wrapper select {
  width: 100%;
  appearance: none;
  border: 1px solid #dbe3ee;
  border-radius: 10px;
  background: #fff;
  padding: 0.85rem 2.25rem 0.85rem 1rem;
  font-size: 0.95rem;
  font-weight: 600;
  color: #1e293b;
  cursor: pointer;
}

.select-wrapper select:invalid,
.select-wrapper select option[value=''] {
  color: #1e293b;
}

.select-wrapper select:focus {
  outline: 2px solid #93c5fd;
  outline-offset: 1px;
}

.chevron {
  position: absolute;
  right: 0.85rem;
  top: 50%;
  transform: translateY(-50%);
  width: 1rem;
  height: 1rem;
  color: #64748b;
  pointer-events: none;
}

.icon-button {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  width: 2.5rem;
  height: 2.5rem;
  border: 1px solid #dbe3ee;
  border-radius: 10px;
  background: #fff;
  color: #475569;
  cursor: pointer;
}

.icon-button svg {
  width: 1.1rem;
  height: 1.1rem;
}

.icon-button:hover {
  background: #f8fafc;
}

.swap-button {
  margin-bottom: 0.15rem;
}

.close-button {
  margin-bottom: 0.15rem;
}

.divider {
  margin: 1rem 0 0.85rem;
  border: none;
  border-top: 1px dashed #dbe3ee;
}

.tip {
  font-size: 0.82rem;
  line-height: 1.5;
  color: #94a3b8;
}
</style>
