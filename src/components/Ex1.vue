<script>
export default {
  data() {
    return {
      x: 0,
      y: 0,
      selectedOp: '+',
      operators: ['+', '-', '*', '/']
    };
  },
  computed: {
    result() {
      switch (this.selectedOp) {
        case '+':
          return this.x + this.y;
        case '-':
          return this.x - this.y;
        case '*':
          return this.x * this.y;
        case '/':
          return this.y !== 0 ? this.x / this.y : 'Error (÷0)';
        default:
          return 'Invalid';
      }
    }
  }
};
</script>

<template>
  <p>x <input v-model.number="x"></p>
  <select v-model="selectedOp">
    <option v-for="op in operators" :key="op">{{ op }}</option>
  </select>
  <p>y <input v-model.number="y"></p>

  <p>---------------------</p>

  <p>= {{ result }}</p>
</template>

<style scoped>
p, input {
  font-family: monospace;
}
p {
  white-space: pre;
}
</style>

