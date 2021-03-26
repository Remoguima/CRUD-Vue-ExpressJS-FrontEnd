<template>
  <div>
    <div class="field">
      <label class="label">Patient Name</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="Patient Name"
          v-model="patientName"
        />
      </div>
    </div>
 
    <div class="field">
      <label class="label">Age</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="Age"
          v-model="patientAge"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">Diagnosis</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="Diagnosis"
          v-model="patientDiagnosis"
        />
      </div>
    </div>
 
    <div class="control">
      <button class="button is-success" @click="savePatient">SAVE</button>
    </div>
  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  name: "AddPatient",
  data() {
    return {
      patientName: "",
      patientAge: "",
      patientDiagnosis: "",
    };
  },
  methods: {
    // Create New patient
    async savePatient() {
      try {
        await axios.post("http://localhost:5000/patients", {
          name: this.patientName,
          age: this.patientAge,
          diagnosis: this.patientDiagnosis,
        });
        this.patientName = "";
        this.patientAge = "";
        this.patientDiagnosis = "";
        this.$router.push("/");
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
 
<style>
</style>