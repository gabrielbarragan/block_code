<template>
<div id="app" class="h-100">

  <div id="header">
    <HeaderBar/>
  </div>

  <div class="row h-100 w-100 ">
    <div class="col-2 bg-dark">
      <h4 class="text-light p-2">Bloques disponibles</h4>
      <div class="flex-column py-3 px-2">
        <button @click="valuenodedf" class="btn btn-warning btn-lg w-100 mb-2" >
          <input type="text" id="value_input" class="w-50 px-2" style="font-size:0.8rem;" placeholder="value here...">
        </button>
        <button @click="asignanodedf" class="btn btn-danger btn-lg w-100 mb-2" >=</button>
        <button @click="addnodedf" class="btn btn-success btn-lg w-100 mb-2" >+</button>
        <button @click="lessnodedf" class="btn btn-success btn-lg w-100 mb-2">-</button>
        <button @click="productnodedf" class="btn btn-success btn-lg w-100 mb-2">*</button>
        <button @click="divisionnodedf" class="btn btn-success btn-lg w-100 mb-2">/</button>
        <button @click="ifnodedf" class="btn btn-primary btn-lg w-100 mb-2">if</button>
        <button @click="fornodedf" class="btn btn-primary btn-lg w-100 mb-2">For</button>
      </div>
    </div>

    <div class="col-10 px-0">
      <div id="drawflow" class="w-100 " @click="extract"></div>
    </div>

  </div>

  <div class="row bg-light w-100 py-2">
    <span> </span>
    <div class="col-12 d-flex justify-content-center  px-0 ">
          <button @click="exportdf" class="btn btn-primary mx-1">Export</button>
          <button @click="importdf" class="btn btn-danger mx-1">Import</button>
          <button @click="cleardf" class="btn btn-dark mx-1">Clear</button>
    </div>
  </div>
</div>
</template>

<script>
/*eslint-disable */
import Drawflow from 'drawflow'
import styleDrawflow from 'drawflow/dist/drawflow.min.css'
import SumaBlock from '@/components/SumaBlock.vue'
import ValueBlock from '@/components/ValueBlock.vue'
import RestaBlock from '@/components/RestaBlock.vue'
import IfBlock from '@/components/IfBlock.vue'
import ForBlock from '@/components/ForBlock.vue'
import ProductBlock from '@/components/ProductBlock.vue'
import AsignaBlock from '@/components/AsignaBlock.vue'
import DivisionBlock from '@/components/DivisionBlock.vue'
import HeaderBar from '@/components/Header/Header.vue'
import * as Vue from 'vue';
import {createApp} from 'vue'



