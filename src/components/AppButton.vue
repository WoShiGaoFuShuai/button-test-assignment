<template>
  <div class="button-wrapper">
    <div class="button-item">
      <h1 class="title">Result:</h1>
      <div v-if="!isLink">
        <button :class="['btn', bgColor]">
          <img class="image" :src="props.currentIcon" alt="" />
          {{ props.btnText }}
        </button>
      </div>
      <div v-else>
        <a href="#" target="_blank" class="btn-link">
          {{ btnText }}
        </a>
      </div>
      <div></div>
    </div>
  </div>
</template>

<script setup>
import { computed } from '@vue/runtime-core';

// PROPS ///////////////////////////////////////////////
const props = defineProps({
  currentColor: { type: String, required: true },
  btnText: { type: String, required: true },
  currentIcon: { type: String, required: false },
  isLink: { type: Boolean, required: true },
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
  cursor: pointer;
}

.image {
  max-height: 30px;
  max-width: 20px;
  position: absolute;
  top: 14px;
  left: 14px;
}

.btn-link {
  font-family: 'Nunito', sans-serif;
  font-weight: 700;
  font-size: 16px;
  line-height: 18px;
  color: #767679;
  text-decoration: none;
}

.btn-link:hover {
  /* text-decoration: underline; */
  border-bottom: 1px solid #767679;
}

.btn-link:active {
  color: #c4296c;
  border-bottom: 1px solid #c4296c;
}
</style>
