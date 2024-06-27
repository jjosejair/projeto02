<template>
  <div class="cal">
    <input v-model="display" readonly class="display" />
    <div class="buttons">
      <button v-for="button in buttons" :key="button" @click="handleClick(button)">
        {{ button }}
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'Calculator',
  setup() {
    const display = ref('');

    const buttons = [
      '7', '8', '9', '/',
      '4', '5', '6', '*',
      '1', '2', '3', '-',
      '0', '.', '=', '+',
      'C'
    ];

    const handleClick = (button: string) => {
      if (button === 'C') {
        display.value = '';
      } else if (button === '=') {
        try {
          display.value = eval(display.value);
        } catch (e) {
          display.value = 'Error';
        }
      } else {
        display.value += button;
      }
    };

    return {
      display,
      buttons,
      handleClick
    };
  }
});
</script>

<style scoped>
.cal {
  max-width: 200px;
  margin: 50px auto;
  text-align: center;
  border: 1px solid black;
  padding: 10px;
  border-radius: 10px;
  background-color:rgb(60, 60, 60)

}

.display {
  width: 100%;
  height: 50px;
  margin-bottom: 10px;
  font-size: 2em;
  text-align: right;
  background-color: rgb(180, 180, 180)
  
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  width: 100%;
  height: 50px;
  font-size: 1.5em;
}
</style>