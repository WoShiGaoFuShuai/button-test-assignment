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
      <div class="settings-icons">
        <h3 class="settings-title">Choose an icon:</h3>
        <div class="icons-content">
          <div
            @click="changeIcon(item.name)"
            v-for="(item, i) in icons"
            :key="i"
            class="icons-item"
          >
            <img :src="item.icon" alt="" />
          </div>
          <button @click="resetIcon" class="casual-btn">reset</button>
        </div>
      </div>

      <div class="settings-link">
        <h3 class="settings-title">
          Do you want to change the button to a link?
        </h3>
        <label class="label-link"
          >Yes
          <input
            @change="buttonOrLink"
            class="input-link"
            type="checkbox"
            v-model="isLink"
          />
        </label>
      </div>

      <div :class="['settings-timer', { hide: isLink }]">
        <h3 class="settings-title">Do you want to add timer?</h3>
        <div class="timer-content">
          <label class="label-timer"
            >Yes
            <input
              @change="toggleTimer"
              class="input-timer"
              type="checkbox"
              v-model="showTimer"
              :disabled="showTimer"
            />
          </label>
          <button @click="resetTimer" class="btn-timer casual-btn">
            reset
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from '@vue/runtime-core';
import { colors } from '../assets/settingsData/settingsData.js';
import { icons } from '../assets/settingsData/settingsData.js';

//EMITS ////////////////////////////////
const emit = defineEmits([
  'changeColor',
  'changeIcon',
  'resetIcon',
  'changeToLinkOrButton',
  'showTimer',
]);

const changeColor = (classname) => {
  emit('changeColor', classname);
};

const changeIcon = (icon) => {
  emit('changeIcon', icon);
};

const resetIcon = () => {
  emit('resetIcon');
};

const toggleTimer = () => {
  emit('showTimer', showTimer);
};

// DATA /////////////////////////////
const isLink = ref(false);
const showTimer = ref(false);

//FUNCTIONS //////////////////
const buttonOrLink = () => {
  if (isLink) {
    showTimer.value = false;
    resetTimer();
  }
  emit('changeToLinkOrButton', isLink);
};

const resetTimer = () => {
  showTimer.value = false;
  emit('showTimer', showTimer);
};

//HOOKS
onMounted(() => {
  let body = document.querySelector('body');
  window.addEventListener('resize', () => {
    if (body.offsetWidth <= 640) {
      resetTimer();
    }
  });
});
</script>

<style scoped>
.settings-wrapper {
  margin-top: 40px;
}

.main-title {
  text-align: center;
  font-size: 26px;
  color: var(--disabled);
  margin-bottom: 30px;
}

.settings-color {
  margin-bottom: 26px;
}
.settings-title {
  font-size: 20px;
  color: var(--disabled);
  margin-bottom: 20px;
}

.settings-ul {
  display: flex;
  flex-wrap: wrap;
}

.settings-li {
  width: 20px;
  height: 20px;
  margin-right: 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.5s transform ease-in;
  margin-bottom: 8px;
}

.settings-li:hover {
  transform: scale(1.2);
}

/* // ICONS */
.settings-icons {
  margin-bottom: 26px;
}

.icons-content {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.icons-item {
  margin-right: 10px;
  cursor: pointer;
  transition: 0.5s transform ease-in;
}

.icons-item:hover {
  transform: scale(1.1);
  filter: brightness(0) saturate(100%) invert(21%) sepia(78%) saturate(1115%)
    hue-rotate(259deg) brightness(92%) contrast(96%);
}

.casual-btn {
  background-color: var(--primary);
  padding: 10px 20px;
  border-radius: 40px;
  outline: none;
  border: none;
  cursor: pointer;
  transition: 0.5s all ease-in;
}

.casual-btn:hover {
  transform: scale(1.05);
  background-color: #a83cbe;
}

/* /////////LINK & TIMER */

.settings-link {
  margin-bottom: 26px;
}

.label-link,
.label-timer {
  color: var(--disabled);
  font-size: 20px;
}

.input-link,
.input-timer {
  margin-left: 20px;
  width: 16px;
  height: 16px;
}

/* TIMER */
.btn-timer.casual-btn {
  margin-left: 20px;
}

.timer-content {
  display: flex;
  align-items: center;
}

.settings-timer.hide {
  display: none;
}

@media (max-width: 640px) {
  .settings-timer {
    display: none;
  }
}
</style>
