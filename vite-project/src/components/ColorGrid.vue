<template>
  <div class="color-grid">
    <button
      v-for="color in COLORS"
      :key="color.id"
      class="color-btn"
      :class="{ selected: selected === color.id }"
      :style="{ background: color.hex }"
      :title="color.name"
      @click="emit('select', color.id)"
    >
      <span v-if="selected === color.id" class="check">✓</span>
    </button>
  </div>
</template>

<script setup lang="ts">
import { COLORS } from '../data/colors'

defineProps<{
  selected: number
}>()

const emit = defineEmits<{
  (e: 'select', id: number): void
}>()
</script>

<style scoped>
.color-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 12px;
  margin: 8px 0 24px;
}
.color-btn {
  width: 100%; aspect-ratio: 1;
  border-radius: 50%;
  border: 3px solid transparent;
  cursor: pointer;
  position: relative;
  transition: transform .2s, border-color .2s;
  outline: none;
}
.color-btn:hover    { transform: scale(1.08); }
.color-btn.selected { border-color: #2d2d2d; transform: scale(1.13); }

.check {
  position: absolute; inset: 0;
  display: flex; align-items: center; justify-content: center;
  font-size: 15px; font-weight: 900;
  color: #fff;
  text-shadow: 0 1px 4px rgba(0,0,0,.45);
}
</style>