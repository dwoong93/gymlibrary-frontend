<template>
  <div>
    <h1>Add a Workout</h1>
    <div>
      <label class="form-label">Workout Name</label>
      <input type="text" class="form-control" v-model="workoutName" />
      <label class="form-label">Training Goal</label>
      <input type="text" class="form-control" v-model="trainingGoal" />
      <label class="form-label">Equipment Needed</label>
      <input type="text" class="form-control" v-model="equipment" />
      <label class="form-label" for="instruction">Notes</label>
      <div class="form-floating">
        <textarea
          class="form-control"
          placeholder="Exercise Instruction"
          id="instruction"
          v-model="additionalNote"
          style="height: 250px"
        ></textarea>
      </div>
      <label class="form-label">Author</label>
      <input type="text" class="form-control" v-model="author" />
    </div>
    <button class="btn btn-dark my-3" v-on:click="goExercise">Cancel</button>
    <button class="btn btn-warning mx-3 my-3" v-on:click="processAddWorkout">
      Add Workout
    </button>
  </div>
</template>

<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "addWorkoutPage",
  data: function () {
    return {
      workoutName: "",
      trainingGoal: "",
      equipment: "",
      additionalNote: "",
      author: "",
    };
  },
  methods: {
    processAddWorkout: async function () {
      await axios.post(API_URL + "/userAdd/workout", {
        workoutName: this.workoutName,
        trainingGoal: this.trainingGoal,
        equipment: this.equipment,
        additionalNote: this.additionalNote,
        author: this.author,
      });
      this.$emit("new-workout-added");
    },
    goExercise: function () {
      this.$emit("add-wod-cancelled");
    },
  },
};
</script>