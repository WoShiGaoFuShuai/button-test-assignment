<template>
  <div class="settings-wrapper">
    <h2 class="main-title">Settings:</h2>
    <div class="settings-content">
      <div class="settings-color">
        <h3 class="settings-title">Change a color:</h3>
        <ul class="settings-ul">
          <li
            @click="changeColor(item.classname)"
            v-for="(item, i) in colors"
            :key="i"
            :class="[
              'settings-li',
              {
                primary: item.classname === 'primary',
                secondary: item.classname === 'secondary',
                warning: item.classname === 'warning',
                disabled: item.classname === 'disabled',
                info: item.classname === 'info',
                danger: item.classname === 'danger',
                action: item.classname === 'action',
              },
            ]"
          ></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from '@vue/runtime-core';
import { colors } from '../assets/settingsData/settingsData.js';

//EMITS
const emit = defineEmits(['changeColor']);

const changeColor = (classname) => {
  emit('changeColor', classname);
};
</script>

<style scoped>
.settings-wrapper {
  margin-top: 40px;
}

.main-title {
  text-align: center;
  font-size: 26px;
  color: var(--disabled);
  margin-bottom: 20px;
}

.settings-title {
  font-size: 20px;
  color: var(--disabled);
  margin-bottom: 20px;
}

.settings-ul {
  display: flex;
}

.settings-li {
  width: 20px;
  height: 20px;
  margin-right: 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.5s transform ease-in;
}

.settings-li:hover {
  transform: scale(1.1);
}
</style>
