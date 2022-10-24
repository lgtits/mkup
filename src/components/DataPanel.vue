<template>
  <div class="container mt-5">
    <div class="row" id="search-bar">
      <form id="search" class="form-inline">
        <label class="sr-only" for="inlineFormInputName2">Name</label>
        <input
          type="text"
          class="form-control mb-2 mr-sm-2"
          id="search-input"
          placeholder="search name ..."
          v-model="keyword"
        />
        <button type="submit" class="btn btn-primary mb-2" @click.prevent="searchProduct">
          Search
        </button>
      </form>
    </div>
  </div>

  <div class="container mt-5">
    <div class="row" id="data-panel">
      <div class="col-sm-3 card_wrapper" 
        v-for="product in filterProducts" 
        :key="product.id" 
        :class="{ 'display': product.page === currentPage }"
      > 
        <div class="card mb-2">
          <img class="card-img-top" alt="Card image cap" :src="product.image_link" />
          <div class="card-body product-item-body">
            <h5 class="card-title">{{ product.name }}</h5>
          </div>
          <!-- "More" button -->
          <div class="card-footer d-flex justify-content-around">
            <button
              class="btn btn-primary btn-show-product"
              data-toggle="modal"
              data-target="#show-product-modal"
              @click="showDetail(product)"
            >
              More
            </button>
            <div class="showInfo" v-if="showInfo">
              <div>
                <ProductInfo
                  :moreInfo="moreInfo"
                  
                  @close-info="closeInfo"
                />
              </div>
            </div>
            <button
              class="btn btn-success btn-show-product"
              @click="addFavorite(product.id)"
            >
              +
            </button>
          </div>
        </div>
      </div>
      <div v-if="filterProducts.length === 0">查無此相關商品...</div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "@vue/reactivity";
import { computed, onBeforeMount, onMounted } from "@vue/runtime-core";
import axios from "axios";
import ProductInfo from "../components/ProductInfo.vue";

// const BASE_URL = "http://makeup-api.herokuapp.com";
// const INDEX_URL = BASE_URL + "/api/v1/products.json"

const props = defineProps({
  products: {
    type: Array,
    required: true,
  },
  currentPage: {
    type: Number,
    required: true,
  }
});
// const products = reactive([]);
const searchProductName = ref("");
const keyword = ref();
const showInfo = ref(false);
const moreInfo = ref('')

// onBeforeMount(() => {
//   console.log("myheader mounted");
//   axios
//     .get("http://makeup-api.herokuapp.com/api/v1/products.json?brand=maybelline")
//     .then((response) => {
//       const data = response.data;
//       data.forEach((e) => {
//         products.push(e);
//       });
//     })
//     .catch((error) => console.log(error));
// });

const searchProduct = () => {
  searchProductName.value = keyword.value.trim().toLowerCase();
  keyword.value = "";
};

const filterProducts = computed(() =>
  props.products.filter((product) =>
    product.name.toLowerCase().includes(searchProductName.value)
  )
);

const showDetail = (product) => {
  // const product = props.products.find((product) => product.id === productId);
  // if (product.id === productId) {
  //   showInfo.value = true;
  // }
  // console.log(productId)
  // console.log(product)
  showInfo.value = true;
  moreInfo.value = product
};

const closeInfo = () => {
  showInfo.value = false;
};

const addFavorite= (id) => {
      console.log("add favorite");
      const list = JSON.parse(localStorage.getItem("makeup-app-vue")) || [];
      const product = props.products.find((product) => product.id === id);
      if (list.some((product) => product.id === id)) {
        return alert("此商品已經在收藏清單中！");
      }
      list.push(product);
      localStorage.setItem("makeup-app-vue", JSON.stringify(list));
    }

</script>

<style scoped>
.container{
  background: transparent;
}

.card_wrapper{
  display: none;
}

.display{
  display: block;
}
</style>