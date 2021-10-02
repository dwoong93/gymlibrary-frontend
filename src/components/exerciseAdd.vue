<template>
  <div>
    <h1>Add an Exercise</h1>
    <div>
      <label class="form-label">Exercise Name</label>
      <input
        type="text"
        class="form-control minlength=6"
        placeholder="Decline Bench Press"
        v-model="exerciseName"
        required
      />
      <p class="warningText">Ex Name:{{ exerciseName }}</p>
      <label class="form-label">Muscle Worked</label>
      <input
        type="text"
        class="form-control"
        placeholder="Pectoralis Major, Pectoralis Minor, Triceps"
        v-model="muscleWorked"
        required
      />
      <label class="form-label">Equipment(s) Needed</label>
      <input
        type="text"
        class="form-control"
        placeholder="Bench, Barbell, Weight plate, Rack"
        v-model="equipment"
        required
      />
      <label class="form-label" for="instruction">Exercise Instruction</label>
      <div class="form-floating">
        <textarea
          class="form-control"
          placeholder="Bench Press"
          id="instruction"
          v-model="instruction"
          style="height: 80px"
          required
        ></textarea>
      </div>
      <label class="form-label">Media Link</label>
      <input
        type="text"
        placeholder="Paste video or image URL here"
        class="form-control"
        v-model="media"
      />
    </div>
    <button class="btn btn-dark my-3" v-on:click="goExercise">Cancel</button>
    <button class="btn btn-warning mx-3 my-3" v-on:click="processAddExercise">
      Add Exercise
    </button>
  </div>
</template>

<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "exerciseAdd",
  data: function () {
    return {
      exerciseName: "",
      muscleWorked: "",
      equipment: "",
      instruction: "",
      media: "",
    };
  },
  methods: {
    processAddExercise: async function () {
      await axios.post(API_URL + "/exercise_record/add-record", {
        exerciseName: this.exerciseName,
        muscleWorked: this.muscleWorked,
        equipment: this.equipment,
        instruction: this.instruction,
        media: this.media,
      });
      this.$emit("new-exercise-added");
    },
    goExercise: function () {
      this.$emit("add-ex-cancelled");
    },
  },
};
</script>

<style scoped>
.warningText {
  color: rgb(255, 94, 94);
}
</style>