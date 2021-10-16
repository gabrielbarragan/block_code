<template>
<div id="app" class="h-100">

  <div id="header">

  </div>

  <div class="row h-100 w-100 ">
    <div class="col-2 bg-dark">
      <h4 class="text-light p-2">Bloques disponibles</h4>
      <div class="flex-column py-3 px-2">
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
      <div id="drawflow" class="w-100 "></div>
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
import RestaBlock from '@/components/RestaBlock.vue'
import IfBlock from '@/components/IfBlock.vue'
import ForBlock from '@/components/ForBlock.vue'
import ProductBlock from '@/components/ProductBlock.vue'
import AsignaBlock from '@/components/AsignaBlock.vue'
import DivisionBlock from '@/components/DivisionBlock.vue'
import * as Vue from 'vue';



export default {
  name: 'App',
  components: {
    SumaBlock,
    RestaBlock,
    IfBlock,
    ForBlock,
    DivisionBlock,
    AsignaBlock,
    ProductBlock,
  },
  data() {
    return {
      exportValue: null,
    }
  },
  mounted() {
    const id = document.getElementById("drawflow");
    this.$df = new Drawflow(id, Vue);
    this.$df.reroute = true;
    this.$df.reroute_fix_curvature = true;

    this.$df.start();
    this.$df.zoom_out();


    
    this.$df.registerNode('SumaBlock', SumaBlock, {}, {});
    this.$df.registerNode('RestaBlock', RestaBlock,{}, {});
    this.$df.registerNode('ProductBlock', ProductBlock,{}, {});
    this.$df.registerNode('DivisionBlock', DivisionBlock,{}, {});
    this.$df.registerNode('IfBlock', IfBlock,{}, {});
    this.$df.registerNode('ForBlock', ForBlock,{}, {});
    this.$df.registerNode('AsignaBlock', AsignaBlock,{}, {});



    this.$df.addNode('SumaBlock', 1, 2, 150, 300, 'SumaBlock', {}, 'SumaBlock', 'vue');

    this.$df.addNode('RestaBlock', 1, 2, 150, 300, 'RestaBlock', {}, 'RestaBlock', 'vue');

  },
  methods: {
    exportdf() {
      this.exportValue = this.$df.export();
      console.log(this.exportValue);
    },
    importdf() {
      this.$df.import(this.exportValue);
    },
    addnodedf() {
      this.$df.addNode('SumaBlock', 2, 1, 150, 300, 'SumaBlock', {}, 'SumaBlock', 'vue');
    },
    lessnodedf() {
      this.$df.addNode('RestaBlock', 2, 1, 150, 300, 'RestaBlock', {}, 'RestaBlock', 'vue');
    },
    ifnodedf() {
      this.$df.addNode('IfBlock', 2, 0, 150, 300, 'IfBlock', {}, 'IfBlock', 'vue');
    },
    asignanodedf() {
      this.$df.addNode('AsignaBlock', 1, 1, 150, 300, 'AsignaBlock', {}, 'AsignaBlock', 'vue');
    },
    fornodedf() {
      this.$df.addNode('ForBlock', 2, 1, 150, 300, 'ForBlock', {}, 'ForBlock', 'vue')
    },
    productnodedf() {
      this.$df.addNode('ProductBlock', 2, 1, 150, 300, 'ProductBlock', {}, 'ProductBlock', 'vue')
    },
    divisionnodedf() {
      this.$df.addNode('DivisionBlock', 2, 1, 150, 300, 'DivisionBlock', {}, 'DivisionBlock', 'vue')
    },
    cleardf() {
      this.$df.clear()
    }
    




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