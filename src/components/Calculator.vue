<template>
  <div id="calc-container">
    <Display v-bind:displayValue=dispValue v-bind:subDisplayValue=subDispValue></Display>
    <Button v-for="b in buttons"
            v-bind:key="b.id"
            v-bind:buttonValues="b"
            v-bind:style="b.id === 1 ? bStyleObjectLarge:  bStyleObjectRegular"
            v-on:handle-press="handlePress" >
    </Button>
  </div>
</template>

<script>
import Display from "@/components/Display";
import Button from "@/components/Button";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'calculator',
  data: function () {
    return {
      dispValue: "0",
      subDispValue: "",
      bStyleObjectRegular:{
        width: '25%'
      },
      bStyleObjectLarge:{
        width: '50%',
      },

      prevValue: "0",
      prevOp: "=",

      buttons: [
        {
          id: 1,
          name: "AC",
          isNum: true,
          isSym: false
        },
        {
          id: 2,
          name: "C",
          isNum: true,
          isSym: false
        },
        {
          id: 3,
          name: "/",
          isNum: false,
          isSym: true
        },
        {
          id: 4,
          name: "7",
          isNum: true,
          isSym: false
        },
        {
          id: 5,
          name: "8",
          isNum: true,
          isSym: false
        },
        {
          id: 6,
          name: "9",
          isNum: true,
          isSym: false
        },
        {
          id: 7,
          name: "x",
          isNum: false,
          isSym: true
        },
        {
          id: 8,
          name: "4",
          isNum: true,
          isSym: false
        },
        {
          id: 9,
          name: "5",
          isNum: true,
          isSym: false
        },
        {
          id: 10,
          name: "6",
          isNum: true,
          isSym: false
        },
        {
          id: 11,
          name: "+",
          isNum: false,
          isSym: true
        },
        {
          id: 12,
          name: "1",
          isNum: true,
          isSym: false
        },
        {
          id: 13,
          name: "2",
          isNum: true,
          isSym: false
        },
        {
          id: 14,
          name: "3",
          isNum: true,
          isSym: false
        },
        {
          id: 15,
          name: "-",
          isNum: false,
          isSym: true
        },
        {
          id: 16,
          name: "0",
          isNum: true,
          isSym: false
        },
        {
          id: 17,
          name: ".",
          isNum: true,
          isSym: false
        },
        {
          id: 18,
          name: "\u00b1",
          isNum: true,
          isSym: false
        },
        {
          id: 19,
          name: "=",
          isNum: false,
          isSym: true
        }
      ]
    }
  },
  components: {
    Display,
    Button
},
methods: {
  handlePress: function (event){
    var number = event.textContent.trim();
    switch (number){
      case "AC": this.clearAll();
        break;
      case "C": this.clearDisplay();
        break;
      case "0":
      case "1":
      case "2":
      case "3":
      case "4":
      case "5":
      case "6":
      case "7":
      case "8":
      case "9": this.numberPressed(number);
        break;
      case "+": this.computeOp("+");
        break;
      case "-": this.computeOp("-");
        break;
      case "/": this.computeOp("/");
        break;
      case "x": this.computeOp("x");
        break;
      case "=": this.equalPressed();
        break;
      case ".": this.addPoint();
        break;
      case "\u00b1": this.negateValue();
        break;
      default:
        alert("KEY ERROR: in default");
    }
  },
  numberPressed: function(number) {
    if (this.dispValue === "0") {
      this.dispValue = number;
    }
    else {
      if (this.dispValue.length >= 15) {
        alert("KEY ERROR: Display limit reached");
      } else {
        this.dispValue += number;

      }
    }
  },
  computeOp: function (op) {
    this.computeEqual(this.prevValue, this.dispValue, this.prevOp)
    this.prevValue = this.dispValue;
    this.dispValue = "0";
    this.prevOp=op;
    this.subDispValue = this.prevValue.toString() + " " + this.prevOp + "    ";
  },
  computeEqual: function(op1, op2, op){
    let op1_num = parseFloat(op1);
    let op2_num = parseFloat(op2);
    let result = 0;
    if (op === "+"){
      result = op1_num + op2_num;
    }
    else if (op === "-"){
      result = op1_num - op2_num;
    }
    else if (op === "x"){
      result = op1_num * op2_num;
    }
    else if (op === "/"){
      if (op2_num == 0){
        throw "MATH ERROR: Cannot divide by 0";
      }
      else{
        result = op1_num / op2_num;
      }

    }
    else{
      result = op2_num;
    }
    let temp = result.toString();
    if (temp.length >= 15){
      throw "DISPLAY ERROR: Computation result will not fit on display. Use C or AC to perform a simpler computation.";
    }
    this.dispValue = temp;
    this.prevValue = "0";
    this.prevOp = "=";
  },
  equalPressed: function(){
    try{
      this.computeEqual(this.prevValue, this.dispValue, this.prevOp);
      this.subDispValue = "";
    }
    catch (e){
      alert(e);
    }
  },
  clearDisplay: function (){
    this.dispValue = "0";
  },
  clearAll: function (){
    this.clearDisplay();
    this.prevValue = "0";
    this.prevOp = "=";
    this.subDispValue ="";
  },
  negateValue: function(){
    if (this.dispValue != "0"){
      if (this.dispValue.indexOf("-") < 0){
        this.dispValue = "-" + this.dispValue;
      }
      else{
        this.dispValue = this.dispValue.substring(1);
      }
    }

  },
  addPoint: function() {
    if (this.dispValue.indexOf(".") < 0){
      this.dispValue += "."
    }
  },
}
}
</script>

<style>
#calc-container {
  width: 100%;
  margin: auto;
  box-sizing: border-box;
  border: 15px solid black;
  border-radius: 5px;
  height: 700px;
  overflow: hidden;
  box-shadow: 5px 5px 5px #4b4b4c;
}

@media screen and (min-width: 768px){
  #calc-container {
    width: 40%;
    margin: auto;
  }
}
</style>