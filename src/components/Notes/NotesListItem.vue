<template>
  <li class="mb-4">
    <div class="card w-100 mx-auto">
      <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">{{ description }}</p>
        <button class="btn btn-success" type="button" @click="addFavourite(id)">Add to Favorite</button>
        <button class="btn btn-danger ms-5" type="button" @click="deleteNoteHandler(id)">Delete</button>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  inject: ["addFavourite", "deleteNoteHandler"],
  props: ["title", "description", "id"],
};
</script>
