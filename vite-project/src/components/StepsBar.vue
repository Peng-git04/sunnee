<template>
  <div class="steps-bar">
    <template v-for="i in total" :key="i">
      <div
        class="step-dot"
        :class="{
          done:   i - 1 < step,
          active: i - 1 === step,
          idle:   i - 1 > step,
        }"
      >
        {{ i - 1 < step ? '✓' : i }}
      </div>
      <div
        v-if="i < total"
        class="step-line"
        :class="{ done: i - 1 < step }"
      />
    </template>
  </div>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    step:   number
    total?: number
  }>(),
  { total: 3 }
)
</script>

<style scoped>
.steps-bar {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 28px;
}
.step-dot {
  width: 34px; height: 34px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 13px; font-weight: 800;
  flex-shrink: 0;
  transition: all .3s;
}
.step-dot.done   { background: #A29BFE; color: #fff; }
.step-dot.active { background: #FF6B6B; color: #fff; transform: scale(1.1); }
.step-dot.idle   { background: #ede9fe; color: #aaa; }

.step-line {
  flex: 1; height: 3px; border-radius: 3px;
  background: #ede9fe;
  transition: background .4s;
}
.step-line.done { background: #A29BFE; }
</style>