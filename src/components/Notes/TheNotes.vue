<template>
  <ul v-if="notes_list?.length > 0" class="list-group">
    <notes-list-item
      v-for="item in notes_list"
      :key="item.id"
      :title="item.title"
      :description="item.description"
      :id="item.id"
    ></notes-list-item>
  </ul>
  <h4 v-else class="text-center">No Notes found!!</h4>
</template>

<script>
import NotesListItem from "./NotesListItem.vue";
export default {
  components: {
    NotesListItem,
  },
  props: {
    notes_list: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
}
</style>
