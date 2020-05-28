<template>
  <v-app>
    <v-container fluid class="bg">
      <v-col xs="12" md="8" class="mx-auto">
        <Input @add-todo="addTodo" />
        <v-select class="mt-5" v-model="filter" :items="items" label="Фільтр" dense outlined></v-select>
        <v-divider></v-divider>
        <h3>Список справ :</h3>
        <v-row dense v-if="filteredTodos.length">
          <v-col v-for="(todo, i) in filteredTodos" :index="i" :key="todo.id" cols="12">
            <v-card class="d-flex justify-space-between">
              <div class="subtitle-1 black--text">
                <div class="d-flex align-center ml-3">
                  <v-checkbox v-model="todo.complited"></v-checkbox>
                  <strong class="mr-2">{{i + 1}}</strong>
                  <input v-if="isEdit" v-model="todo.title" @keyup="submitForm" />
                  <span
                    v-if="!isEdit"
                    @dblclick="showEditForm()"
                    :class="{done: todo.complited}"
                  >{{todo.title}}</span>
                </div>
              </div>
              <v-card-actions>
                <v-btn icon x-small fab color="error" @click="removeTodo(todo.id)">
                  <v-icon>mdi-close</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
        <v-card v-else>
          <v-card-text>No todos!</v-card-text>
        </v-card>
      </v-col>
    </v-container>
  </v-app>
</template>

<script>
import Input from "@/components/Input";
export default {
  name: "App",

  components: {
    Input
  },

  data: () => ({
    todos: [
      { id: 1, title: "Купити хліб", complited: false },
      { id: 2, title: "Купити масло", complited: false },
      { id: 3, title: "Купити молоко", complited: false }
    ],
    items: ["Всі", "Завершені", "Незавершені"],
    filter: "Всі",
    isEdit: false
  }),
  computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    filteredTodos() {
      if (this.filter === "Всі") {
        return this.todos;
      }
      if (this.filter === "Завершені") {
        return this.todos.filter(t => t.complited);
      }
      if (this.filter === "Незавершені") {
        return this.todos.filter(t => !t.complited);
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
    showEditForm() {
      this.isEdit = !this.isEdit;
    },
    submitForm(e) {
      if (e.keyCode === 13) {
        this.showEditForm();
      }
    }
  }
};
</script>
<style scoped>
.done {
  text-decoration: line-through;
}
.bg {
  background: #7f7fd5;
  background: linear-gradient(to right, #91eae4, #86a8e7, #7f7fd5);
}
</style>
