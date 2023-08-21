<template>
    <div>
      <input v-model="newBase" placeholder="Nome da Ação" v-if="!baseSet">
      <button @click="setBase" v-if="!baseSet">Adicionar Nome</button>
  
      <input v-model="newYear" placeholder="Ano" v-if="baseSet">
      <input v-model="newValue" placeholder="Valor do Dividendo" v-if="baseSet">
      <button @click="addValue" v-if="baseSet">Adicionar Valor</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newBase: '',
        newYear: '',
        newValue: '',
        baseSet: false,
        selectedBase: '',
      };
    },
    methods: {
      addValue() {
        if (this.newYear.trim() !== '' && this.newValue.trim() !== '') {
          const newEntry = {
            base: this.selectedBase,
            year: this.newYear,
            dividendValue: this.newValue,
          };
          this.$emit('value-added', newEntry);
          this.newYear = '';
          this.newValue = '';
        }
      },
      setBase() {
        if (this.newBase.trim() !== '') {
          this.baseSet = true;
          this.selectedBase = this.newBase;
        }
      },
    },
  };
  </script>
  