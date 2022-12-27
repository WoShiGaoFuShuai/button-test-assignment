<template>
  <AppButton :currentColor="currentColor" />
  <AppSettings @changeColor="setColorToButton" />
</template>

<script setup>
import { ref } from '@vue/reactivity';
import AppButton from './components/AppButton.vue';
import AppSettings from './components/AppSettings.vue';

const setColorToButton = (value) => {
  currentColor.value = value;
};

const currentColor = ref('primary');
</script>

<style scoped></style>
