<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg sticky-top navbar-dark bg-dark">
      <div class="container-fluid">
        <div id="statusBox" class="alert alert-success my-5" v-if="status">{{ status }}</div>
        <a href="/"><img class="navbar-brand" id="logo" src="https://i.imgur.com/a9mMFf2.png" alt="HomePage"></a>

        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a
                class="nav-link"
                test-warning
                aria-current="page"
                v-on:click="goExercise"
                >Exercise Library</a
              >
            </li>
            <li class="nav-item">
              <a class="nav-link" v-on:click="goWorkout">Workout Library</a>
            </li>
          </ul>
        </div>
        <ul class="navbar-nav d-lg-none">
            <li class="nav-item">
              <a
                class="nav-link"
                test-warning
                aria-current="page"
                v-on:click="goExercise"
                >Exercise Library</a
              >
            </li>
            <li class="nav-item">
              <a class="nav-link" v-on:click="goWorkout">Workout Library</a>
            </li>
          </ul>
      </div>
    </nav>
    <div class="container">
      <exerciseLibrary
        v-if="page == 'exerciseLibrary'"
        v-on:exercise-add="onAddExercise"
        v-on:update-exercise="onEditExercise"
        v-on:delete-exercise="onDelExercise"
      />
      <workoutLibrary
        v-if="page == 'workoutLibrary'"
        v-on:addEx-Workout="onAddWorkoutEx"
        v-on:workout-add="onAddWorkout"
        v-on:update-wod-ex="onEditWodExercise"
        v-on:del-wod-ex="onDelWodExercise"
        v-on:updateWod="onUpdateWod"
        v-on:delete-wod="delWod"
      />
      <exerciseAdd
        v-if="page == 'exerciseAdd'"
        v-on:new-exercise-added="onExerciseAdded"
        v-on:add-ex-cancelled="onExAddCancelled"
      />
      <updateExercise
        v-if="page == 'updateExercise'"
        v-bind:exerciseId="exerciseBeingEdited"
        v-on:exercise-updated="onExerciseUpdated"
        v-on:update-exercise="onEditExercise"
        v-on:exUpdCancelled="cancelEditEx"
      />
      <addWorkoutExercise
        v-if="page == 'addWorkoutExercise'"
        v-bind:workoutId="addExToWod"
        v-on:wod-exercise-added="onWodExProcess"
        v-on:add-wod-ex-cancelled="addWodExCancel"
      />
      <updateWodExercise
        v-if="page == 'updateWodExercise'" 
        v-bind:wodexId="updateWodEx"
        v-on:wod-exercise-updated="onProcessWodExEdit"
        v-on:wod-ex-up-cancelled="wodExEditCancelled"   
      />
      <deleteWorkoutExercise 
        v-if="page == 'deleteWorkoutExercise'" 
        v-bind:wodexId="delExfrWod"
        v-on:wod-exercise-deleted="exDelFrWodProcess"
        v-on:workout-ex-del-cancelled="wodExDelCancelled"
      />
      <updateWorkout v-if="page == 'updateWorkout'" 
      v-bind:workoutId="wodBeingUpdated"
      v-on:workout-updated="wodUpdated"
      v-on:wodUpdCancelled="wodUpdateCancelled"
      />
      <deleteWorkout 
      v-if="page == 'deleteWorkout'"
      v-bind:workoutId="wodBeingDel"
      v-on:cancel-workout-del="onCancelWodDeletion"
      v-on:workout-deleted="ondeleteWod"
      />
      <exerciseDelete
        v-if="page == 'exerciseDelete'"
        v-bind:exerciseId="exBeingDel"
        v-on:delete-exercise="onDelExercise"
        v-on:exercise-deleted="onExDeleteProcess"
        v-on:ex-del-cancelled="exDelCancelProcess"
      />
      <addWorkoutPage
        v-if="page == 'addWorkoutPage'"
        v-on:new-workout-added="onWorkoutAddProcess"
        v-on:add-wod-cancelled="wodAddCancelled"
      />
    </div>
  </div>
</template>

