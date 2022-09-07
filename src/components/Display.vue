<template>
  <div id="display">
    <div id="display-text">
      <div id="left">{{displayValue}}</div>
    </div>
    <div id="sub-text"><p>{{subDisplayValue}}</p></div>
  </div>
</template>

<script>

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'display',
  props: {
    displayValue: String,
    subDisplayValue: String
  }
}

</script>

<style>
@font-face {
  font-family: 'Lato';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
}

#display {
  width: 100%;
  border-radius: 5px;
  height: 200px;
  float: right;
}

#left{
  width: 99.75%;
}

#display-text,  #sub-text{
  font-family: 'Lato', sans-serif;
  text-align: right;
  margin-bottom: 0px;
  overflow:hidden;
  text-overflow: ellipsis;
}
#display-text{
  display: flex;
  flex-direction: row;
  height: 100px;
  font-size: 3em;
}

#sub-text {
  height: 100px;
  font-size: 1.5em;
  color: #38908f;
  border: none;
  background-color: #f9f9f9;
}
</style>
