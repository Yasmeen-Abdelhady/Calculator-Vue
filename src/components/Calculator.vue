<template>
    <div class="calculator">
        <div class="display">{{current || 0}}</div>
        <div class="btn" @click="clear">C</div>
        <div class="btn" @click="sign">+/-</div>
        <div class="btn" @click="percentage">%</div>
        <div class="operator" @click="divide">÷</div>
        <div class="btn" @click="append(7)">7</div>
        <div class="btn" @click="append(8)">8</div>
        <div class="btn" @click="append(9)">9</div>
        <div class="operator" @click="times">×</div>
        <div class="btn" @click="append(4)">4</div>
        <div class="btn" @click="append(5)">5</div>
        <div class="btn" @click="append(6)">6</div>
        <div class="operator" @click="minus">-</div>
        <div class="btn" @click="append(1)">1</div>
        <div class="btn" @click="append(2)">2</div>
        <div class="btn" @click="append(3)">3</div>
        <div class="operator" @click="add">+</div>
        <div class="zero btn" @click="append(0)">0</div>
        <div class="btn" @click="dot">.</div>
        <div class="operator equal" @click="equal">=</div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            current:'',
            previous:'',
            operatorClicked:false,
            operation: null
        }
    },
    methods:{
        clear(){
            this.current = ''
        },
        sign(){
            this.current = this.current.charAt(0) === '-' ? 
            this.current.slice(1) : `-${this.current}`
        },
        percentage(){
            this.current = `${parseFloat(this.current) / 100}`
        },
        append(num){
            if(this.operatorClicked){
                this.current = ''
            }
            this.current = `${this.current}${num}`
            this.operatorClicked = false
        },
        dot(){
            !this.current.includes('.') ? this.append('.') : '' 
        },
        setPrevious(){
            this.operatorClicked = true
            this.previous = this.current
        },
        divide(){
            this.setPrevious()
            this.operation = (a,b) => a / b
        },
        times(){
            this.setPrevious()
            this.operation = (a,b) => a * b
        },
        add(){
            this.setPrevious()
            this.operation = (a,b) => a + b
        },
        minus(){
            this.setPrevious()
            this.operation = (a,b) => a - b
        },
        equal(){
            this.current =  `${this.operation(parseFloat(this.previous),parseFloat(this.current))}`
        this.operatorClicked = true
        this.operation = null
        }
    }
}
</script>

<style>
.calculator{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows:minmax(50px , 1fr);
    font-size: 30px;
    width: 600px;
    margin: 20px auto;
    line-height: 50px;
}
.calculator .display{
    grid-column: 1/5;
    background-color: #444;
    color: white;
}
.calculator .zero{
    grid-column: 1/3;
}
.calculator .btn{
    background-color: #eee;
}
.calculator .operator{
    background-color: orange;
}
.calculator .btn ,
.calculator .operator{
    cursor: pointer;
    border: 1px solid #555;
}
.calculator .equal{
    background-color: orangered;
    opacity: .8;
}
.calculator .equal:hover{
    opacity: 1;
}
</style>