<template>
  <aside class="preview-panel">
    <p class="preview-label">Anteprima</p>

    <svg width="110" height="280" viewBox="0 0 110 280" fill="none">
      <defs>
        <clipPath id="bodyClip">
          <rect x="15" y="80" width="80" height="160" rx="12"/>
        </clipPath>
      </defs>
      <rect x="50" y="4"  width="10" height="16" rx="5"  :fill="capColor"/>
      <rect x="32" y="12" width="46" height="48" rx="10" :fill="capColor"/>
      <rect x="28" y="52" width="54" height="10" rx="4"  fill="white" opacity=".2"/>
      <rect x="36" y="58" width="38" height="26" rx="4"  :fill="capColor" opacity=".85"/>
      <rect x="15" y="80" width="80" height="160" rx="12" :fill="bodyColor"/>
      <rect x="22" y="90" width="14" height="100" rx="7"
        fill="white" opacity=".18" clip-path="url(#bodyClip)"/>
      <rect x="15" y="220" width="80" height="44"
        :fill="bottomColor" clip-path="url(#bodyClip)"/>
      <rect x="15" y="232" width="80" height="6"
        fill="white" opacity=".12" clip-path="url(#bodyClip)"/>
      <rect x="15" y="80" width="80" height="160" rx="12"
        stroke="rgba(0,0,0,.08)" stroke-width="1.5" fill="none"/>
      <rect x="32" y="12" width="46" height="48" rx="10"
        stroke="rgba(0,0,0,.08)" stroke-width="1.5" fill="none"/>
    </svg>

    <div class="legend">
      <div v-for="item in legendItems" :key="item.part" class="legend-row">
        <span class="legend-dot" :style="{ background: item.hex }"/>
        <span class="legend-label">{{ item.part }}:</span>
        <span class="legend-name">{{ item.name }}</span>
      </div>
    </div>
  </aside>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { COLORS } from '../data/colors'

interface LegendItem {
  part: string
  hex:  string
  name: string
}

const props = defineProps<{
  chosen: [number, number, number]
}>()

const capColor    = computed((): string => COLORS[props.chosen[0]].hex)
const bodyColor   = computed((): string => COLORS[props.chosen[1]].hex)
const bottomColor = computed((): string => COLORS[props.chosen[2]].hex)

const legendItems = computed((): LegendItem[] => [
  { part: 'Tappo', hex: capColor.value,    name: COLORS[props.chosen[0]].name },
  { part: 'Corpo', hex: bodyColor.value,   name: COLORS[props.chosen[1]].name },
  { part: 'Fondo', hex: bottomColor.value, name: COLORS[props.chosen[2]].name },
])
</script>

<style scoped>
.preview-panel {
  width: 240px; flex-shrink: 0;
  background: #f7f4ff;
  border-radius: 0 24px 24px 0;
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  padding: 24px;
}
.preview-label {
  font-size: 11px; font-weight: 800;
  color: #A29BFE; letter-spacing: 2px;
  text-transform: uppercase; margin-bottom: 16px;
}
.legend { margin-top: 18px; width: 100%; }
.legend-row {
  display: flex; align-items: center;
  gap: 7px; margin-bottom: 7px; font-size: 11px;
}
.legend-dot {
  width: 12px; height: 12px; border-radius: 50%;
  border: 1.5px solid rgba(0,0,0,.1); flex-shrink: 0;
}
.legend-label { font-weight: 800; color: #888; }
.legend-name  { font-weight: 700; color: #444; }
</style>