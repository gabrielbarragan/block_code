<template>
<div class="blockcode-aritmetico">
   <h1>+</h1>
</div>
</template>

<script>
export default {
  name: 'SumaBlock',
  props: {
    select_type: String,
  },
  methods: {
        'onMyChange': function () {
            console.log(`New select type: ${this.select_type}`);
        },
  }
}
</script>

