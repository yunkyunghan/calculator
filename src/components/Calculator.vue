<template>
  <div class="calculator">
    <div class="display ">{{current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="devide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
    data() {
      return {
        previous: null,
        current : '', 
        operator: null,
        operatorClicked: false
      }
    },

    methods: {
      clear() {
        this.current = '';
      },

      sign() { //charAt(index)는 string으로 저장된 문자열 중에서 한 글자만 선택해서 char타입으로 변환
      this.current = this.current.charAt(0) == '-'? this.current.slice(1) : `-${this.current}`;
    },

    percent() {
      this.current = `${parseFloat(this.current)/ 100}`;
    },

    append(number) { //number을 요소 끝부분에 삽입
    if(this.operatorClicked){
      this.current ='';
      this.operatorClicked = false;
    }
      this.current = `${this.current}${number}`; 
    },

    dot(){ //이미 '.'이 있으면 그 후로는 안찍힘, -1은 없는 경우를 뜻함
       if(this.current.indexOf('.') === -1){
         this.append('.');
       }
    },

    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    }, 

    devide() {
      this.operator = (a,b) => a / b;
      this.setPrevious();
    },

    times(){
      this.operator = (a,b) => a * b;
      this.setPrevious();
    },

    minus() {
      this.operator = (a,b) => b -a ;
      this.setPrevious();
    },

    add(){
      this.operator = (a,b) => a + b;
      this.setPrevious();
    },

    equal(){
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`;
      this.previous = null;
    },

    btn() {
   cursor:pointer
   }
    }

  } 
</script>

<style scoped>
  .calculator{
    width: 400px;
    margin: 0 auto;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    grid-column: 1/5;
    background-color: #333;
    color: white;
  }

  .zero {
    grid-column :1/3;
  }

  .btn{
    background-color: #f2f2f2;
    border: 1px solid #999;
  }

  .operator {
    background-color: orange;
    color: white;
  } 

  .btn:active {
   transform: scale(0.95);
  }
  
</style>
