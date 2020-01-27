<template>
  <section class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn aux">C</div>
    <div @click="sign" class="btn aux">+/-</div>
    <div @click="percent" class="btn aux">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn number">7</div>
    <div @click="append('8')" class="btn number">8</div>
    <div @click="append('9')" class="btn number">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn number">4</div>
    <div @click="append('5')" class="btn number">5</div>
    <div @click="append('6')" class="btn number">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn number">1</div>
    <div @click="append('2')" class="btn number">2</div>
    <div @click="append('3')" class="btn number">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn number zero">0</div>
    <div @click="dot" class="btn number dot">.</div>
    <div @click="dot" class="btn number dot"></div>
    <div @click="equal" class="btn operator equal">=</div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-'
        ? this.current.slice(1)
        : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
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
        parseFloat(this.current),
        parseFloat(this.previous),
      )}`;
      this.previous = null;
    },
  },
};
</script>

<style scoped>
.calculator {
  --color-numbers:#818181;
  --color-operator:  #BEBEBE;
  --color-black: #4E4E4E;
  --color-dark: #494949;
  --color-equal: #FE6E70;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(84px, auto);
  margin: 0 auto;
  padding: 4rem 2rem 2rem;
  max-width: 400px;
  width: 100%;
  font-size: 30px;
  color: var(--color-black);
  background: var(--color-dark);
  border-radius: 2rem;
  box-shadow: 0.5rem 1rem 2rem rgba(0, 0, 0, 0.392);
}

.aux {
  color: var(--color-operator);
}

.display {
  position: relative;
  grid-column: 1 / -1;
  display: flex;
  justify-content: flex-end;
  margin-bottom: 2rem;
  padding-right: 1.5rem;
  padding-bottom: 1rem;
  font-size: 4rem;
  color: white;
  font-weight: bold;
}

.display::after {
  position: absolute;
  left: 0;
  bottom: 0;
  content: '';
  width: 100%;
  height: 1px;
  background: var(--color-numbers);
}

.number {
  color: var(--color-numbers);
}

div {
  display: flex;
  justify-content: center;
  align-items: center;
}

.operator {
  color:  var(--color-equal);
}

.equal {
  color: white;
  background: radial-gradient(
    circle at center,
    var(--color-equal) 50%, transparent 50%);
  border-radius: 50%;
  /* box-shadow: 3px 7px 1rem rgba(254, 110, 112, 0.432); */
}

@media screen and (max-width: 360px) {
  .calculator {
    grid-auto-rows: minmax(64px, auto);
    font-size: 24px;
  }
}

</style>
