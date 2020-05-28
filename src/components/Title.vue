<template>
  <v-form @submit.prevent="showEditForm" ref="form" class="d-flex align-center">
    <v-text-field
      v-if="isEdit"
      v-model="todo.title"
      :counter="counterEn"
      :rules="rule"
      append-icon="mdi-check"
      @click:append="showEditForm"
    />
    <span v-if="!isEdit" :class="{done: todo.complited}">{{todo.title}}</span>
    <v-btn v-if="!isEdit" icon @click="showEditForm">
      <v-icon>mdi-pencil</v-icon>
    </v-btn>
  </v-form>
</template>

<script>
export default {
  data() {
    return {
      isEdit: false,
      counterEn: 50,
      rule: [
        v =>
          (v.trim().length >= 5 && v.trim().length <= this.counterEn) ||
          `Мін. довживна 5 смволів макс.- ${this.counterEn}`
      ]
    };
  },
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    showEditForm() {
      if (this.$refs.form.validate()) {
        this.isEdit = !this.isEdit;
      }
    }
  }
};
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>