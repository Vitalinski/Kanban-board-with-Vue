<template>
  <nav-bar></nav-bar>

  <div class="main-page">
    <Spinner v-if="isLoaderActive"></Spinner>
<div v-else>
  
      <OverlayForm v-model:isActive="isActive"></OverlayForm>
  
      <div v-if="Object.keys(store.tasks).length > 0">
        <div class="buttons">
          <div class="buttons__add">
            <button class="buttons__btn btn" @click="store.showForm()">
            {{ $t('mainPage.addTask') }}
            </button>
          </div>
          <div class="buttons__sort">
            <button class="buttons__btn btn" @click="store.sortByDate()">
              {{ $t('mainPage.sortByDate') }}
            </button>
            <button class="buttons__btn btn" @click="store.sortByPriority()">
              {{ $t('mainPage.sortByPriority') }}
            </button>
          </div>
        </div>
        <TasksColumn class="columns"></TasksColumn>
      </div>
      <Initial v-else> </Initial>
</div>
  </div>
</template>

<script>
import Spinner from "../components/Spinner.vue";
import { useToDoStore } from "../store/store";
import Initial from "../components/Initial.vue";
import OverlayForm from "../components/OverlayForm.vue";
import TasksBoard from "../components/TasksBoard.vue";
import TasksColumn from "../components/TasksColumn.vue";
import NavBar from "../components/NavBar.vue";

export default {
  name: "MainPage",
  components: {
    Initial,
    TasksBoard,
    OverlayForm,
    TasksColumn,
    NavBar,
    Spinner,
  },

  data() {
    return {
      store: useToDoStore(),
    };
  },

  mounted() {
    this.store.getTasks();
  },
 
  computed: {
    isActive() {
      return useToDoStore().isActive;
    },
    isLoaderActive(){
      return useToDoStore().isLoaderActive
    }
  },
};
</script>

<style >
.columns {
  overflow: auto;
}
</style>


