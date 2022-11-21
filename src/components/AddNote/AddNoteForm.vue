<template>
  <form @submit.prevent="onFormSubmit" class="d-flex flex-column gap-2 align-items-center">
    <div class="mb-3 w-100">
      <label for="noteTitle" class="form-label">Note Title</label>
      <input type="text" class="form-control" id="noteTitle" aria-describedby="noteTitledesc" ref="title" />
    </div>
    <div class="mb-3 w-100">
      <label for="noteDesc" class="form-label">Description</label>
      <input type="text" class="form-control" id="noteDesc" ref="desc" />
    </div>

    <button type="submit" class="btn btn-primary btn-lg float-center">Add Note</button>
  </form>
</template>

<script>
export default {
  emits: ["note_emit"],
  methods: {
    onFormSubmit() {
      let title = this.$refs.title.value;
      let desc = this.$refs.desc.value;
      this.$emit("note_emit", title, desc);
    },
  },
};
</script>
