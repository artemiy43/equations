<script setup lang="ts">
import { ref } from "vue";

defineProps<{ msg: string; num: Number }>();

//const emits = defineEmits(["setCount"]);

const emits = defineEmits<{
  (e: "setCount", newValue: number): void;
}>();
//const count = ref(0);
</script>

<template>
  <div class="input-container">
    <label class="input__label">{{ msg }}</label>
    <input
      type="number"
      :value="num"
      @input="emits('setCount', $event.target.value)"
      class="input"
    />
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}

.input {
  width: 50px;
  height: 35px;
  font-size: 28px;
  font-weight: 600;
}

.input-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 28px;
  font-weight: 600;
}

.input__label {
  color: red;
}
</style>
