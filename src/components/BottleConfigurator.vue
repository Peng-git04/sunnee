<template>
  <div class="card">

    <!-- LEFT PANEL -->
    <div class="left">

      <!-- Brand -->
      <div class="brand">Sunnee <span>Kids</span></div>
      <p class="tagline">Personalizza la tua bottiglia</p>

      <!-- SUCCESS STATE -->
      <template v-if="done">
        <div class="success">
          <div class="success-icon">🎉</div>
          <h2 class="success-title">Bottiglia creata!</h2>
          <p class="success-msg">
            La tua bottiglia è pronta. Riceverai un regalo speciale con
            il tuo primo ordine Sunnee Kids!
          </p>
          <div class="recap">
            <div v-for="(item, i) in recapItems" :key="i" class="recap-row">
              <span class="recap-dot" :style="{ background: item.hex }"/>
              {{ item.part }}: <strong>{{ item.name }}</strong>
            </div>
          </div>
          <button class="btn-ghost" @click="restart">Ricomincia</button>
        </div>
      </template>

      <!-- CONFIGURATOR STATE -->
      <template v-else>
        <StepsBar :step="step" :total="3" />

        <p class="step-title">{{ STEPS[step].label }}</p>
        <p class="step-desc">{{ STEPS[step].desc }}</p>

        <ColorGrid :selected="chosen[step]" @select="selectColor" />

        <div class="actions">
          <button v-if="step > 0" class="btn-ghost" @click="step--">
            ← Indietro
          </button>
          <button
            v-if="step < 2"
            class="btn-primary"
            @click="step++"
          >
            Avanti →
          </button>
          <button
            v-else
            class="btn-send"
            @click="done = true"
          >
            Invia 🎉
          </button>
        </div>
      </template>
    </div>

    <!-- RIGHT PANEL -->
    <BottlePreview :chosen="chosen" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { COLORS, STEPS } from '../data/colors.js'
import StepsBar      from './StepsBar.vue'
import ColorGrid     from './ColorGrid.vue'
import BottlePreview from './BottlePreview.vue'

const step   = ref(0)
const chosen = ref([6, 5, 4])
const done   = ref(false)

function selectColor(idx) {
  const next = [...chosen.value]
  next[step.value] = idx
  chosen.value = next
}

function restart() {
  step.value = 0
  chosen.value = [6, 5, 4]
  done.value = false
}

const recapItems = computed(() => [
  { part: 'Tappo', hex: COLORS[chosen.value[0]].hex, name: COLORS[chosen.value[0]].name },
  { part: 'Corpo', hex: COLORS[chosen.value[1]].hex, name: COLORS[chosen.value[1]].name },
  { part: 'Fondo', hex: COLORS[chosen.value[2]].hex, name: COLORS[chosen.value[2]].name },
])
</script>

<style scoped>
.card {
  display: flex;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 8px 40px rgba(162,155,254,.25);
  background: #fff;
  min-height: 520px;
}

.left {
  flex: 1; padding: 32px 28px;
  display: flex; flex-direction: column;
}

.brand {
  font-family: 'Baloo 2', cursive;
  font-size: 22px; font-weight: 800; color: #A29BFE;
  margin-bottom: 2px;
}
.brand span { color: #FF6B6B; }

.tagline {
  font-size: 11px; font-weight: 700;
  letter-spacing: 1.5px; text-transform: uppercase;
  color: #aaa; margin-bottom: 24px;
}

.step-title { font-size: 20px; font-weight: 900; margin-bottom: 4px; }
.step-desc  { font-size: 13px; color: #aaa; font-weight: 600; margin-bottom: 4px; }

.actions {
  display: flex; gap: 10px; margin-top: auto;
}

.btn-ghost {
  padding: 12px 18px; border-radius: 12px;
  border: 1.5px solid #ddd; background: transparent;
  font-family: 'Nunito', sans-serif; font-weight: 700;
  font-size: 14px; cursor: pointer; color: #888;
  transition: background .2s;
}
.btn-ghost:hover { background: #f5f5f5; }

.btn-primary {
  flex: 1; padding: 13px 20px; border-radius: 12px;
  border: none;
  background: linear-gradient(135deg, #A29BFE, #6C5CE7);
  color: #fff; font-family: 'Nunito', sans-serif;
  font-weight: 800; font-size: 15px; cursor: pointer;
  transition: opacity .2s, transform .2s;
}
.btn-primary:hover { opacity: .9; transform: translateY(-1px); }

.btn-send {
  flex: 1; padding: 13px 20px; border-radius: 12px;
  border: none;
  background: linear-gradient(135deg, #FF6B6B, #FF9F43);
  color: #fff; font-family: 'Nunito', sans-serif;
  font-weight: 800; font-size: 15px; cursor: pointer;
  transition: opacity .2s, transform .2s;
}
.btn-send:hover { opacity: .9; transform: translateY(-1px); }

/* Success */
.success {
  flex: 1; display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  text-align: center;
}
.success-icon  { font-size: 48px; margin-bottom: 14px; }
.success-title {
  font-family: 'Baloo 2', cursive;
  font-size: 24px; color: #A29BFE; margin-bottom: 8px;
}
.success-msg {
  font-size: 13px; color: #999; line-height: 1.7;
  max-width: 260px; margin-bottom: 20px;
}

.recap {
  background: #f7f4ff; border-radius: 14px;
  padding: 14px 20px; width: 100%; max-width: 280px;
  margin-bottom: 20px;
}
.recap-row {
  display: flex; align-items: center; gap: 9px;
  font-size: 13px; font-weight: 700; color: #444;
  margin-bottom: 7px;
}
.recap-row:last-child { margin-bottom: 0; }
.recap-dot {
  width: 16px; height: 16px; border-radius: 50%;
  border: 2px solid rgba(0,0,0,.1); flex-shrink: 0;
}
</style>