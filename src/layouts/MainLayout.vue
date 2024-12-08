<template>
  <q-container class="bg-blue-12 flex justify-center" style="height: 100vh">
    <div class="inputBtn">
      <input v-model="newtask" label="Add your task here" class="newinput" />
      <q-btn class="button" @click="add"
        ><i class="fa-solid fa-plus addIcon"></i
      ></q-btn>
      <q-list class="list">
        <q-item
          class="item"
          v-for="(task, index) in tasks"
          :key="index"
          :style="itemStyle"
        >
          <input
            v-model="tasks[index]"
            v-if="taskeditVisible === index"
            label="Edit your task:"
          />
          <p v-if="IsparaVisible === index ? false : true">
            {{ task }}
          </p>
          <span class="icons">
            <q-icon
              class="icon"
              color="red"
              v-if="IsVisibleRemove"
              @click="remove(index)"
              name="delete"
            ></q-icon>
            <q-icon
              class="icon"
              color="black"
              v-if="IsVisibleEdit === index ? false : true"
              @click="edit(index)"
              name="edit"
            ></q-icon>
            <q-icon
              class="icon"
              color="black"
              v-if="IsVisibleCancel"
              @click="cancel"
              name="cancel"
            ></q-icon>

            <q-icon
              class="icon"
              color="blue"
              v-if="IsVisibleSave === index ? false : true"
              @click="save(index)"
              name="save"
            ></q-icon
          ></span>
        </q-item>
      </q-list>
    </div>
  </q-container>
</template>

<script setup>
import { ref } from "vue";

const newtask = ref("");
const tasks = ref([]);
const IsVisibleRemove = ref(true);
const IsVisibleEdit = ref("");
const IsVisibleCancel = ref(false);
const IsVisibleSave = ref(false);
const IsparaVisible = ref("");
const taskeditVisible = ref("");
const add = () => {
  if (newtask.value === "") {
    alert("pleasse add atleast one task *");
  } else {
    tasks.value.push(newtask.value);
    newtask.value = "";
  }
};
const remove = (index) => {
  tasks.value.splice(index, 1);
};
const edit = (index) => {
  IsVisibleSave.value = index;
  IsVisibleEdit.value = index;
  IsparaVisible.value = index;
  tasks.value[index] = tasks.value[index];
  taskeditVisible.value = index;
};

const save = (index) => {
  editOpt.value = true;
  saveOpt.value = false;
  parahide.value[index] = false;
  if (tasks.value[index] === newInput.value[index]) {
    alert("already exist");
  }
};

const cancel = () => {
  newInput.value = false;
  saveOpt.value = false;
  editOpt.value = true;
  cancelOpt.value = false;
  parahide.value = true;
};
</script>
<style scoped>
.container {
  background-color: #d2d2d2;
  width: 100%;
}
.inputBtn {
  height: 50px;
  width: 500px;
  max-width: 80%;
  background-color: #f5f0cd;
  display: flex;
  flex-wrap: wrap;
}
.list {
  width: 100%;
  backdrop-filter: blur(20px);
}
.newinput {
  background-color: red;
  width: 80%;
  height: 100%;
}
.button {
  background-color: aqua;
  width: 20%;
  height: 100%;
}
.addIcon {
  color: #000;
  font-size: 20px;
}
/* .list {
  width: 100%;
  height: 100%;
  margin: 5px;
} */
.item {
  display: flex;
  justify-content: space-evenly;
  height: 20%;
  width: 100%;
  color: black;
  background-color: #d3f1df;
  gap: 10px;
  box-shadow: -2px 0px 1px 0px #000 inset, 2px 0px 1px 0px #000 inset;
}
.item p {
  width: 100%;
  height: 100%;
  margin: auto;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  box-shadow: 0 0 1px 1px #000;
  padding: 5px;
}
.icons {
  color: black;
  width: max-content;
  font-size: 20px;
  display: flex;
  margin: auto;
  justify-content: space-evenly;
  gap: 5px;
}
.newField {
  width: 20px;
  height: 20px;
  margin: auto;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  box-shadow: 0 0 1px 1px #000;
  padding: 5px;
}
</style>
