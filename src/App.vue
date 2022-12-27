<template>
  <AppButton
    :currentColor="currentColor"
    :currentIcon="currentIcon"
    :isLink="isLink"
    :btnText="btnText"
    :showTimer="showTimer"
  />
  <AppSettings
    @changeColor="setColorToButton"
    @changeIcon="setIconToButton"
    @resetIcon="resetIcon"
    @changeToLinkOrButton="changeToLinkOrButton"
    @showTimer="showTimerInButton"
  />
</template>

<script setup>
import { ref } from '@vue/reactivity';
import AppButton from './components/AppButton.vue';
import AppSettings from './components/AppSettings.vue';

// FUNCTIONS ////////////////////////////////////////////
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

const changeToLinkOrButton = (payload) => {
  isLink.value = payload.value;
  if (isLink.value) {
    btnText.value = 'Напомнить PIN-код';
  } else {
    btnText.value = 'Отправить письмо';
  }
};

const showTimerInButton = (payload) => {
  showTimer.value = payload.value;
  if (payload.value) {
    btnText.value = 'Повторное письмо';
    currentColor.value = 'disabled';
  } else {
    btnText.value = 'Отправить письмо';
    currentColor.value = 'primary';
  }
};

// DATA //////////////////////////////
const currentColor = ref('primary');
const currentIcon = ref(null);
const isLink = ref(false);
const btnText = ref('Отправить письмо');
const showTimer = ref(false);
</script>

<style scoped></style>
