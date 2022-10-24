<template>
  <div class="pagination">
    <nav aria-label="Page navigation example">
      <ul class="pagination" v-if="tabs.length">
        <li class="page-item"><a class="page-link" href="#">Previous</a></li>
        <li 
          v-for="tab in tabs"
          :key = "tab.id"
          class="page-item"
          @click="changePage(tab.id)"
        >
          <div class="page-link" >{{ tab.id }}</div>
        </li>
        <li class="page-item"><a class="page-link" href="#">Next</a></li>
      </ul>
    </nav>
  </div>
</template>

<script setup>

import { ref, onBeforeMount, onMounted } from "vue";

const props = defineProps({
  products: {
    type: Array,
    default: [],
  },
});

const emit = defineEmits(['changePage'])

const tabs = ref([])

const showTabs = (productLenth) => {
  let maxTabs = Math.ceil(Number(productLenth / 10))
  for (let i = 1; i <= maxTabs; i++) {
    tabs.value.push({ id: i })
  }
}

const changePage = (id) => {
  emit('changePage', id)
}
onMounted(() => {
  showTabs(props.products.length)
})

</script>