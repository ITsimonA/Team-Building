<script setup>
import mapImage from '@/assets/AdNuMaps.png'
</script>

<template>
  <section class="map-section">
    <div class="map-card">
      <div class="legend">
        <span class="legend-item">
          <span class="dot start" />
          Start
        </span>
        <span class="legend-item">
          <span class="dot destination" />
          Destination
        </span>
        <span class="legend-item">
          <span class="dot path" />
          Suggested path
        </span>
      </div>

      <div class="map-frame">
        <img :src="mapImage" alt="Campus map" class="map-image" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.map-section {
  display: flex;
  justify-content: center;
  padding: 0 1.25rem 1.25rem;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.map-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(15, 23, 42, 0.08);
  padding: 1.5rem;
  width: 80rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.map-frame {
  width: 100%;
  display: flex;
  justify-content: center;
}

.map-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
}

.legend {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin-bottom: 1rem;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.85rem;
  font-weight: 600;
  color: #475569;
}

.dot {
  width: 0.7rem;
  height: 0.7rem;
  border-radius: 50%;
  display: inline-block;
}

.dot.start {
  background: #22c55e;
}

.dot.destination {
  background: #ef4444;
}

.dot.path {
  background: #f59e0b;
}
</style>