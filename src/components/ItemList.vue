<script setup>
import { ref } from "vue";

const undoneitems = ref([]);

const doneitems = ref([]);

let newItemId = 0;
const newItemName = ref("");
const newItemDone = ref(false);

const addItem = () => {
  if (newItemName.value != "") {
    undoneitems.value.push({
      id: newItemId,
      name: newItemName.value,
      done: false,
    });
    newItemId++;
    newItemName.value = "";
    newItemDone.value = false;
  }
};

const TaskDone = (id) => {
  const index = undoneitems.value.findIndex((item) => item.id === id);
  if (index !== -1) {
    undoneitems.value[index].done = true;
    let tmp = undoneitems.value.splice(index, 1);
    doneitems.value.push(tmp[0]);
  }
};
</script>

<template>
  <div>
    <div id="Lists" class="flex">
      <div>
        <div class="items">UndoneList</div>
        <div v-for="item in undoneitems" :key="item.id">
          <div class="item">
            <!-- <div class="id">ID: {{ item.id }}</div> -->
            <div class="name">{{ item.name }}</div>
            <!-- <div class="done">{{ item.done }}</div> -->
            <div>
              <button @click="TaskDone(item.id)">完了！</button>
            </div>
          </div>
        </div>
      </div>
      <div>
        <div class="items">DoneList</div>
        <div v-for="item in doneitems" :key="item.id">
          <div class="item">
            <!-- <div class="id">ID: {{ item.id }}</div> -->
            <div class="name">{{ item.name }}</div>
            <!-- <div class="done">{{ item.done }}</div> -->
          </div>
        </div>
      </div>
    </div>

    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <button @click="addItem">add</button>
    </div>
  </div>
</template>

<style>
.flex {
  display: flex;
  justify-content: center;
}
.items {
  margin: 30px;
}
.item {
  margin: 10px;
}
.over500 {
  color: red;
}
</style>

<style></style>
