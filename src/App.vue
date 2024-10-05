<script setup lang="ts">
import { ref, computed } from "vue";
import BaseInput from "./components/BaseInput.vue";
const a = ref<number>(1);
const b = ref<number>(1);
const c = ref<number>(1);

const setA = (newValue: number): void => {
  a.value = newValue;
};
const setB = (newValue: number): void => {
  b.value = newValue;
};
const setC = (newValue: number): void => {
  c.value = newValue;
};

const D = computed<number>(() => {
  return b.value ** 2 - 4 * a.value * c.value;
});

const X1 = computed<number>(() => {
  return (-b.value + Math.sqrt(D.value)) / (2 * a.value);
});

const X2 = computed<number>(() => {
  return (-b.value - Math.sqrt(D.value)) / (2 * a.value);
});
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
    <h3 class="text_inline">
      Введите коэффициенты
      <span class="red_text">a, b, c</span>
      . Коэффициент
      <span class="red_text">a</span>
      должен быть не равен
      <span class="red_text">0</span>
      .
    </h3>
  </div>
  <div class="equation">
    <BaseInput msg="a" :num="a" @setCount="setA" />
    <p class="equation__text">x<sup>2</sup> +</p>
    <BaseInput msg="b" :num="b" @setCount="setB" />
    <p class="equation__text">x +</p>
    <BaseInput msg="c" :num="c" @setCount="setC" />
  </div>
  <div class="solution">
    <h2>Решение через дискриминант</h2>
    <div class="solution__text">
      <p>Дискриминант: D = b<sup>2</sup> - 4ac</p>
      <p>D = {{ b }}<sup>2</sup> - 4*{{ a }}*{{ c }}</p>
      <p>D = {{ D }}</p>
      <p>Если D > 0 - два корня уравнения</p>
      <p>Если D = 0 - один корень уравнения</p>
      <p>Если D < 0 - нет корней уравнения</p>
      <div v-show="D > 0">
        <p>Корни: X<sub>1,2</sub> = (-b &plusmn; &radic; D )/ 2a</p>
        <p>Корни: X<sub>1</sub> = {{ X1 }}</p>
        <p>Корни: X<sub>2</sub> = {{ X2 }}</p>
      </div>
      <div v-show="D === 0">
        <p>Корень: X = -b / 2a</p>
        <p>Корень: X = {{ X1 }}</p>
      </div>
      <p v-show="D < 0">Корней нет</p>
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.equation {
  display: inline-flex;
  width: 100%;
  flex-direction: row;
  justify-content: center;
  align-items: end;
  font-size: 28px;
  font-weight: 600;
  text-align: end;
}

.equation__text {
  margin: 0;
}

.red_text {
  color: red;
  margin: 0;
  padding: 0;
}
/* .text_inline {
  display: inline-block;
  margin: 0;
} */

.solution__text {
  font-size: 22px;
  font-weight: 400;
}
</style>
