<template>
  <div>
    <div class="alert alert-danger" id="deleteForm">
      <div>
        <h3>Confirm Delete Workout?</h3>
      </div>
      <input
        type="text"
        class="form-control"
        name="deleteAuthKey"
        placeholder="Enter Authentication Key"
      />
      <button class="btn btn-dark my-3" @click="cancelDel">Cancel</button>
      <button class="btn btn-warning mx-3" @click="processDelete">
        Delete
      </button>
    </div>
  </div>
</template>



<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "deleteWorkout",
  data: function () {
    return {};
  },
  props: ["workoutId"],
  methods: {
    processDelete: async function () {
      alert(this.workoutId);
      let response = await axios.delete(
        API_URL + "/userSubmitted/workout/" + this.workoutId + "/delete"
      );
      this.$emit("workout-deleted");
    },
    cancelDel: function () {
      alert("cancel test message");
      this.$emit("cancel-workout-del");
      alert("test");
    },
  },
};
</script>