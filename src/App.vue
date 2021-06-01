<template> 
    <div class="container">
      <input class="input" type="number" v-model="operator1">
      <Button @calculate="action = $event" @clean="cleanHandler"/>
      <input class="input" type="number" v-model="operator2">
      <Result :result="result" />      
    </div>    
    <Numkeypad @ekeypad="ekpInput" @toggleHandle="toggle = $event"/>
</template>

<script>
import Button from './components/Button.vue'
import Result from './components/Result.vue'
import Numkeypad from './components/NumKeypad.vue'

export default {
  name: 'App',
  components: {
    Button,
    Result,
    Numkeypad
  },
  data() {
    return {      
      action: '0',
      operator1: '',
      operator2: '', 
      operand: '',
      toggle: '1'
    }
  },
  methods: {
    cleanHandler() {
      this.action ='0'
      this.operator1 =''
      this.operator2 ='' 
      this.operand = ''     
    },
    ekpInput(item) {      
      if (item === '\u2190') {
        this.operand = this.operand.slice(0, (this.operand.length - 1))
      } else { 
        this.operand += (item === '0' && this.operand === '') ? '' : item;
      } 
      this.toggle === '1' ? this.operator1 = this.operand : this.operator2 = this.operand        
    }
  },
  watch: {
    toggle(value){
      this.operand = '';
      value === '1' ? this.operator1 = '' : this.operator2 = '' 
    }
  },
  computed: {
     result() {
      if (!(this.operator1 && this.operator2)) {        
        return 'Введите операнды'
      } else {
        switch (this.action) {
          case '+':
            return +this.operator1 + +this.operator2; 
          case '-':
            return +this.operator1 - +this.operator2;
          case '*':
            return +this.operator1 * +this.operator2;        
          case '/':
            return +this.operator1 / +this.operator2;
          case 'e':
            return (+this.operator1) ** (+this.operator2);
          case 'i':
            return Math.floor(+this.operator1 / +this.operator2); 
          default:
            return ''
        }
      }
    }
  }
}
</script>

<style>
.input {
    width: 400px;
    height: 25px;
    padding-left: 5px;
    font-size: 16px;
}
</style>
