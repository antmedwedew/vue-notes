<template>
  <div class="new-note">
    <label for="name">Title</label>
    <input v-model="note.title" type="text" id="name" />
    <label>important</label>
    <div class="new-note__importance">
      <div class="new-note__checkbox">
        <input
          type="radio"
          name="important"
          id="standart"
          v-model="activeColor"
          value=""
          @change="change"
        />
        <label for="standart">standart</label>
        <input
          type="radio"
          name="important"
          id="important"
          v-model="activeColor"
          value="orange"
          @change="change"
        />
        <label for="important">important</label>
        <input
          type="radio"
          name="important"
          id="very-important"
          v-model="activeColor"
          value="red"
          @change="change"
        />
        <label for="very-important">very-important</label>
      </div>
    </div>
    <label for="description">Description</label>
    <textarea v-model="note.description" id="description"></textarea>
    <button class="btn btn--primary new-note__btn" @click="addNote">
      add note
    </button>
  </div>
</template>


<script>
export default {
  data() {
    return {
      activeColor: "",
    };
  },
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
      this.activeColor = "";
    },

    change() {
      this.$emit("changeRadio", this.activeColor);
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

  &__importance {
    display: flex;
    justify-content: center;

    input {
      width: auto;
      margin-right: 10px;
      cursor: pointer;
    }

    label {
      margin-right: 10px;
      cursor: pointer;
    }
  }

  &__checkbox {
    display: flex;
    align-items: baseline;
  }
}
</style>