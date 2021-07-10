<template>
  <div class="notes">
    <div class="note" v-for="(note, index) in notes" :key="index">
      <div class="note__header">
        <p>{{ note.title }}</p>
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
}

.note {
  width: 48%;
  padding: 20px;
  margin-bottom: 20px;
  background-color: #ffffff;

  &__header {
    p {
      font-size: 22px;
      color: #402caf;
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