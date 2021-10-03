<template>
  <div>
    <h1>Update Workout Exercise</h1>
    <div>
      <label class="form-label">Exercise Name</label>
      <input type="text" class="form-control" v-model="exerciseName" />
      <label class="form-label">Sets</label>
      <input type="text" class="form-control" v-model="Sets" />
      <label class="form-label">Repetitions/Time</label>
      <input type="text" class="form-control" v-model="Repetitions" />
      <label class="form-label">Target Intensity (Scale of 10) </label>
      <input type="text" class="form-control" v-model="Intensity" />
    </div>
    <button class="btn btn-dark my-3" v-on:click="goWorkout">Cancel</button>
    <button class="btn btn-warning mx-2 my-3" v-on:click="processUpdate">
      Update Exercise
    </button>
  </div>
</template>

<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "updateExercise",
  data: function () {
    return {
      exerciseName: "",
      Sets: "",
      Repetitions: "",
      Intensity: "",
    };
  },
  props: ["wodexId"],
  mounted: async function () {
    let response = await axios.get(
      API_URL + "/userSubmitted/workout/exercise/" + this.wodexId + "/update"
    );
    this.exerciseName = response.data.exerciseName;
    this.Sets = response.data.Sets;
    this.Repetitions = response.data.Repetitions;
    this.Intensity = response.data.Intensity;
  },
  methods: {
    processUpdate: async function () {
      let response = await axios.patch(
        API_URL + "/userSubmitted/workout/exercise/" + this.wodexId + "/update",
        {
          exerciseName: this.exerciseName,
          Sets: this.Sets,
          Repetitions: this.Repetitions,
          Intensity: this.Intensity,
        }
      );
      this.$emit("wod-exercise-updated");
    },
    goWorkout: function () {
      this.$emit("wod-ex-up-cancelled");
    },
  },
};
</script>
