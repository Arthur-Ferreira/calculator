<script>
import AppDisplay from '../components/AppDisplay.vue'
import AppButton from '../components/AppButton.vue'

export default {
  data: function () {
    return {
      displayValue: '0',
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0
    }
  },
  components: { AppButton, AppDisplay },
  methods: {
    clearMemory() {
      Object.assign(this.$data, this.$options.data())
    },
    setOperation(event) {
      const operation = event.target.textContent

      if (this.current === 0) {
        this.operation = operation
        this.current = 1
        this.clearDisplay = true
      } else {
        const equals = operation === '='
        const currentOperation = this.operation

        try {
          this.values[0] = eval(`${this.values[0]} ${currentOperation} ${this.values[1]}`)
          
          if (isNaN(this.values[0]) || !isFinite(this.values[0])) {
            this.clearMemory()
            return;
          }
        } catch (error) {
          this.$emit('onError', error)
        }

        this.values[1] = 0

        this.displayValue = this.values[0]
        this.operation = equals ? null : operation
        this.current = equals ? 0 : 1
        this.clearDisplay = !equals
      }
    },
    addDigit(event) {
      let number = event.target.textContent
      if (number === '.' && this.displayValue.includes('.')) {
        return
      }

      const clearDisplay = this.displayValue === '0' || this.clearDisplay
      const currentValue = clearDisplay ? '' : this.displayValue
      const displayValue = currentValue + number

      this.displayValue = displayValue
      this.clearDisplay = false

      if (number !== '.') {
        const index = this.current
        const newValue = parseFloat(displayValue)
        this.values[index] = newValue
      }
    }
  }
}
</script>

<template>
  <div class="calculator">
    <AppDisplay :value="displayValue" />
    <AppButton label="AC" triple @click="clearMemory" />
    <AppButton label="/" operation @click="setOperation" />
    <AppButton label="7" @click="addDigit" />
    <AppButton label="8" @click="addDigit" />
    <AppButton label="9" @click="addDigit" />
    <AppButton label="*" operation @click="setOperation" />
    <AppButton label="4" @click="addDigit" />
    <AppButton label="5" @click="addDigit" />
    <AppButton label="6" @click="addDigit" />
    <AppButton label="-" operation @click="setOperation" />
    <AppButton label="1" @click="addDigit" />
    <AppButton label="2" @click="addDigit" />
    <AppButton label="3" @click="addDigit" />
    <AppButton label="+" operation @click="setOperation" />
    <AppButton label="0" double @click="addDigit" />
    <AppButton label="." @click="addDigit" />
    <AppButton label="=" operation @click="setOperation" />
  </div>
</template>


<style>
.calculator {
  height: 18rem;
  width: 18rem;
  border-radius: 5px;
  overflow: hidden;

  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px;
}
</style>
