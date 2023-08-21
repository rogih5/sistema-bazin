<template>
  <div>
    <div v-for="(baseValues, baseName) in baseData" :key="baseName">
      <p>Base: {{ baseName }}</p>
      <table>
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
      <div>
        Média dos Dividendos: {{ calculateAverage(baseValues).toFixed(2) }}
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
      this.values.forEach((entry) => {
        if (!data[entry.base]) {
          data[entry.base] = [];
        }
        data[entry.base].push({
          year: entry.year,
          dividendValue: parseFloat(entry.dividendValue),
        });
      });
      return data;
    },
  },
  methods: {
    calculateAverage(values) {
      if (values.length > 0) {
        const totalDividends = values.reduce(
          (sum, entry) => sum + entry.dividendValue,
          0
        );
        const average = totalDividends / values.length;
        return average;
      }
      return 0;
    },
  },
};
</script>
<style>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

th,
td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
