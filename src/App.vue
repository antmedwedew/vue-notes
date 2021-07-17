<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1 class="title">{{ title }}</h1>

          <Message v-if="message" :message="message" />

          <NewNote :note="note" @addNote="addNote" />

          <Notes :notes="notes" @remove="removeNote" />

        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";
import NewNote from "@/components/NewNote.vue";
import Notes from "@/components/Notes.vue";

export default {
  components: {
    Message,
    NewNote,
    Notes,
  },
  data() {
    return {
      title: "Notes app",
      message: null,
      notes: [],
      note: {
        title: "",
        description: "",
      },
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

    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

 
<style lang="scss" scoped>
.title {
  text-align: center;
}
</style>