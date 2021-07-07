<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1>{{ title }}</h1>

          <div class="error-message" v-if="errorMessage">
            {{ errorMessage }}
          </div>

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
export default {
  data() {
    return {
      title: "Notes app",
      errorMessage: null,
      note: {
        title: "",
        description: "",
      },
      notes: [
        {
          title: "First Note",
          description: "Description note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second Note",
          description: "Description note",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third Note",
          description: "Description note",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  methods: {
    addNote() {
      let { title, description } = this.note;

      if (title === "") {
        this.errorMessage = "title can`t be blank!";
        return false;
      }

      this.notes.push({
        title,
        description,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.note.title = "";
      this.note.description = "";
      this.errorMessage = null;
    },
  },
};
</script>