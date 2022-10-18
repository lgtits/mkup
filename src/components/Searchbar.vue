<template>
  <div class="container mt-5">
    <div class="row" id="search-bar">
      <form id="search" class="form-inline">
        <label class="sr-only" for="inlineFormInputName2">Name</label>
        <input type="text" class="form-control mb-2 mr-sm-2" id="search-input" placeholder="search name ..." v-model="keyword">
        <button type="submit" class="btn btn-primary mb-2" @click.prevent="searchProduct">Search</button>
      </form>
    </div>
    </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const searchProductName = ref()
const keyword = ref()

const searchProduct= () => {
      searchProductName = keyword.trim().toLowerCase();
      keyword = "";
    },
</script>