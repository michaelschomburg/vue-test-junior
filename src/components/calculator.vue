<template>
  <div id="calculator">
  <input type="string" class="calculator-input" v-model="value" @keyup.enter="getResult()">

  <div class="calculator-row">
    <div class="calculator-col">
      <button class="calculator-btn gray action" @click="clear()">C</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn gray action" @click="del()">del</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn gray action" @click="addExpresion('%')">%</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn accent action" @click="addExpresion('/')">/</button>
    </div>
  </div>
  <div class="calculator-row">
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(7)">7</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(8)">8</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(9)">9</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn accent action" @click="addExpresion('*')">*</button>
    </div>
  </div>
  <div class="calculator-row">
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(4)">4</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(5)">5</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(6)">6</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn accent action" @click="addExpresion('-')">-</button>
    </div>
  </div>
  <div class="calculator-row">
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(1)">1</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(2)">2</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn number" @click="addExpresion(3)">3</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn accent action" @click="addExpresion('+')">+</button>
    </div>
  </div>
  <div class="calculator-row">
    <div class="calculator-col wide">
      <button class="calculator-btn zero" @click="addExpresion(0)">0</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn action dot" @click="addExpresion('.')">.</button>
    </div>
    <div class="calculator-col">
      <button class="calculator-btn accent action" @click="getResult">=</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'calculator',
  props: {
    msg: String
  },
    data() {
      return {
          value: 0,
          logs:  []
      }
    },
  methods: {
        addExpresion(e) {
            if ( Number.isInteger(this.value) ) {
              this.value = '';
            }
            this.value += e;
        },
        getResult() {
            let log = this.value;
            this.value = eval(this.value);
            this.logs.push( log + `=${this.value}` );
            this.$emit('get-quote');
        },
        clear() {
            this.value = 0;
        },
        del() {
            this.value = this.value.slice(0, -1);
        }
    }
}
</script>

<style lang="scss" scoped>

    $light-gray: rgba(0, 0, 0, 0.07);;
    $dark-gray: rgba(0, 0, 0, 0.75);;
    $gray: #616163;
    $white: #fff;
    $blue: rgba(61, 171, 255, 1);
    $green: rgba(93,216,139, 1);
    $sd-shadow-1: 0 2px 4px -1px rgba(0, 0, 0, 0.2), 0 1px 10px 0 rgba(0, 0, 0, 0.12), 0 4px 5px 0 rgba(0, 0, 0, 0.14);

    *, ::after, ::before {
        box-sizing: border-box;
    }

    #calculator {
        width: 100%;
        margin: 0 auto;
        display: flex;
        padding: 0;
        max-width: 320px;
        flex-direction: column;
        background-color: $light-gray;
        box-shadow: $sd-shadow-1;

        .calculator-logs {
        height: 80px;
        display: flex;
        position: relative;
        overflow: hidden;
        align-items: flex-end;
        flex-direction: column;
        justify-content: flex-end;
            &:before {
                 top: 0;
                 left: 0;
                 right: 0;
                 height: 48px;
                 content: '';
                 z-index: 5;
                 position: absolute;
                 background: linear-gradient(to bottom, $light-gray, rgba($light-gray, 0));
             }
            span {
                color: $blue;
                opacity: .75;
                display: block;
                font-size: .8rem;
                text-align: right;
                margin-top: .4rem;
                line-height: 1;
                font-weight: lighter;
            }
        }

        .calculator-input {
            color: $blue;
            width: 100%;
            border: none;
            padding: 1rem;
            display: block;
            font-size: 2.4rem;
            background: none;
            text-align: right;
            font-weight: lighter;
            box-shadow: inset -1px -1px 12px -6px rgba(0,0,0,0.55);
                &:focus, &:active {
                          outline: none;
                }
        }

        .calculator-row {
        display: flex;
        padding: 0;
        justify-content: space-around;
            .calculator-col {
                width: 25%;
                padding: 3px;
            &.wide {
                width: 50%;
                }
            }
        }

        .calculator-btn {
            width: 100%;
            color: $blue;
            border: none;
            cursor: pointer;
            padding: .8rem;
            outline: none;
            font-size: 1.6rem;
            transition: all .3s ease-in-out;
            font-weight: 200;
            justify-content: center;
            background-color: $gray;
            box-shadow: 0px 0px 5px 2px rgba(0,0,0,0.25);
                &.accent {
                    background-color: $green;
                    color: $white;
                    height: 100%;
                }
                &.gray {
                    background-color: $dark-gray;
                }
                &.action {
                  color: $white;
                    &.dot {
                        border-radius: 100px;
                        width: 70px;
                        height: 70px;
                      color: $blue;
                    }
                }
                &:active {
                     background-color: $light-gray;
                }
                &.number{
                    border-radius: 115px;
                    width: 70px;
                    height: 70px;
                }
                &.zero {
                    border-radius: 100px;
                    height: 100%;
                }
        }
    }
</style>
