<template>
  <DataPanel :products="products" :currentPage="currentPage"/>
  <ProductInfo :products="products"/>
  <Pagination 
    :products="products" 
    v-if="products.length"
    @changePage = changePage
  />
</template>


<script setup>
import DataPanel from "../components/DataPanel.vue";
import ProductInfo from "../components/ProductInfo.vue";
import Pagination from "../components/Pagination.vue";
import { reactive, ref } from "@vue/reactivity";
import { onMounted } from "vue";
import axios from "axios";

const products = reactive([]);

const isLoaded = ref(false)
const currentPage = ref(1)
const changePage = (id) => currentPage.value = id

onMounted(() => {
  axios
    .get("http://makeup-api.herokuapp.com/api/v1/products.json?brand=maybelline")
    .then((response) => {
      const data = response.data;
      data.forEach((e, index) => {
        products.push({ ...e, page: Math.ceil((index + 1) / 10) });
      });
    })
    .catch((error) => console.log(error));
  isLoaded.value = true
});

</script>
