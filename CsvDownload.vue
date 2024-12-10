<template>
  <div>
    <h1>Asset List</h1>
    <table border="1">
      <thead>
        <tr>
          <th>Asset Name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in data" :key="index">
          <td>{{ item.asset_name }}</td>
          <td>{{ item.department }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Button to download the data -->
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>
import Papa from "papaparse";

export default {
  name: "CsvDownload",
  data() {
    return {
      data: [
        { asset_name: "Printer", department: "HR" },
        { asset_name: "Monitor", department: "IT" },
        { asset_name: "Barcode Scanner", department: "ACCOUNT" }
      ]
    };
  },
  methods: {
    downloadCSV() {
      const csv = Papa.unparse(this.data);

      const link = document.createElement("a");
      link.href = URL.createObjectURL(new Blob([csv], { type: "text/csv" }));
      link.download = "assets.csv";
      link.click();
    }
  }
};
</script>

<style scoped>
button {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #45a049;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  text-align: left;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}
</style>