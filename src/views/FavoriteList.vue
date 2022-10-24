<template>
  <div class="container mt-5">
    <div class="row" id="data-panel">
      <div v-for="product in products" :key="product" class="col-sm-3 fav-products">
        <div class="card mb-2">
          <img
            class="card-img-top"
            :src="product.image_link"
            alt="Card image cap"
          />
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
              class="btn btn-danger btn-show-product"
              @click="removeProduct(product.id)"
            >
              x
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-if="products.length === 0">
      <p>尚未蒐藏任何商品！</p>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";
import ProductInfo from "../components/ProductInfo.vue";

const products = reactive([]);
const showInfo = ref(false);
const moreInfo = ref('')
onMounted(() => {
  const data = JSON.parse(localStorage.getItem("makeup-app-vue"));
  data.forEach((e) => {
    products.push(e);
  });
});

const removeProduct = (id) => {
  const list = products;
  const productIndex = list.findIndex((product) => product.id === id);
  if (productIndex === -1) return;
  list.splice(productIndex, 1);
  localStorage.setItem("makeup-app-vue", JSON.stringify(list));
};

const showDetail = (product) => {
  // const product = products.find((product) => product.id === productId);
  // if (product.id === productId) {
  //   showInfo.value = true;
  // }
  // console.log(productId)
  // console.log(product.id)
  showInfo.value = true;
  moreInfo.value = product
};

const closeInfo = () => {
  showInfo.value = false;
};
</script>

<style scoped>
.container{
  background: transparent;
}
</style>
