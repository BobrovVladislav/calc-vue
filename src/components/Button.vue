<template>
  <div id="vue-button">
    <button class="calc-button"
            v-on:click=buttonPressed
            v-bind:class="{numberButton: buttonValues.isNum, symbolButton: buttonValues.isSym}">
            {{buttonValues.name}}
    </button>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'vuebutton',
  props: {
    buttonValues: Object
},
  methods:{
    buttonPressed: function (event){
this.$emit ('handle-press', event.target)
    }
  }
}
</script>

<style>
#vue-button {
  margin: 0px;
  height: 100px;
  box-sizing: border-box;
  float: left;

}
.calc-button{
  width: 100%;
  height: 100%;
  font-family: Lato, Verdana, sans-serif;
  text-align: center;
  font-size: 30px;
  color: white;
}

.numberButton{
  background-color: #676767;
}
.symbolButton{
  background-color: orange;
}
</style>