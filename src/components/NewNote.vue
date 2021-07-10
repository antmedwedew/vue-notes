<template>
  <div class="new-note">
    <label for="name">Title</label>
    <input v-model="note.title" type="text" id="name" />
    <label for="description">Description</label>
    <textarea v-model="note.description" id="description"></textarea>
    <button class="btn btn--primary new-note__btn" @click="addNote">
      add note
    </button>
  </div>
</template>


<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    },
  },
};
</script>


<style lang="scss">
.new-note {
  text-align: center;

  &__btn {
    margin-top: 25px;
  }
}
</style>