<template>
  <div class="notes">
    <p v-if="notes.length === 0" class="notes__empty">no notes</p>

    <div
      class="note"
      :class="({ full: !grid }, `${note.color}`)"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note__header">
        <p>{{ note.title }}</p>
        <button class="btn btn--danger" @click="removeNote(index)">X</button>
      </div>
      <div class="note__body">
        <p>{{ note.description }}</p>
      </div>
      <span class="note__date">{{ note.date }}</span>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
    color: {
      type: String,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      this.$emit("remove", index);
    },
  },
};
</script>


<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;

  &__empty {
    margin: 0 auto;
    font-size: 25px;
    color: #999999;
  }
}

.note {
  width: 48%;
  padding: 20px;
  margin-bottom: 20px;
  background-color: #ffffff;

  &.full {
    width: 100%;
  }

  &.orange {
    background-color: #fed330;
  }

  &.red {
    background-color: #fc5c65;
  }

  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;

    p {
      font-size: 22px;
      color: #402caf;
      padding-right: 10px;
    }
  }

  &__body {
    p {
      margin: 15px 0;
    }
  }

  &__date {
    font-size: 14px;
    color: #999999;
  }
}
</style>