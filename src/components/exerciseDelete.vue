<template>
  <div>
    <div class="alert alert-danger" id="deleteForm">
      <div>
        <h3>Confirm Delete Exercise?</h3>
      </div>
      <input
        type="text"
        class="form-control"
        name="deleteAuthKey"
        v-model="exerciseName"
        placeholder="Enter Authentication Key"
      />
      <button class="btn btn-dark my-3" v-on:click="goExercise">Cancel</button>
      <button class="btn btn-warning mx-3" v-on:click="processDelete">
        Delete
      </button>
    </div>
  </div>
</template>



<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "exerciseDelete",
  data: function () {
    return {
      exerciseName: this.exerciseName,
    };
  },
  props: ["exerciseId"],
  // mounted: async function () {
  //   let response = await axios.get(
  //     API_URL + "/exerciselibrary/find/" + this.exerciseId
  //   );
  //   this.exerciseName = response.data.exerciseName;
  // },

  methods: {
    processDelete: async function () {
      let response = await axios.delete(
        API_URL + "/exerciseRecord/" + this.exerciseId + "/delete"
      );
      this.$emit("exercise-deleted");
    },
    goExercise: function () {
      this.$emit("ex-del-cancelled");
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