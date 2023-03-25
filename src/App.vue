<script>
import Items from "./components/Items.vue"
import Cart from "./components/Cart.vue"

export default {
  name: 'App',
  components: {
    Items,
    Cart,
  },
  data() {
    return {
      items: [{ name: "Headphone", harga: 200000, stok: 25, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas", img:"../src/assets/img/headshet.png" },
      { name: "Televisi", harga: 2000000, stok: 15, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas", img: "../src/assets/img/tv.png" },
      { name: "Kulkas", harga: 1500000, stok: 10, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas", img: "../src/assets/img/kulkas.png" },
      { name: "Laptop", harga: 7500000, stok: 5, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas", img: "../src/assets/img/laptop.png" }],

      cart: [],
    };
  },

    mounted() {
    const storedCart = localStorage.getItem('cart');
    if (storedCart) {
      this.cart = JSON.parse(storedCart);
    }
  },
  
  methods: {
    addCart(item) {
      this.cart = [...this.cart, item];
      localStorage.setItem('cart', JSON.stringify(this.cart));
    },
  },

};
</script>

<template>
  <div class="p-10 max-w-md mx-auto my-20 min-w-fit  bg-white rounded-xl shadow-lg  font-serif">
    <h1 class="text-center my-10 text-3xl font-bold">Sistem Keranjang Sederhana</h1>
    <div class="md:flex ">
      <div class="p-5 m-2 bg-white rounded-xl shadow-lg items-center">
        <Items :items="items" :cart="cart" @add-cart="addCart" />
      </div>
      <div class="p-5 m-2 bg-white rounded-xl shadow-lg items-center ">
        <Cart :cart="cart" @add-cart="addCart" />
      </div>
    </div>
  </div>
</template>


