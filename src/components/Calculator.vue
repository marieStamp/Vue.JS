<template>
    <div class="calc">
        <div class="main">
            <input v-model.number="op1" type="number" @focus="checkedOp"/>
            <input v-model.number="op2" type="number" @focus="checkedOp"/>
            = {{ result }}
        </div>
        <div class="error" v-if="error">
          Ошибка! {{ error }}
        </div>
        <div class="operations">
          <button v-for="(operand, idx) in operands" :key="idx" @click="calculate(operand)">
            {{ operand }}
          </button>
        </div>
        <label>
          <input type="checkbox" v-model="checked"/>
            Отобразить экранную клавиатуру
        </label>
        <div class="keyboard" v-show="checked">
          <button v-for="(number, idx) in keyboard" :key="idx" v-html="number" @click="setValue"></button>
          <br>
          <label>
            <input type="radio" name="operand" value="op1" v-model="checkedOp"/>
              Первый операнд
          </label>
          <label>
            <input type="radio" name="operand" value="op2" v-model="checkedOp"/>
              Второй операнд
          </label>
        </div>
  </div>
</template>

<script lang='js'>
export default {
  name: 'Calculator',
  data () {
    return {
      op1: 0,
      op2: 0,
      error: '',
      operands: ['+', '-', '/', '*', 'x^y', '//'],
      result: 0,
      checkedOp: '',
      checked: false,
      keyboard: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0, '&larr;']
    }
  },
  methods: {
    calculate (operation = '+') {
      this.error = ''
      switch (operation) {
        case '+':
          this.sum()
          break
        case '-':
          this.sub()
          break
        case '*':
          this.multi()
          break
        case '/':
          this.div()
          break
        case 'x^y':
          this.power()
          break
        case '//':
          this.quotient()
          break
      }
    },

    sum () {
      const { op1, op2 } = this
      this.result = op1 + op2
    },
    sub () {
      const { op1, op2 } = this
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
      this.result = op1 ** op2
    },
    quotient () {
      const { op1, op2 } = this
      if (op2 === 0) {
        this.error = 'На 0 делить нельзя!'
      }
      this.result = Math.trunc(op1 / op2)
    },
    focusOperand (e) {
      if (e.target.value === 'op1') {
        this.$els.inputOp1.focus()
      }
    },
    setValue (e) {
      switch (this.checkedOp) {
        case 'op1':
          if (e.target.textContent === '←') {
            const str = this.op1.toString()
            this.op1 = str.slice(0, str.length - 1)
          } else this.op1 = +(this.op1 + e.target.textContent)
          break
        case 'op2':
          if (e.target.textContent === '←') {
            const str = this.op2.toString()
            this.op2 = str.slice(0, str.length - 1)
          } else this.op2 = +(this.op2 + e.target.textContent)
          break
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .error {
    color: red;
  }
  .operations {
    margin: 20px 0;
  }
  .keyboard {
    margin-top: 20px;
  }
</style>
