<template>
  <div class="flex justify-center w-auto">
    <div class="grid justify-items-center">
      <h1 class="text-3xl py-3 mt-4 font-bold">ToDoリスト</h1>
      <div class="flex my-4">
        <!-- 入力部分 -->
        <input v-model="todoInput" class="border-solid border-2 rounded-md"/>

        <!-- 追加ボタン -->
        <button @click="addTodo" class="bg-blue-500 hover:bg-blue-300 rounded-md text-white py-2 px-4 mx-2">
          追加
        </button>
      </div>

      <!-- ToDoリスト -->
      <div v-for="todo in todos" key="id" class="p-3 m-2 rounded-md min-w-full flex items-center justify-between">
        <p :class="{ 'line-through    ': todo.isCompleted }">{{ todo.title }}</p>
        <div>
            <!-- 完了ボタン -->
            <button v-show="!todo.isCompleted" @click="toggleComplete(todo.id)" class="py-1 px-2 bg-green-500 hover:bg-green-300 mx-1 rounded-md text-white">
                完了
            </button>

            <!-- 未完了ボタン -->
            <button v-show="todo.isCompleted" @click="toggleComplete(todo.id)" class="py-1 px-2 bg-blue-500 hover:bg-blue-300 mx-1 rounded-md text-white">
                未完了
            </button>

            <!-- 削除ボタン -->
            <button @click="deleteTodo(todo.id)" class="py-1 px-2 bg-red-500 hover:bg-red-300 mx-1 rounded-md text-white">
                削除
            </button>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, reactive } from 'vue';
const todoInput = ref('');
const todos = reactive([
  {
    id: 1,
    title: 'Task to do',
    isCompleted: true,
  },
  {
    id: 2,
    title: 'Task to do',
    isCompleted: false,
  },
]);

// 削除処理
function deleteTodo(id) {
  todos.pop(id);
  console.log('delete');
}

// 追加処理
function addTodo() {
  todos.push({
    id: todos.length + 1,
    title: todoInput.value,
    isCompleted: false,
  });
  todoInput.value = '';
  console.log('add');
}

// 完了 未完了処理
function toggleComplete(id) {
  const index = todos.findIndex((todo) => todo.id === id);
  todos[index].isCompleted = !todos[index].isCompleted;
}
</script>