export default {
  name: 'App',
  components: {
    ValueBlock,
    SumaBlock,
    RestaBlock,
    IfBlock,
    ForBlock,
    DivisionBlock,
    AsignaBlock,
    ProductBlock,
    HeaderBar,
  },
  data() {
    return {
      exportValue: null,
      
    }
  },
  mounted() {
    const id = document.getElementById("drawflow");
    
    const props = {
      $df: this.$df,
    };

    const app = createApp({})
    app.config.globalProperties.$df= new Drawflow(id, Vue, this);
    this.$df= app.config.globalProperties.$df
    this.$df.reroute = true;
    this.$df.reroute_fix_curvature = true;


    this.$df.start();
    this.$df.zoom_out();

    const random_int = (min,max) => { return Math.random() * (max - min) + min; }

    const x_pos = 150 
    const y_pos = 300
    
    this.$df.registerNode('SumaBlock', SumaBlock, props, {});
    this.$df.registerNode('ValueBlock', ValueBlock, props, {});
    this.$df.registerNode('RestaBlock', RestaBlock,props, {});
    this.$df.registerNode('ProductBlock', ProductBlock,props, {});
    this.$df.registerNode('DivisionBlock', DivisionBlock,props, {});
    this.$df.registerNode('IfBlock', IfBlock,props, {});
    this.$df.registerNode('ForBlock', ForBlock,props, {});
    this.$df.registerNode('AsignaBlock', AsignaBlock,props, {});



    this.$df.addNode('SumaBlock', 2, 1, random_int(150,180), random_int(300,350), 'SumaBlock',{}, 'SumaBlock', 'vue');

    this.$df.addNode('RestaBlock', 2, 1, random_int(150,180), random_int(300,350), 'RestaBlock',{}, 'RestaBlock', 'vue');
    this.$df.on('nodeCreated', function(id) {
      
      console.log('El id es:',id)

    })  


  },
  methods: {
    exportdf() {  
      
      this.input_val1 = parseInt(document.getElementById('SumaInput').value)
      this.input_val2 = parseInt(document.getElementById('SumaInput1').value)
      this.output_val= parseInt(document.getElementById('output').value)

      this.$df.updateNodeDataFromId(1,{output_val:this.output_val,input_val:this.input_val1, input_val2:this.input_val2})
      this.exportValue = this.$df.export();

      console.log(this.exportValue)
      console.log('los datos del df son:',this.$df)
    },

    importdf() {
      this.$df.import(this.exportValue);
    },
    valuenodedf() {
      this.$df.addNode('ValueBlock', 0, 1, 150, 300, 'ValueBlock', {}, 'ValueBlock', 'vue');
    },
    addnodedf() {
      this.$df.addNode('SumaBlock', 2, 1, 150, 300, 'SumaBlock', {}, 'SumaBlock', 'vue');
    },
    lessnodedf() {
      this.$df.addNode('RestaBlock', 2, 1, 150, 300, 'RestaBlock', {}, 'RestaBlock', 'vue');
    },
    ifnodedf() {
      this.$df.addNode('IfBlock', 2, 0, 150, 300, 'IfBlock', 'if', {}, 'vue');
    },
    asignanodedf() {
      this.$df.addNode('AsignaBlock', 1, 1, 150, 300, 'AsignaBlock',{}, 'AsignaBlock', 'vue');
    },
    fornodedf() {
      this.$df.addNode('ForBlock', 2, 1, 150, 300, 'ForBlock', 'for', {}, 'vue')
    },
    productnodedf() {
      this.$df.addNode('ProductBlock', 2, 1, 150, 300, 'ProductBlock', {}, 'ProductBlock', 'vue')
    },
    divisionnodedf() {
      this.$df.addNode('DivisionBlock', 2, 1, 150, 300, 'DivisionBlock', {}, 'DivisionBlock', 'vue')
    },
    cleardf() {
      this.$df.clear()
    },
    extract(){
      const nodos_suma_list = this.$df.getNodesFromName('SumaBlock')
      console.log(nodos_suma_list)
      for (const nodo_id_suma of nodos_suma_list) {
        console.log(nodo_id_suma)
        this.nodoSuma = this.$df.getNodeFromId(nodo_id_suma).inputs
        
        for(const input in this.nodoSuma){
         for(const connection in this.nodoSuma[input]){

            this.nodoSuma[input][connection].forEach(element => {
              
              const nombreNodo= `node-${element['node']}`
              console.log(nombreNodo)
              console.log(document.getElementById(nombreNodo).querySelectorAll('input'))
              
            });            

          }
        
        }  
      
      }
    },

    
  }

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}


#drawflow {
  text-align: initial;
  height: 92vh;
  position: relative;
  background-color: dimgray;
  background: var(--background-color);
  background-size: 25px 25px;
  background-image: linear-gradient(to right, #f1f1f1 1px, transparent 1px),
    linear-gradient(to bottom, #f1f1f1 1px, transparent 1px);

}

.drawflow .drawflow-node {
  background-color:transparent;
  border:1px solid #839bb2;
  padding-top: 0;
  padding-bottom: 0;
  padding: 0;
}

</style>