<template>
  <div class="calculator">
    <input type="text" v-model="input" />
    <button @click="handleClick('C')">C</button>
    <br>
    <div class="data">
      <div id="buttons-section" v-for="(item, index) in list" :key="index">
        <button @click="handleClick(item)">{{ item }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorVue',
  props: {
    msg: String
  },
  data() {
    return {
      input: '',
      list: [7, 8, 9, '*', 4, 5, 6, '/', 1, 2, 3, '-', 0, '.', '+', '='],
    }
  },
  methods: {
    handleClick(item) {
      if (Number.isInteger(item)) {
        this.input += item;
      } else if (item === '.') {
        if (!this.input.includes('.')) {
          this.input += item;
        }
      } else if (item === '+/-') {
        this.input = String(-parseFloat(this.input));
      } else if (item === 'C') {
        this.input = '';
      } else if (item === '=') {
        try {
          this.input = String(eval(this.input));
        } catch (error) {
          this.input = 'Error';
        }
      } else {
        this.input += ' ' + item + ' ';
      }
    }
  }
}
</script> 

<style>
.data {
  width: 120px;
  margin: auto;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

#buttons-section {
  width: calc(100% / 4);
}
</style>