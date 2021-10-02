<template>
  <div>
    <h1>Update Exercise</h1>
    <div>
      <label class="form-label">Exercise Name</label>
      <input class="form-control" type="text" v-model="exerciseName" />

      <label class="form-label">Muscle Worked</label>
      <input type="text" class="form-control" v-model="muscleWorked" />

      <label class="form-label">Equipment(s) Needed</label>
      <input type="text" class="form-control" v-model="equipment" />

      <label class="form-label" for="instruction">Exercise Instruction</label>
      <div class="form-floating">
        <textarea
          class="form-control"
          v-model="instruction"
          style="height: 250px"
        ></textarea>
      </div>

      <label class="form-label">Media Link</label>
      <input type="text" class="form-control" v-model="media" />
    </div>
    <button class="mt-3 btn btn-dark" v-on:click="goExercise">Cancel</button>
    <button class="mt-3 mx-3 btn btn-warning" v-on:click="processUpdate">
      Update
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
      muscleWorked: "",
      equipment: "",
      instruction: "",
      media: "",
    };
  },
  props: ["exerciseId"],
  mounted: async function () {
    let response = await axios.get(
      API_URL + "/exerciselibrary/update/" + this.exerciseId
    );
    this.exerciseName = response.data.exerciseName;
    this.muscleWorked = response.data.muscleWorked;
    this.equipment = response.data.equipment;
    this.instruction = response.data.instruction;
    this.media = response.data.media;
  },
  methods: {
    processUpdate: async function () {
      let response = await axios.patch(
        API_URL + "/exerciselibrary/update/" + this.exerciseId,
        {
          exerciseName: this.exerciseName,
          muscleWorked: this.muscleWorked,
          equipment: this.equipment,
          instruction: this.instruction,
          media: this.media,
        }
      );
      this.$emit("exercise-updated");
    },
    goExercise: function () {
      this.$emit("exUpdCancelled");
    },
  },
};
</script>