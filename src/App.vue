<template>
  <NavBar :title="'Notes App'" :search-handler="searchHandler" />
  <div class="container mt-5">
    <TheLoader v-show="loading" :color="'dark'" />
    <div class="row g-5">
      <div class="col-12 col-md-6">
        <h2 class="text-center">Add Note</h2>
        <AddNoteForm @note_emit="addNoteHandler" />
      </div>
      <div class="col-12 col-md-6">
        <h2 class="text-center">Notes</h2>
        <TheNotes class="mt-5" :notes_list="showList" />
      </div>
    </div>
  </div>
</template>

<script>
import TheNotes from "./components/Notes/TheNotes.vue";
import AddNoteForm from "./components/AddNote/AddNoteForm.vue";
import NavBar from "./components/UI/NavBar.vue";
import TheLoader from "./components/UI/TheLoader.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    TheNotes,
    AddNoteForm,
    NavBar,
    TheLoader,
  },
  data() {
    return {
      db_url: process.env.VUE_APP_URL,
      lists: [],
      loading: false,
      filteredNotes: {
        show: false,
        value: [],
      },
    };
  },
  provide() {
    return {
      addFavourite: this.addFavouriteHandler,
      deleteNoteHandler: this.deleteNoteHandler,
    };
  },
  watch: {
    lists: {
      handler: function () {
        this.filteredNotes = { show: false, value: [] };
      },
      deep: true,
    },
  },
  computed: {
    showList() {
      if (this.filteredNotes.show) {
        console.log("found search value");
        return this.filteredNotes.value;
      } else {
        console.log("nothing found");
        return this.lists;
      }
    },
  },
  methods: {
    async addNoteHandler(title, description) {
      this.loading = true;
      try {
        let { data } = await axios.post(this.db_url + "notes.json", {
          title,
          description,
        });
        if (data && typeof data == "object") {
          this.lists.unshift({
            id: data.name,
            title,
            description,
          });
        } else {
          throw new Error("Can't add notes!");
        }
      } catch (err) {
        console.log("we got error", err);
      } finally {
        this.loading = false;
      }
    },
    addFavouriteHandler(id) {
      console.log("we got id", id);
    },
    async deleteNoteHandler(id) {
      this.loading = true;
      try {
        let res = await axios.delete(this.db_url + `notes/${id}.json`);
        console.log("we got res", res);
        let index = this.lists.findIndex((note) => note.id == id);
        this.lists.splice(index, 1);
      } catch (err) {
        console.log("we got error", err);
      } finally {
        this.loading = false;
      }
    },
    async getAllNotes() {
      this.loading = true;
      try {
        let { data } = await axios.get(this.db_url + "notes.json");
        if (data && typeof data == "object") {
          let arr = [];
          for (let key in data) {
            arr.push({ id: key, title: data[key].title, description: data[key].description });
          }
          this.lists = arr.reverse();
        } else {
          throw new Error("Something went wrong!");
        }
      } catch (err) {
        console.log("Error occured", err);
      } finally {
        this.loading = false;
      }
    },
    searchHandler(val) {
      if (val.length > 0) {
        let filteredNotes = this.lists.filter((note) => note.title.includes(val) || note.description.includes(val));
        this.filteredNotes = { value: filteredNotes, show: true };
      } else {
        this.filteredNotes = { value: [], show: false };
      }
    },
  },
  mounted() {
    console.log("got mounted");
    this.getAllNotes();
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.container-width {
  max-width: 600px;
}
</style>
