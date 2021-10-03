<template>
  <div>
    <div class="container-fluid">
      <h1 class="mx-1">Exercise Library</h1>
      <input
        class="mx-2 my-1"
        id="searchbar"
        type="text"
        placeholder="Search for a targeted muscle"
        v-model="searchTerms"
      /><br />
      <button class="btn btn-warning btn-sm mx-2 my-2" v-on:click="addExercise">
        Add New Exercise
      </button>
      <div class="row">
        <div
          class="col-lg-4 col-md-6 col-12"
          v-for="e in filteredExercises"
          v-bind:key="e._id"
        >
          <div class="card bg-light border-light shadow-lg">
            <img :src="e.media" class="card-img-top" alt="media image" />
            <div class="card-header text-white bg-dark">
              <h3>{{ e.exerciseName }}</h3>
            </div>
            <div class="card-body">
              <h6 class="card-text my-0">Muscles worked</h6>
              <p class="card-text">{{ e.muscleWorked }}</p>

              <h6 class="card-text my-0">Equipment Needed</h6>
              <p class="card-text">{{ e.equipment }}</p>

              <h6 class="card-text my-0">Instruction</h6>
              <p class="card-text">{{ e.instruction }}</p>
              <a
                v-bind:href="e.media"
                class="btn btn-warning btn-sm mx-1"
                target="_blank"
                >Media link</a
              >
              <div class="my-3">
                <button
                  class="btn btn-dark btn-sm mx-1"
                  v-on:click="update(e._id)"
                >
                  Update
                </button>
                <button
                  class="btn border-dark btn-sm"
                  v-on:click="delEx(e._id)"
                >
                  Delete
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const API_URL = "https://dwjf-glib.herokuapp.com";
export default {
  name: "exerciseLibrary",
  data: function () {
    return {
      exercises: [],
      searchTerms: "",
    };
  },
  mounted: async function () {
    let response = await axios.get(API_URL + "/exerciselibrary");
    this.exercises = response.data;
  },
  methods: {
    addExercise: function () {
      this.$emit("exercise-add");
    },
    update: function (exerciseId) {
      this.$emit("update-exercise", exerciseId);
    },
    delEx: function (exerciseId) {
      this.$emit("delete-exercise", exerciseId);
    },
  },
  created: async function () {
    let response = await axios.get(API_URL + "/exerciselibrary");
    this.exercises = response.data;
  },
  computed: {
    filteredExercises: function () {
      let filteredExercises = [];
      for (let eachExercise of this.exercises) {
        if (
          eachExercise.muscleWorked.toLowerCase().includes(this.searchTerms)
        ) {
          filteredExercises.push(eachExercise);
        }
      }
      return filteredExercises;
    },
  },
};
</script>

<style scoped>
#searchbar {
  width: 300px;
  border-radius: 5px;
  border-width: 1px;
}
.btn {
  margin: 1px;
  padding: 2px;
  cursor: pointer;
}
.card {
  width: 18rem;
  height: 25rem;
  overflow-x: hidden;
  overflow-y: scroll;
  border-radius: 10px;
  margin-bottom: 1em;
  margin-top: 1em;
}
::-webkit-scrollbar {
  width: 20px;
}
::-webkit-scrollbar-thumb {
  height: 5px;
  background: linear-gradient(transparent, rgb(241, 185, 0.4));
  border-radius: 8px;
}
::-webkit-scrollbar-track {
  border-radius: 30rem;
  background: transparent;
  margin-block: 0.5rem;
}
</style>