<template>
  <div class="w-4/12 m-auto">
    <div class="w-auto">
      <input
        class="mt-1 mr-1 px-2 py-1 w-[73%] bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 rounded-md focus:ring-1 inline-block text-base"
        type="text"
        v-model="todoName"
      />
      <button
        @click="submitHendeler"
        v-if="!isEdit"
        class="bg-sky-500 hover:bg-sky-600 rounded p-1 px-5 text-lg text-white shadow-lg shadow-sky-500/50"
      >
        Add Todo
      </button>
      <button
        @click="updateHendeler"
        v-if="isEdit"
        class="bg-sky-500 hover:bg-sky-600 rounded py-1 px-2 text-lg text-white shadow-lg shadow-sky-500/50"
      >
        Update Todo
      </button>
    </div>
    <div>
      <ul class="mt-3">
        <li
          class="list-none w-full flex justify-between mb-3 p-2 bg-sky-500 rounded shadow shadow-sky-500/50"
          v-for="todo in todos"
          :key="todo.id"
        >
          <span class="text-white text-lg">{{ todo.name }}</span>
          <div>
            <button
              @click="() => editHendeler(todo)"
              class="bg-green-600 px-3 py-1 text-white ml-1 rounded shadow shadow-green-500/50"
            >
              Edit
            </button>
            <button
              @click="() => deleteHendeler(todo.id)"
              class="bg-red-600 px-3 py-1 text-white ml-1 rounded shadow shadow-red-500/50"
            >
              Delete
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "RootApp",
  data() {
    return {
      todoName: "",
      todos: [],
      isEdit: false,
      editId: null,
    };
  },
  methods: {
    submitHendeler() {
      if (this.todoName !== "") {
        const newObject = {
          id: Date.now(),
          name: this.todoName,
        };

        this.todos = [newObject, ...this.todos];
        this.todoName = "";
      } else {
        alert("Enter The Todo");
      }
    },
    editHendeler({ name, id }) {
      this.isEdit = true;
      this.todoName = name;
      this.editId = id;
    },
    deleteHendeler(id) {
      this.todos = [...this.todos.filter((items) => items.id !== id)];
    },

    updateHendeler() {
      if (this.todoName !== "") {
        this.todos = [
          ...this.todos
            .filter((items) => items.id === this.editId)
            .map((item) => ({ ...item, name: this.todoName })),
          ...this.todos
            .filter((items) => items.id !== this.editId)
            .map((item) => ({ ...item })),
        ];

        this.todoName = "";
        this.isEdit = false;
      } else {
        alert("Update Your Todos");
      }
    },
  },
};
</script>
