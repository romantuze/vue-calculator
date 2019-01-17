<template>
  <div class="calculator">
	<div class="display">{{current || '0'}}</div>
 	<div @click="clear" class="count" >C</div>
 	<div @click="sign" class="count">+/-</div>
	<div @click="percent" class="count">%</div>   
    <div @click="divide" class="count">/</div>
    <div @click="append('7')" class="count">7</div>
    <div @click="append('8')" class="count">8</div>
    <div @click="append('9')" class="count">9</div>
    <div @click="times" class="count">x</div>
    <div @click="append('4')" class="count">4</div>
    <div @click="append('5')" class="count">5</div>
    <div @click="append('6')" class="count">6</div>
    <div @click="minus" class="count">-</div>
	<div @click="append('1')" class="count">1</div>
	<div @click="append('2')" class="count">2</div>
	<div @click="append('3')" class="count">3</div>  
    <div @click="add" class="count">+</div>
    <div @click="append('0')" class="count zero">0</div>
    <div @click="dot" class="count">.</div>
    <div @click="equal" class="count">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
    	previous: null,
	     current: '',
	     operator: null,
	     operatorClicked: false
    };
  },
  methods: {
  		setPrevious() {
  			this.previous = this.current;
  			this.operatorClicked = true;
  		},
	  clear() {
	  	this.current = '';
	  },
	  sign() {
	 	 this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
	  },
	  percent() {
	  	this.current = `${parseFloat(this.current)/100}`;
	  },
	  append(number) {
		if(this.operatorClicked) {
		  this.current = '';
		  this.operatorClicked = false;
		}
	  	this.current = `${this.current}${number}`;
	  },
	  dot() {
	  	if(this.current.indexOf('.') === -1) {
	  		this.append('.');
	  	}
	  },
	  divide() {
	  	this.operator = (a,b) => a / b;
	  	this.setPrevious();	  	
	  },
	  times() {
	  	this.operator = (a,b) => a * b;
	  	this.setPrevious();	  
	  },
	  minus() {
	  	this.operator = (a,b) => a - b;
	  	this.setPrevious();	  
	  },
	  add() {
	 	 this.operator = (a,b) => a + b;
	 	 this.setPrevious();
	  },
	  equal() {
	  	this.current = this.operator(
	  		parseFloat(this.current),
	  		parseFloat(this.previous)
	  	);
	  	this.previos = null;
	  }
  }
}
</script>

<style scoped>
.calculator {
	display: grid;
	grid-template-columns: repeat(4,1fr);
	grid-auto-rows: minmax(50px,auto);
	font-size: 40px;
	max-width: 500px;
	margin: 0 auto;
}

a {
  color: #42b983;
}
.display {
	grid-column: 1/5;
	background-color: #333;
	color: white;
	padding: 10px 0;
}
.zero {
	grid-column: 1/3;
}
.count {
	background-color: #eee;
	border: 1px solid #999;
	cursor: pointer;
}
.operator {
	background-color: orange;
	color: white;
}
</style>