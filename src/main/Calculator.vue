<script>
import AppDisplay from '../components/AppDisplay.vue'
import AppButton from '../components/AppButton.vue'

export default {
  data: function () {
    return {
      // The value displayed on the calculator
      displayValue: '0',
      // Clear the display on the next input
      clearDisplay: false,
      // Current operation
      operation: null,
      // Values of current operation
      values: [0, 0],
      // Index of current value
      current: 0
    }
  },
  components: { AppButton, AppDisplay },
  methods: {
    // Resets the calculator to its initial state
    clearMemory() {
      Object.assign(this.$data, this.$options.data())
    },
    // Sets the operation to be performed
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
          // Evaluate the expression using the current operation
          this.values[0] = eval(`${this.values[0]} ${currentOperation} ${this.values[1]}`)

          // If the result is not a number or is infinite, reset the calculator
          if (isNaN(this.values[0]) || !isFinite(this.values[0])) {
            this.clearMemory()
            return;
          }
        } catch (error) {
          // Emit an error event if the expression is invalid
          this.$emit('onError', error)
        }

        // Reset the second value
        this.values[1] = 0

        // Update the display and operation
        this.displayValue = this.values[0]
        this.operation = equals ? null : operation
        this.current = equals ? 0 : 1
        this.clearDisplay = !equals
      }
    },
    // Adds a digit to the current value
    addDigit(event) {
      let number = event.target.textContent
      if (number === '.' && this.displayValue.includes('.')) {
        return
      }

      // Determine whether to clear the display or append the digit
      const clearDisplay = this.displayValue === '0' || this.clearDisplay
      const currentValue = clearDisplay ? '' : this.displayValue
      const displayValue = currentValue + number

      // Update the display and clearDisplay flag
      this.displayValue = displayValue
      this.clearDisplay = false

      // Update the current value
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
  grid-template-rows: 1fr 3rem 3rem 3rem 3rem;
}
</style>
