<template>
  <div class="value-viewer-container">
    <div v-for="(baseValues, baseName) in baseData" :key="baseName" class="base-section">
      <h2 class="base-title">Base: {{ baseName }}</h2>
      <p class="action-value">Valor da Ação: {{ baseValues[0].actionValue }}</p>
      <table class="value-table">
        <thead>
          <tr>
            <th>Ano</th>
            <th>Valor do Dividendo</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(entry, index) in baseValues" :key="index">
            <td>{{ entry.year }}</td>
            <td>{{ entry.dividendValue }}</td>
          </tr>
        </tbody>
      </table>
      <div class="result-section">
        <p class="result-label">Média dos Dividendos: {{ calculateAverage(baseValues).toFixed(2) }}</p>
        <p class="result-label">Resultado do Valor que a ação esta valendo segundo Bazin: R${{ calculateResultAfter6Percent(baseValues).toFixed(2) }}</p>
        <p class="result-label">Diferença do valor recomendado em relação ao preço da ação: {{ calculateProfit(baseValues).toFixed(2) }}%</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    values: Array,
  },
  computed: {
    baseData() {
      const data = {};
      this.values.forEach(entry => {
        if (!data[entry.base]) {
          data[entry.base] = [];
        }
        data[entry.base].push({
          year: entry.year,
          dividendValue: parseFloat(entry.dividendValue),
          actionValue: parseFloat(entry.actionValue),
        });
      });
      return data;
    },
  },
  methods: {
    calculateAverage(values) {
      if (values.length > 0) {
        const totalDividends = values.reduce((sum, entry) => sum + entry.dividendValue, 0);
        const average = totalDividends / values.length;
        return average;
      }
      return 0;
    },
    calculateResultAfter6Percent(values) {
      const average = this.calculateAverage(values);
      const result = (average / 0.06);
      return result;
    },
    calculateProfit(values) {
      const resultAfter6Percent = this.calculateResultAfter6Percent(values);
      const actionValue = values[0].actionValue;
      const profit = (resultAfter6Percent - actionValue) / actionValue * 100;
      return profit;
    },
  },
};
</script>

<style scoped>
.value-viewer-container {
  margin: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.base-section {
  margin-bottom: 30px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.base-title {
  font-size: 1.5rem;
  margin-bottom: 10px;
  color: #333;
}

.action-value {
  font-size: 1rem;
  margin-bottom: 10px;
  color: #666;
}

.value-table {
  width: 100%;
  border-collapse: collapse;
}

.value-table th,
.value-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

.result-section {
  margin-top: 20px;
  border-top: 1px solid #ddd;
  padding-top: 20px;
  color: #333;
}

.result-label {
  font-size: 1rem;
  margin-bottom: 5px;
}

</style>
