<template>
  <v-form v-on:submit.prevent="submitInput" ref="form">
    <v-text-field
      v-model="title"
      label="Нова справа"
      :rules="rule"
      :counter="counterEn"
      append-icon="mdi-plus"
      @click:append="addTodo"
    ></v-text-field>
    <!-- <v-btn class="success mb-3" @click="addTodo">Додати</v-btn> -->
  </v-form>
</template>

<script>
export default {
  data() {
    return {
      counterEn: 50,
      rule: [
        v =>
          (v.trim().length >= 5 && v.trim().length <= this.counterEn) ||
          `Мін. довживна 5 смволів макс.- ${this.counterEn}`
      ],
      title: ""
    };
  },
  methods: {
    addTodo() {
      if (this.$refs.form.validate()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          complited: false
        };
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    },
    submitInput(e) {
      e.preventDefault();
      this.addTodo();
    }
  }
};
</script>