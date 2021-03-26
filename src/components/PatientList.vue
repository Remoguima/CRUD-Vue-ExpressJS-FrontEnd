<template>
  <div>
    <router-link :to="{ name: 'Create' }" class="button is-success mt-5"
      >Add New</router-link
    >
    <table class="table is-striped is-bordered mt-2 is-fullwidth">
      <thead>
        <tr>
          <th>Patient Name</th>
          <th>Age</th>
          <th>Diagnosis</th>
          <th class="has-text-centered">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="patient in patients" :key="patient.id">
          <td>{{ patient.name }}</td>
          <td>{{ patient.age }}</td>
          <td>{{ patient.diagnosis }}</td>
          <td class="has-text-centered">
            <router-link
              :to="{ name: 'Edit', params: { id: patient.id } }"
              class="button is-info is-small"
              >Edit</router-link
            >
            <a
              class="button is-danger is-small"
              @click="deletePatient(patient.id)"
              >Delete</a
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  name: "PatientList",
  data() {
    return {
      patients: [],
    };
  },
 
  created() {
    this.getPatients();
  },
 
  methods: {
    // Get All Patients
    async getPatients() {
      try {
        const response = await axios.get("http://localhost:5000/patients");
        this.patients = response.data;
      } catch (err) {
        console.log(err);
      }
    },
 
    // Delete Patient
    async deletePatient(id) {
      try {
        await axios.delete(`http://localhost:5000/patients/${id}`);
        this.getPatients();
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
 
<style>
</style>