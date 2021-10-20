<template>

  <div class="blockcode-value ps-0">
      <input df-input_val type="number" @blur="onChange" class="h-100 w-100" v-model="input_val">
  </div>
 
</template>
<script>

export default {
  name: 'ValueBlock',
  props:{
    inputs: {
      type: Number,
      default:0,
      },
  },
  data(){
    return {input_val:''}
  },
  methods: {
        'onChange': function () {
          this.input= this.input_val
          console.log(this.input_val)
        },
  
  },
  

  mounted() {
    
  },
}
</script>

<style>
:root {

  
  --dfNodeBackgroundColor4: #ffc107;

  
  --dfNodePaddingy1:6%;
  --dfNodePaddingx1:20%;
  

  --dfNodeHoverBackgroundColor4: #c99700;

  --dfNodeSelectedBackgroundColor4: #806000;

}

.drawflow .drawflow-node .blockcode-value{
  display: var(--dfNodeType);
  background: var(--dfNodeBackgroundColor4);
  color: var(--dfNodeTextColor);
  border: var(--dfNodeBorderSize)  solid var(--dfNodeBorderColor);
  border-radius: var(--dfNodeBorderRadius);
  min-height: var(--dfNodeMinHeight1);
  width: auto;
  min-width: var(--dfNodeMinWidth);
  padding-top: var(--dfNodePaddingy1);
  padding-bottom: var(--dfNodePaddingy1);
  -webkit-box-shadow: var(--dfNodeBoxShadowHL) var(--dfNodeBoxShadowVL) var(--dfNodeBoxShadowBR) var(--dfNodeBoxShadowS) var(--dfNodeBoxShadowColor);
  box-shadow:  var(--dfNodeBoxShadowHL) var(--dfNodeBoxShadowVL) var(--dfNodeBoxShadowBR) var(--dfNodeBoxShadowS) var(--dfNodeBoxShadowColor);
  padding-left: var(--dfNodePaddingx1);
  padding-right: var(--dfNodePaddingx1);

}

.drawflow .drawflow-node:hover .blockcode-value{
  background: var(--dfNodeHoverBackgroundColor4);
  color: var(--dfNodeHoverTextColor);
  border: var(--dfNodeHoverBorderSize)  solid var(--dfNodeHoverBorderColor);
  border-radius: var(--dfNodeHoverBorderRadius);
  -webkit-box-shadow: var(--dfNodeHoverBoxShadowHL) var(--dfNodeHoverBoxShadowVL) var(--dfNodeHoverBoxShadowBR) var(--dfNodeHoverBoxShadowS) var(--dfNodeHoverBoxShadowColor);
  box-shadow:  var(--dfNodeHoverBoxShadowHL) var(--dfNodeHoverBoxShadowVL) var(--dfNodeHoverBoxShadowBR) var(--dfNodeHoverBoxShadowS) var(--dfNodeHoverBoxShadowColor);
}

.drawflow .drawflow-node.selected .blockcode-value{
  background: var(--dfNodeSelectedBackgroundColor4);
  color: var(--dfNodeSelectedTextColor);
  border: var(--dfNodeSelectedBorderSize)  solid var(--dfNodeSelectedBorderColor);
  border-radius: var(--dfNodeSelectedBorderRadius);
  -webkit-box-shadow: var(--dfNodeSelectedBoxShadowHL) var(--dfNodeSelectedBoxShadowVL) var(--dfNodeSelectedBoxShadowBR) var(--dfNodeSelectedBoxShadowS) var(--dfNodeSelectedBoxShadowColor);
  box-shadow:  var(--dfNodeSelectedBoxShadowHL) var(--dfNodeSelectedBoxShadowVL) var(--dfNodeSelectedBoxShadowBR) var(--dfNodeSelectedBoxShadowS) var(--dfNodeSelectedBoxShadowColor);
}

.blockcode-value{
  height: 4rem;
}



</style>