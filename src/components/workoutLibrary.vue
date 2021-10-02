<template>
  <div>
    <div class="container-fluid justify-content-start">
      <h1 class="mx-1">Workouts Library</h1>
      <input
        class="my-1"
        id="searchbar"
        type="text"
        placeholder="Search for a programme (e.g leg day, strength, flexibility)"
        v-model="searchResult"/><br />
      <button class="btn btn-warning mb-4 btn-sm my-2" @click="addWorkout">
        Add New Workout
      </button>
      <div class="row justify-content-center">
        <div class="col-lg-6 col-md-12 col-12" v-for="w in filteredResult" v-bind:key="w._id">
          <div class="card bg-light border-secondary" >
            <div class="card-header text-white bg-dark">
              <h3>{{w.workoutName}}</h3>
            </div>
            <div class="card-body">
              <h6 class="card-text my-0">Training Goal</h6>
              <p class="card-text">{{w.trainingGoal}}</p>
              <h6 class="card-text my-0">Equipment Needed</h6>
              <p class="card-text">{{w.equipment}}</p>

              <h6 class="card-text my-0">Notes</h6>
              <p class="card-text">additionalNote</p>
                <table class="table ">
                  <thead class="table table-dark mx-0">
                    <tr>
                      <th class="text-left align-middle">Exercise</th>
                      <th class="text-center align-middle">Sets</th>
                      <th class="text-center align-middle">Repetition/Time</th>
                      <th class="text-center align-middle">Target Intensity<br>(Scale of 10)</th>
                      <th class="text-center align-middle"></th>
                    </tr>
                  </thead>
                  <tbody class="table" v-for="(a,index) in w.exercise">
                      <td class="text-left">{{a.exerciseName}}</td>
                      <td class="text-center">{{a.Sets}}</td>
                      <td class="text-center">{{a.Repetitions}}</td>
                      <td class="text-center">{{a.Intensity}}</td>
                      <button class="btn btn-warning btn-sm my-1" @click="updateWodEx(a._id)">Update</button>
                      <button class="btn btn-dark btn-sm my-1" @click="delExWod(a._id)">Delete</button>
                        
                    </tr>
                  </tbody>
                </table>
                <button class="btn btn-warning btn-sm" v-on:click="addExWod(w._id)" >Add Exercise</button>
              <div class="my-3">
                <button class="btn btn-dark btn-sm" @click="updateWOD(w._id)">
                  Update
                </button>
                <button class="btn border-dark btn-sm mx-1" @click="deleteWOD(w._id)">Delete</button>
                <h6 class="card-text my-0">Uploaded By: {{w.author}}</h6>
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
  name: "workoutLibrary",
  data: function () {
    return {
      workouts: [],
      searchResult: "",
    };
  },
  mounted: async function () {
    let response = await axios.get(API_URL + "/userSubmitted/workout");
    this.workouts = response.data;
  },
  methods: {
    addExWod: function (workoutId) {
      this.$emit("addEx-Workout", workoutId);
    },
    addWorkout: function () {
      this.$emit("workout-add");
    },
    delExWod: function (wodexId) {
      this.$emit("del-wod-ex", wodexId);
    },
    updateWodEx: function (wodexId) {
      this.$emit("update-wod-ex", wodexId);
    },
    updateWOD: function (workoutId) {
      this.$emit("updateWod", workoutId);
    },
    deleteWOD: function (workoutId) {
      alert("emitting", workoutId);
      this.$emit("delete-wod", workoutId);
    },
  },
  created: async function () {
    let response = await axios.get(API_URL + "/userSubmitted/workout");
    this.workouts = response.data;
  },
  computed: {
    filteredResult: function () {
      let filteredWorkouts = [];
      if (this.workouts.length > 0) {
        for (let eachWorkout of this.workouts) {
          if (
            eachWorkout.workoutName.toLowerCase().includes(this.searchResult)
          ) {
            filteredWorkouts.push(eachWorkout);
          }
        }
      }
      return filteredWorkouts;
    },
  },
};
</script>

<style scoped>
#searchbar {
  width: 450px;
  border-radius: 5px;
}
.btn {
  margin: 1px;
  padding: 2px;
  cursor: pointer;
}
.card {
  width: 28rem;
  height: 40rem;
  overflow-x: hidden;
  overflow-y: scroll;
  border-radius: 10px;
  margin-bottom: 50px;
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