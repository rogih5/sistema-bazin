<template>
    <div>
      <value-adder @value-added="addValue"></value-adder>
      <value-viewer :values="values"></value-viewer>
    </div>
  </template>
  
  <script>
  import ValueAdder from '@/components/ValueAdder.vue';
  import ValueViewer from '@/components/ValueViewer.vue';
  
  export default {
    components: {
      ValueAdder,
      ValueViewer,
    },
    data() {
      return {
        values: [],
      };
    },
    methods: {
      addValue(newEntry) {
        this.values.push(newEntry);
      },
    },
  };
  </script>
  