<template>
  <div class="value-input-container">
    <div v-if="!baseSet">
      <input class="input-field" v-model="actionName" placeholder="Nome da Ação">
      <input class="input-field" v-model.number="actionValue" placeholder="Valor da Ação">
      <button class="action-button" @click="setBase">Adicionar Nome e Valor</button>
    </div>
    <div v-if="baseSet">
      <input class="input-field" type="number" v-model="newYear" placeholder="Ano" min="2000" max="2099">
      <input class="input-field" type="number" v-model.number="newValue" placeholder="Valor do Dividendo">
      <button class="action-button" @click="addValue">Adicionar Valor</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      actionName: '',
      actionValue: '',
      newYear: '',
      newValue: '',
      baseSet: false,
      selectedBase: '',
    };
  },
  methods: {
    addValue() {
      if (this.newYear && this.newValue !== '') {
        const newEntry = {
          base: this.actionName,
          actionValue: this.actionValue,
          year: this.newYear,
          dividendValue: this.newValue,
        };
        this.$emit('value-added', newEntry);
        this.newYear = '';
        this.newValue = '';
      }
    },
    setBase() {
      if (this.actionName.trim() !== '' && this.actionValue !== '') {
        this.baseSet = true;
      }
    },
  },
};
</script>

<style scoped>
.value-input-container {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.input-field {
  margin: 10px 0;
  padding: 10px;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 3px;
}

.action-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
</style>
