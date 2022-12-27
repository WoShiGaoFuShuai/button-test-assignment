<template>
  <div class="button-wrapper">
    <div class="button-item">
      <h1 class="title">Result:</h1>
      <button :class="['btn', bgColor]">
        <img class="image" :src="props.currentIcon" alt="" />
        {{ btnText }}
      </button>
      <div></div>
    </div>
  </div>
</template>

<script setup>
import { computed } from '@vue/runtime-core';

// PROPS ///////////////////////////////////////////////
const props = defineProps({
  currentColor: { type: String, required: true },
  btnText: { type: String, default: 'Отправить письмо' },
  currentIcon: { type: String, required: false },
});

// COMPUTED ///////////////////////////////////////////////
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
  position: relative;
}

.image {
  max-height: 30px;
  max-width: 20px;
  position: absolute;
  top: 14px;
  left: 20px;
}
</style>
