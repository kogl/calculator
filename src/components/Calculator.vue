<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="btn hej">C</div>
    <div @click="sign" class="btn hej">+/-</div>
    <div @click="percent" class="btn hej">%</div>
    <div @click="divide" class="btn hej operator">÷</div>
    <div @click="append('7')" class="btn hej">7</div>
    <div @click="append('8')" class="btn hej">8</div>
    <div @click="append('9')" class="btn hej">9</div>
    <div @click="times" class="btn hej operator">*</div>
    <div @click="append('4')" class="btn hej">4</div>
    <div @click="append('5')" class="btn hej">5</div>
    <div @click="append('6')" class="btn hej">6</div>
    <div @click="minus" class="btn hej operator">-</div>
    <div @click="append('1')" class="btn hej">1</div>
    <div @click="append('2')" class="btn hej">2</div>
    <div @click="append('3')" class="btn hej">3</div>
    <div @click="add" class="btn hej operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn hej">.</div>
    <div @click="equal" class="btn hej operator">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorCliked: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorCliked) {
        console.log("hej");
        this.current = "";
        this.operatorCliked = false;
      }
      this.current = ` ${this.current} ${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) this.append(".");
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    },

    setPrevious() {
      this.operatorCliked = true;
      this.previous = this.current;
    },
  },
};
</script>

<style scoped>
.calculator {
  width: 500px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 35px;
}

.display {
  grid-column: 1/5;
  background: black;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background: #ccc;
}

.operator {
  background: orange;
  color: white;
}
</style>
