<template>
     <div>
    <h1>Dashboard</h1>
    <v-data-table
      :headers="headers"
      :items="employees"
      :items-per-page="5"
      class="elevation-1"
       @click:row="selectRow"
    ></v-data-table>
     <v-snackbar
      v-model="snackbar"
    >
        You have selected {{ selectedEmployee.name }} - {{selectedEmployee.title}}
      <v-btn
        color="pink"
        text
        @click="snackbar = false"
      >
        Close
      </v-btn>
    </v-snackbar>
  </div>
</template>

<script>
import Employees from "../data/employees.json";
export default {
  name: "DashboardPage",
  data() {
    return {
      selectedEmployee: {
        name: null,
        title: null,
      },
      snackbar: false,
      headers: [
        {
          text: "Id",
          align: "left",
          sortable: false,
          value: "id",
        },
        { text: "Name", value: "name" },
        { text: "Title", value: "title" },
        { text: "Salary", value: "salary" },
      ],
      employees: Employees,
    };
  },
  methods: {
    selectRow(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.title;
    },
  },
};
</script>

<style scoped>
</style>