<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1 class="title">{{ title }}</h1>

          <Message v-if="message" :message="message" />

          <NewNote :note="note" @addNote="addNote" />

          <div class="notes-controls">
            <div class="notes-controls__icons">
              <IconColumn :class="{ active: grid }" @click="grid = true" />
              <IconGrid :class="{ active: !grid }" @click="grid = false" />
            </div>
            <Search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />
          </div>

          <Notes :notes="notesFilter" @remove="removeNote" :grid="grid" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";
import NewNote from "@/components/NewNote.vue";
import Notes from "@/components/Notes.vue";
import Search from "@/components/Search.vue";

import IconColumn from "@/assets/svg/column.svg";
import IconGrid from "@/assets/svg/grid.svg";

export default {
  components: {
    Message,
    NewNote,
    Notes,
    Search,

    IconColumn,
    IconGrid,
  },
  data() {
    return {
      title: "Notes app",
      search: "",
      message: null,
      grid: true,
      notes: [],
      note: {
        title: "",
        description: "",
      },
    };
  },
  computed: {
    notesFilter() {
      let array = this.notes;
      let search = this.search;

      if (!search) return array;
      // small
      search = search.trim().toLowerCase();
      // filter
      array = array.filter((item) => {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      return array;
    },
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
.notes-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 15px;

  svg {
    cursor: pointer;
    margin-right: 10px;
    color: #999999;

    &.active {
      color: #402caf;
    }

    &:last-child {
      margin-right: 0;
    }
  }
}
</style>