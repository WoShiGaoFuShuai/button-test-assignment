<template>
  <AppButton :currentColor="currentColor" :currentIcon="currentIcon" />
  <AppSettings
    @changeColor="setColorToButton"
    @changeIcon="setIconToButton"
    @resetIcon="resetIcon"
  />
</template>

<script setup>
import { ref } from '@vue/reactivity';
import AppButton from './components/AppButton.vue';
import AppSettings from './components/AppSettings.vue';

const setColorToButton = (value) => {
  currentColor.value = value;
};

const setIconToButton = (value) => {
  let path = '../src/assets/settingsData/imgs/';
  switch (value) {
    case 'bigArrow':
      currentIcon.value = path + 'Big-arrow.svg';
      break;

    case 'cancel':
      currentIcon.value = path + 'Cancel.svg';
      break;

    case 'questionMark':
      currentIcon.value = path + 'Question-mark.svg';
      break;

    case 'smallArrow':
      currentIcon.value = path + 'Small-arrow.svg';
      break;

    case 'smallArrow':
      currentIcon.value = path + 'Small-arrow.svg';
      break;

    case 'google':
      currentIcon.value = path + 'Google.svg';
      break;

    case 'vk':
      currentIcon.value = path + 'Vk.svg';
      break;

    case 'ok':
      currentIcon.value = path + 'Ok.svg';
      break;

    case 'pen':
      currentIcon.value = path + 'Pen.svg';
      break;
  }
};

const resetIcon = () => {
  currentIcon.value = null;
};

const currentColor = ref('primary');
const currentIcon = ref(null);
</script>

<style scoped></style>
