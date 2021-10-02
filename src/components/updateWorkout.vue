<template>
  <div>
    <h1>Update Workout</h1>
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
    <button class="mt-3 btn btn-dark my-3" v-on:click="goWorkout">
      Cancel
    </button>
    <button class="btn btn-warning mx-2 my-3" v-on:click="processWorkoutUpdate">
      Update Workout
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
  props: ["workoutId"],
  mounted: async function () {
    let response = await axios.get(
      API_URL + "/userSubmitted/workout/" + this.workoutId + "/update"
    );
    this.workoutName = response.data.workoutName;
    this.trainingGoal = response.data.trainingGoal;
    this.equipment = response.data.equipment;
    this.additionalNote = response.data.additionalNote;
    this.author = response.data.author;
  },
  methods: {
    processWorkoutUpdate: async function () {
      let response = await axios.post(
        API_URL + "/userSubmitted/workout/" + this.workoutId + "/update",
        {
          workoutName: this.workoutName,
          trainingGoal: this.trainingGoal,
          equipment: this.equipment,
          additionalNote: this.additionalNote,
          author: this.author,
        }
      );
      this.$emit("workout-updated");
    },
    goWorkout: function () {
      this.$emit("wodUpdCancelled");
    },
  },
};
</script>