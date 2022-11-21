<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">{{ title }}</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="true"
        aria-label="Toggle navigation"
        @click="mobile_nav = !mobile_nav"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" :class="{ show: mobile_nav }" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto me-3 mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active user-select-auto" aria-current="page">Notes</a>
          </li>
          <li class="nav-item">
            <a class="nav-link pe-auto">Add Notes</a>
          </li>
        </ul>
        <form class="d-flex" role="search" @submit.prevent="searchHandler(searchInput)">
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" v-model.trim="searchInput" />
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  props: ["title", "searchHandler"],

  data() {
    return { mobile_nav: false, searchInput: "" };
  },
};
</script>
