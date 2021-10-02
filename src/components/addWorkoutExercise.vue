<template>
  <div>
    <h1>Add an Exercise to the Workout</h1>
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
    <button class="btn btn-dark my-3" v-on:click="goExercise">Cancel</button>
    <button class="btn btn-warning my-3" v-on:click="processAdd">
      Add Exercise
    </button>
  </div>
</template>

<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "addWorkoutExercise",
  data: function () {
    return {
      exerciseName: "",
      Sets: "",
      Repetitions: "",
      Intensity: "",
      workoutName: "",
    };
  },
  props: ["workoutId"],
  mounted: async function () {
    let response = await axios.get(
      API_URL + "/userSubmitted/workout/" + this.workoutId + "/exercise/add"
    );
  },
  methods: {
    processAdd: async function () {
      await axios.post(
        API_URL + "/userSubmitted/workout/" + this.workoutId + "/exercise/add",
        {
          exerciseName: this.exerciseName,
          Sets: this.Sets,
          Repetitions: this.Repetitions,
          Intensity: this.Intensity,
        }
      );
      this.$emit("wod-exercise-added");
    },
    goExercise: function () {
      this.$emit("add-wod-ex-cancelled");
    },
  },
};
</script>