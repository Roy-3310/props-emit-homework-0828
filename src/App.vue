<template>
  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 -->
      <ProductList :products="products" @add-carts="addCarts" />

      <!-- 購物車區 -->
      <Cart class="cart" :carts="carts" :sum="sum" @delet-carts="deletCarts" />
    </div>

    <!-- 通知元件 -->

    <NotificationMessage />
  </div>
</template>
<script setup>
import ProductList from "./components/icons/ProductList.vue";
import Cart from "./components/icons/Cart.vue";
import NotificationMessage from "./components/icons/NotificationMessage.vue";
import { computed, provide, reactive, ref } from "vue";

const products = ref([
  {
    id: "p01",
    title: "耳罩式藍牙耳機",
    describe: "舒適配戴，支援降噪技術",
    price: "2490",
    imgURL:
      "https://plus.unsplash.com/premium_photo-1678066730788-fdc6d64b4679?q=80&w=1332&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p02",
    title: "真無線藍牙耳機",
    describe: "小巧輕便，長效電池續航",
    price: "1990",
    imgURL:
      "https://images.unsplash.com/photo-1612116454817-2b0841e30eaf?q=80&w=1244&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p03",
    title: "降噪無線耳機",
    describe: "專業主動降噪，沉浸式體驗",
    price: "3290",
    imgURL:
      "https://images.unsplash.com/photo-1655628143563-a4b1c60de33d?q=80&w=1332&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p04",
    title: "運動型耳機",
    describe: "防水抗汗，運動專用",
    price: "1490",
    imgURL:
      "https://plus.unsplash.com/premium_photo-1679913792954-6a5a93ae4cff?q=80&w=784&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p05",
    title: "頭戴式高音質耳機",
    describe: "立體環繞音效，適合音樂愛好者",
    price: "4590",
    imgURL:
      "https://images.unsplash.com/photo-1655628143766-172ca2198096?q=80&w=1332&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p06",
    title: "電競耳機（有麥克風）",
    describe: "遊戲專用，清晰語音與低延遲",
    price: "2990",
    imgURL:
      "https://images.unsplash.com/photo-1533575349875-5f372f88e25b?q=80&w=689&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p07",
    title: "入耳式降噪耳機",
    describe: "入耳封閉式，音場集中",
    price: "1290",
    imgURL:
      "https://images.unsplash.com/photo-1688561075097-0db5a6bc8eaa?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p08",
    title: "高解析藍牙耳機",
    describe: "支援高解析音訊編碼",
    price: "3790",
    imgURL:
      "https://images.unsplash.com/photo-1673854624483-3e26b2a4dc25?q=80&w=880&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p09",
    title: "可折疊便攜耳機",
    describe: "折疊設計，收納方便",
    price: "2290",
    imgURL:
      "https://www.syf.com.tw/images/202001/source_img/14718_58JN-0009-YK_7.jpg",
  },
  {
    id: "p10",
    title: "金屬質感耳機",
    describe: "鋁合金外殼，時尚耐用",
    price: "1890",
    imgURL:
      "https://plus.unsplash.com/premium_photo-1679865289918-b21aae5a9559?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p11",
    title: "耳掛式運動耳機",
    describe: "穩固不掉落，跑步首選",
    price: "1590",
    imgURL:
      "https://images.unsplash.com/photo-1611805913511-2ae08657b636?q=80&w=1157&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p12",
    title: "錄音室專業耳機",
    describe: "監聽級，頻率響應平直",
    price: "4990",
    imgURL:
      "https://media.istockphoto.com/id/1285338543/photo/wired-headphones-for-listening-to-music-on-a-white-wooden-background-concept-to-illustrate.jpg?s=2048x2048&w=is&k=20&c=L2savbHkmsvjgILNNlS0nkQZNLfht41GKZLIVewfPE4=",
  },
  {
    id: "p13",
    title: "智慧語音耳機",
    describe: "內建語音助理與觸控操作",
    price: "2690",
    imgURL:
      "https://images.unsplash.com/photo-1633329102202-eaa697179563?q=80&w=627&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p14",
    title: "皮革包覆耳機",
    describe: "質感皮革耳墊，舒適透氣",
    price: "3890",
    imgURL:
      "https://plus.unsplash.com/premium_photo-1680124607783-b99d86ed3015?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p15",
    title: "多點連線藍牙耳機",
    describe: "同時配對多台裝置，切換順暢",
    price: "3190",
    imgURL:
      "https://plus.unsplash.com/premium_photo-1706561441108-8d4be241fdc0?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p16",
    title: "復古風頭戴耳機",
    describe: "經典造型，懷舊音色",
    price: "2790",
    imgURL:
      "https://images.unsplash.com/photo-1677086852955-83f5942cae8a?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p17",
    title: "快充無線耳機",
    describe: "快速充電設計，臨時補電超方便",
    price: "2090",
    imgURL:
      "https://plus.unsplash.com/premium_photo-1701816071651-e0e1cf31e1d4?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p18",
    title: "輕量化藍牙耳機",
    describe: "僅重150g，久戴無負擔",
    price: "1890",
    imgURL:
      "https://images.unsplash.com/photo-1738694179762-9edf07a3c721?q=80&w=627&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p19",
    title: "DJ 專業耳機",
    describe: "可單耳監聽，耐用設計",
    price: "4590",
    imgURL:
      "https://images.unsplash.com/photo-1651435866499-d9538767a36e?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
  {
    id: "p20",
    title: "智慧感應耳機",
    describe: "摘下自動暫停/戴上自動播放",
    price: "2390",
    imgURL:
      "https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
  },
]);

const carts = ref([]);

const addCarts = (product) => {
  const existProduct = carts.value.find((item) => item.id === product.id);
  if (existProduct) existProduct.quantity++;
  else carts.value.push({ ...product, quantity: 1 });
};

const deletCarts = (product) => {
  carts.value = carts.value.filter((item) => item.id !== product.id);
};

const sum = computed(() =>
  carts.value.reduce((total, cart) => total + cart.price * cart.quantity, 0)
);

//使用 provide, inject
const notify = reactive({
  message: "",
  isAppear: false,
});
const enterNotify = (message) => {
  notify.message = message;
  notify.isAppear = true;

  setTimeout(() => {
    notify.isAppear = false;
  }, 2000);
};

provide("notify", notify);
provide("enterNotify", enterNotify);
</script>
