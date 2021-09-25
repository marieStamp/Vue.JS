<template>
    <div class="calc">
        <div class="main">
            <input v-model.number="op1" type="number"/>
            <input v-model.number="op2" type="number"/>
            = {{ result }}
        </div>
        <div class="error">
          {{ error }}
        </div>
        <div class="keyboard">
            <button @click="sum(op1, op2)">+</button>
            <button @click="sub(op1, op2)">-</button>
            <button @click="div">/</button>
            <button @click="multi">*</button>
            <button @click="power">x^y</button>
            <button @click="quotient">//</button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      op1: 0,
      op2: 0,
      error: '',
      result: 0
    }
  },
  methods: {
    sum (op1, op2) {
      this.error = ''
      this.result = op1 + op2
    },
    sub (op1, op2) {
      this.error = ''
      this.result = op1 - op2
    },
    div () {
      const { op1, op2 } = this
      if (op2 === 0) {
        this.error = 'На 0 делить нельзя!'
      }
      this.result = op1 / op2
    },
    multi () {
      const { op1, op2 } = this
      this.error = ''
      this.result = op1 * op2
    },
    power () {
      const { op1, op2 } = this
      this.error = ''
      this.result = op1 ** op2
    },
    quotient () {
      const { op1, op2 } = this
      if (op2 === 0) {
        this.error = 'На 0 делить нельзя!'
      }
      this.result = Math.trunc(op1 / op2)
    }
  }
}
</script>

<style scoped lang="scss">
.error {
  color: red;
}
</style>
