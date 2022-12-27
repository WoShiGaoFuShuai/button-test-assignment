<template>
  <div class="button-wrapper">
    <div class="button-item">
      <h1 class="title">Result:</h1>
      <button :class="['btn', bgColor]">{{ btnText }}</button>
    </div>
  </div>
</template>

<script setup>
import { computed } from '@vue/runtime-core';

const props = defineProps({
  currentColor: { type: String, required: true },
  btnText: { type: String, default: 'Отправить письмо' },
});

const bgColor = computed(() => {
  return props.currentColor;
});
</script>

<style scoped>
.button-wrapper {
  text-align: center;
}

.title {
  font-size: 30px;
  color: var(--disabled);
  margin-bottom: 20px;
}

.btn {
  font-size: 18px;
  line-height: 24px;
  padding: 14px 46px;
  border-radius: 20px;
  outline: none;
  border: none;
  transition: 1s all ease-in;
}
</style>
