<script setup>
import { ref, computed } from 'vue'

let item = ref('')
let lista = ref([
  { name: 'Compras', done: true },
  { name: 'qualquer coisa', done: false }
])

const totalTarefas = computed(() => {
  return lista.value.length
})

const totalTrue = computed(() => {
  let completas = 0
  for (const coiso of lista.value) {
    if (coiso.done == true) {
      completas = completas + 1
      console.log(completas.done)
    }
  }
  return completas
})

function addItem() {
  const objeto = {
    name: item.value,
    done: false
  }
  lista.value.push(objeto)
  item.value = ''
}

function removeItem(indice) {
  lista.value.splice(indice, 1)
}
</script>

<template>
  <div class="container">
    <div class="title">Todo List</div>
    <div class="createItem">
      <input type="text" placeholder="Add Item" class="oneBox" v-model="item" />
      <button class="add" @click="addItem()">Add</button>
    </div>
    <div class="contador">{{ totalTrue }}/{{ totalTarefas }} Completed</div>
    <div class="list" v-for="(item, index) in lista" :key="index">
      <div>
        <input type="checkbox" v-model="item.done" /> <span>{{ item.name }}</span>
      </div>
      <button class="remove" @click="removeItem(index)">Remove</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: baseline;
  gap: 10px;
  width: 30%;
  padding: 15px;
  background-color: white;
  box-shadow: 1px 1px 12px gray;
  border-radius: 5px;

  > .title {
    font-weight: bold;
    font-size: 1.35em;
  }

  > .createItem {
    display: flex;
    flex-direction: row;
    gap: 10px;
    justify-content: space-between;

    > .oneBox {
      flex-grow: 1;
      box-shadow: 0px 2px 2px gray;
    }

    > .add {
      border-radius: 5px;
      border: 2px solid #40e0d0;
      padding: 5px;
      background-color: white;
      color: #40e0d0;
    }
  }

  > .contador {
    display: flex;
    flex-direction: row;
    justify-content: end;
  }

  > .list {
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    > .remove {
      border-radius: 5px;
      border: 2px solid red;
      padding: 5px;
      background-color: white;
      color: red;
    }
  }
}
</style>
