<template>
  <div class="col-md-4 cart">
    <h2 class="mb-3">購物車</h2>
    <ul class="list-group mb-3">
      <li
        v-bind:key="id"
        v-for="cart in carts"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <div>
          <h6 class="my-0">{{ cart.title }}</h6>
          <small class="text-muted">數量：{{ cart.quantity }}</small>
        </div>
        <div>
          <span class="text-muted">${{ cart.quantity * cart.price }}</span>
          <button
            @click="deletBtn(cart)"
            class="btn btn-sm btn-outline-danger ms-2"
          >
            移除
          </button>
        </div>
      </li>
      <li
        v-if="sum"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <h6 class="my-1">總計:</h6>
        <div class="text-muted">${{ sum }}</div>
      </li>
      <li
        v-else
        class="list-group-item d-flex justify-content-between align-items-center err"
      >
        <h6 class="my-1">!!購物車沒有商品!!</h6>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { inject } from "vue";

const props = defineProps({
  carts: { type: Array },
  sum: { type: Number },
});
const emit = defineEmits(["delet-carts"]);
function deletBtn(item) {
  emit("delet-carts", item);
  enterNotify(`${item.title}已從購物車移除`);
}

const enterNotify = inject("enterNotify");
</script>

<style>
body {
  position: relative;
}

.cart {
  position: fixed;
  top: 50px;
  right: 0;
  background-color: lightgrey;
  box-shadow: 0 2px 5px 1px gray;
}

.err {
  border: 2px solid red;
  outline: 2px solid red;
  animation: err 1s ease infinite;
}

@keyframes err {
  0%,
  100% {
    outline-color: red;
  }
  50% {
    outline-color: transparent;
  }
}
</style>