<script>
import exerciseLibrary from "./components/exerciseLibrary";
import workoutLibrary from "./components/workoutLibrary";
import exerciseAdd from "./components/exerciseAdd";
import updateExercise from "./components/updateExercise";
import addWorkoutExercise from "./components/addWorkoutExercise";
import exerciseDelete from "./components/exerciseDelete";
import addWorkoutPage from "./components/addWorkoutPage";
import deleteWorkoutExercise from "./components/deleteWorkoutExercise";
import updateWorkout from "./components/updateWorkout";
import deleteWorkout from "./components/deleteWorkout";
import updateWodExercise from "./components/updateWodExercise";
export default {
  name: "App",
  components: {
    exerciseLibrary,
    workoutLibrary,
    exerciseAdd,
    updateExercise,
    addWorkoutExercise,
    exerciseDelete,
    addWorkoutPage,
    updateWodExercise,
    deleteWorkoutExercise,
    updateWorkout,
    deleteWorkout,
  },
  data: function () {
    return {
      page: "exerciseLibrary",
      status: "",
      exerciseBeingEdited: 0,
      exBeingDel: 0,
      addExToWod: 0,
      delExfrWod: 0,
      updateWodEx: 0,
      wodBeingUpdated: 0,
      wodBeingDel: 0,
      backgroundImg: {
        backgroundImage: "url(https://vuejs.org/images/logo.png)",
      },
    };
  },
  methods: {
    goExercise: function () {
      this.page = "exerciseLibrary";
      this.status = "";
    },
    goWorkout: function () {
      this.page = "workoutLibrary";
      this.status = "";
    },
    onAddExercise: function () {
      this.page = "exerciseAdd";
      this.status = "";
    },
    onExerciseAdded: function () {
      this.page = "exerciseLibrary";
      this.status = " Exercise added!";
    },
    onExAddCancelled: function () {
      this.page = "exerciseLibrary";
      this.status = "";
    },
    onEditExercise: function (exerciseId) {
      this.page = "updateExercise";
      this.status = "";
      this.exerciseBeingEdited = exerciseId;
    },
    onExerciseUpdated: function () {
      this.page = "exerciseLibrary";
      this.status = "Exercise Updated!";
    },
    cancelEditEx: function () {
      this.page = "exerciseLibrary";
    },
    onDelExercise: function (exerciseId) {
      this.page = "exerciseDelete";
      this.status = "";
      this.exBeingDel = exerciseId;
    },
    onAddWorkout: function () {
      this.page = "addWorkoutPage";
      this.status = "";
    },
    wodAddCancelled: function () {
      this.page = "workoutLibrary";
      this.status = "";
    },
    onUpdateWod: function (workoutId) {
      this.page = "updateWorkout";
      this.status = "";
      this.wodBeingUpdated = workoutId;
    },
    wodUpdated: function () {
      this.page = "workoutLibrary";
      this.status = "Workout Updated!";
    },
    ondeleteWod: function () {
      this.page = "workoutLibrary";
      this.status = "Workout Deleted!";
    },
    onCancelWodDeletion: function () {
      this.page = "workoutLibrary";
      this.status = "";
    },
    wodUpdateCancelled: function () {
      this.page = "workoutLibrary";
      this.status = "";
    },
    delWod: function (workoutId) {
      this.page = "deleteWorkout";
      this.status = "";
      this.wodBeingDel = workoutId;
    },
    onAddWorkoutEx: function (workoutId) {
      this.page = "addWorkoutExercise";
      this.status = "";
      this.addExToWod = workoutId;
    },
    addWodExCancel: function () {
      this.page = "workoutLibrary";
      this.status = "";
    },
    onEditWodExercise: function (wodexId) {
      this.page = "updateWodExercise";
      this.status = "";
      this.updateWodEx = wodexId;
    },
    onProcessWodExEdit: function () {
      this.page = "workoutLibrary";
      this.status = "Workout Exercise Updated!";
    },
    wodExEditCancelled: function () {
      this.page = "workoutLibrary";
      this.status = "";
    },
    onDelWodExercise: function (wodexId) {
      this.page = "deleteWorkoutExercise";
      this.status = "";
      this.delExfrWod = wodexId;
    },
    exDelFrWodProcess: function () {
      this.page = "workoutLibrary";
      this.status = "Exercise removed from workout!";
    },
    wodExDelCancelled: function () {
      this.page = "workoutLibrary";
    },
    onWorkoutAddProcess: function () {
      this.page = "workoutLibrary";
      this.status = "Workout Added!";
    },
    onWodExProcess: function () {
      this.page = "workoutLibrary";
      this.status = "Exercise Added to Workout!";
    },
    onExDeleteProcess: function () {
      this.page = "exerciseLibrary";
      this.status = "Exercise Deleted!";
    },
    exDelCancelProcess: function () {
      this.status = "";
      this.page = "exerciseLibrary";
    },
  },
};
</script>

<style>
#statusBox {
  position: absolute;
  top: 1.5em;
  left: 1em;
  border: none;
  background: rgba(241, 185, 0.4, 0.5);
  color: black;
}
#app {
  background-image: linear-gradient(
    0deg,
    rgb(223, 222, 217),
    rgb(255, 255, 255)
  );
}
#logo {
  width: 200px;
}
</style>

