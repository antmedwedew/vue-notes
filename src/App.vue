<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1 class="title">{{ title }}</h1>

          <Message v-if="message" :message="message" />

          <div class="new-note">
            <input v-model="note.title" type="text" />
            <textarea v-model="note.description"></textarea>
            <button @click="addNote">add note</button>
          </div>

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
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";

export default {
  components: {
    Message,
  },
  data() {
    return {
      title: "Notes app",
      message: null,
      note: {
        title: "",
        description: "",
      },
      notes: [],
    };
  },
  methods: {
    addNote() {
      let { title, description } = this.note;

      if (title === "") {
        this.message = "title can`t be blank!";
        return false;
      }

      this.notes.push({
        title,
        description,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.note.title = "";
      this.note.description = "";
      this.message = null;
    },
  },
};
</script>
 
<style lang="scss" scoped>
.title {
  text-align: center;
}
</style>