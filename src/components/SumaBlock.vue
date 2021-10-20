<template>
<div class="blockcode-aritmetico" >
   <div @focus="clicked" class="py-2">
    <input df-input_val1 id="SumaInput" type="number" class=" w-50 " @change="clicked"  v-model="input_valor">
    
    <h5>+</h5>
    <input df-input_val2 id="SumaInput1" type="number" class=" w-50 " @change="clicked" v-model="input_valor1">
   </div>
   <div class="py-4 d-flex justify-content-end " >
      <input df-output_val id="output" type="number" class=" w-50 " @blur="clicked" v-model="output_val" >
     
  </div>
</div>
</template>

<script>
export default {
  
  name: 'SumaBlock',
  props: {
    output: {
      type: Number,
      default: 0,
    },
    inputs:{
      type: Number,
      default: 0,
    },

  },
  data(){
    return {
      output_val:'',
      data:'',
      input_valor:'',
      input_valor1:'',
      }
  },
  methods: {
        'clicked': function () {
         
          console.log(this.$data['input_valor'])
          console.log(this.$data['input_valor1'])
          console.log(this.$data['output_val'])
          console.log(this.$data)

          document.getElementById('output').value = this.input_valor + this.input_valor1;
          this.output_val= document.getElementById('output').value
          const id = this.$el.parentElement.parentElement.id;
          console.log(id.slice(5))

        },

  }
}
</script>

