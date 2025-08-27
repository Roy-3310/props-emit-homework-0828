<template>
  <div class="col-md-8">
    <h2 class="mb-3">商品列表</h2>
    <div class="row">
      <div v-for="product in props.products" class="col-md-4 mb-4">
        <div class="card h-100">
          <img :src="product.imgURL" />
          <div class="card-body">
            <h5 class="card-title">{{ product.title }}</h5>
            <p class="card-text">{{ product.describe }}</p>
            <p class="fw-bold text-primary">$ {{ product.price }}</p>
            <button @click="addBtn(product)" class="btn btn-success w-100">
              加入購物車
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { inject } from "vue";

const props = defineProps({
  products: { type: Array, required: true },
  carts: { type: Array },
});

const emit = defineEmits(["add-carts"]);
function addBtn(item) {
  emit("add-carts", item);
  enterNotify(`${item.title}已加入購物車`);
}

const enterNotify = inject("enterNotify");
</script>
