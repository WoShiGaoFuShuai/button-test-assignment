<template>
  <div class="button-wrapper">
    <div class="button-item">
      <h1 class="title">Result:</h1>
      <div v-if="!isLink">
        <button :class="['btn', bgColor]">
          <img
            :class="[
              'image',
              {
                purple: props.btnText === 'Повторное письмо',
                white: props.currentColor === 'primary',
              },
            ]"
            :src="props.currentIcon"
            alt=""
          />
          <h3 class="btn-text">
            {{ props.btnText }}
          </h3>
          <span class="timer" v-if="props.showTimer"
            >{{ displayMinutes }} : {{ displaySeconds }}</span
          >
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
import { computed, ref, watch } from '@vue/runtime-core';

// PROPS ///////////////////////////////////////////////
const props = defineProps({
  currentColor: { type: String, required: true },
  btnText: { type: String, required: true },
  currentIcon: { type: String, required: false },
  isLink: { type: Boolean, required: true },
  showTimer: { type: Boolean, required: false },
});

// COMPUTED ///////////////////////////////////////////////
const bgColor = computed(() => {
  return props.currentColor;
});

const displayMinutes = computed(() => {
  let mins = Math.floor(totalSeconds.value / 60);
  return formatTime(mins);
});

const displaySeconds = computed(() => {
  let secs = Math.floor(totalSeconds.value % 60);
  return formatTime(secs);
});

//DATA
const minutes = ref(3);
const seconds = ref(0);
const totalSeconds = ref(minutes.value * 60);
const timerInstance = ref(null);

//FUNCTIONS
const formatTime = (time) => {
  if (time < 10) {
    return '0' + time;
  }
  return time.toString();
};

const startTimer = () => {
  timerInstance.value = setInterval(() => {
    totalSeconds.value = totalSeconds.value -= 1;
  }, 1000);
};

//WATCHER
watch(
  () => props.showTimer,
  (newValue) => {
    if (newValue) {
      startTimer();
    } else {
      clearInterval(timerInstance.value);
      timerInstance.value = null;
      totalSeconds.value = minutes.value * 60;
    }
  }
);

watch(
  () => totalSeconds.value,
  (newValue) => {
    if (newValue == 0) {
      clearInterval(timerInstance.value);
      timerInstance.value = null;
    }
  }
);
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
  border-radius: 20px;
  padding: 14px 46px;

  outline: none;
  border: none;
  transition: 1s all ease-in;
  position: relative;
  cursor: pointer;
}

.btn-text {
  display: inline-block;
  font-size: 18px;
  line-height: 24px;
}

.image {
  max-height: 30px;
  max-width: 20px;
  position: absolute;
  top: 14px;
  left: 14px;
}

.image.purple {
  filter: brightness(0) saturate(100%) invert(24%) sepia(20%) saturate(3548%)
    hue-rotate(257deg) brightness(92%) contrast(97%);
}

.image.white {
  filter: brightness(0) saturate(100%) invert(100%) sepia(2%) saturate(720%)
    hue-rotate(262deg) brightness(115%) contrast(100%);
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

.timer {
  background-color: #df3f3e;
  padding: 6px 12px;
  border-radius: 12px;
  margin-left: 4px;
}

@media (max-width: 640px) {
  .btn {
    width: 60px;
    height: 60px;
    padding: 0;
  }

  .btn-text {
    display: none;
  }

  .image {
    max-width: 30px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

@media (max-width: 425px) {
  .btn {
    width: 52px;
    height: 52px;
  }

  .image {
    max-width: 24px;
    max-height: 24px;
  }
}
</style>
