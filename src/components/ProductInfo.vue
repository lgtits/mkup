<template>
  <div id="show-product-modal" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="exampleModalLongTitle" aria-hidden="true">
      <div class="modal-dialog modal-lg" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="show-product-title">{{moreInfo.name}}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">×</span>
            </button>
          </div>
          <div class="modal-body" id="show-product-body">
            <div class="row">
              <img class="col-sm-8" id="show-product-image" :src="moreInfo.image_link">
              <div class="col-sm-4">
                <p><em id="show-product-date">price : $ {{moreInfo.price}}{{moreInfo.currency}}</em></p>
                <p id="show-product-description">{{moreInfo.description}}</p>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
</template>

<script setup>

const props = defineProps({
  // product: {
  //   type:Object,
  //   default:{},
  // } 
  //  products: {
  //   type:Array,
  //   default:[],
  // } 
  moreInfo: {
    type:Object,
    default:{},
  } 
})



</script>

