<template>
  <div>
    <div class="alert alert-danger" id="deleteForm">
      <div>
        <h3>Confirm Delete Exercise from Workout?</h3>
      </div>

      <button class="btn btn-dark my-3" v-on:click="goExercise">Cancel</button>
      <button class="btn btn-warning mx-3" v-on:click="processWodExDel">
        Delete
      </button>
    </div>
  </div>
</template>



<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "deleteWorkoutExercise",
  props: ["wodexId"],

  methods: {
    processWodExDel: async function () {
      let response = await axios.post(
        API_URL + "/userSubmitted/workout/exercise/" + this.wodexId + "/delete"
      );
      this.$emit("wod-exercise-deleted");
    },
    goExercise: function () {
      this.$emit("workout-ex-del-cancelled");
    },
  },
};
</script>

<style scoped>
#deleteForm {
  position: absolute;
  left: 22%;
  width: 60%;
  border-radius: 10px;
  background-color: rgba(255, 174, 174, 0.4);
}
</style>