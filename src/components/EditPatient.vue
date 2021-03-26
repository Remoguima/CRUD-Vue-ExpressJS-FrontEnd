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
      <button class="button is-success" @click="updatePatient">UPDATE</button>
    </div>
  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  name: "EditPatient",
  data() {
    return {
      patientName: "",
      patientAge: "",
      patientDiagnosis: "",
    };
  },
  created: function () {
    this.getPatientById();
  },
  methods: {
    // Get Patient By Id
    async getPatientById() {
      try {
        const response = await axios.get(
          `http://localhost:5000/patients/${this.$route.params.id}`
        );
        this.patientName = response.data.patient_name;
        this.patientAge = response.data.patient_age;
        this.patientDiagnosis = response.data.patient_diagnosis;
      } catch (err) {
        console.log(err);
      }
    },
 
    // Update patient
    async updatePatient() {
      try {
        await axios.put(
          `http://localhost:5000/patients/${this.$route.params.id}`,
          {
            patient_name: this.patientName,
            patient_age: this.patientAge,
            patient_diagnosis: this.patientDiagnosis,
          }
        );
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