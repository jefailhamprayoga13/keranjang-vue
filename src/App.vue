<script>
import Items from "./components/Items.vue"
import Cart from "./components/Cart.vue"
import Swal from 'sweetalert2';

export default {
  name: 'App',
  components: {
    Items,
    Cart,
  },
  data() {
    return {
      items: [{ name: "Headphone", harga: 200000, stok: 25, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas", img: "../src/assets/img/headshet.png" },
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
      const existingItemIndex = this.cart.findIndex(cartItem => cartItem.name === item.name);
      if (existingItemIndex > -1) {
        this.cart[existingItemIndex].quantity++;
      } else {
        this.cart.push({ ...item, quantity: 1 });
      }
      localStorage.setItem('cart', JSON.stringify(this.cart));
      Swal.fire({
        icon: 'success',
        title: 'Barang berhasil ditambahkan ke keranjang',
        showConfirmButton: false,
        timer: 1500
      });
    },
  },


};
</script>

<template>
  <div class="p-10 max-w-md mx-auto bg-orange-200 my-20 min-w-fit rounded-xl shadow-lg ">
    <img src="./assets/img/cart.png" class=" mt-10 mx-auto block" alt="cart.png">
    <h1 class="text-center text-3xl mb-10 text-slate-700 font-bold ">Sistem Keranjang Sederhana</h1>
    <div class="md:flex ">
      <div class="p-5 m-2 bg-orange-300 rounded-xl shadow-lg items-center">
        <Items :items="items" :cart="cart" @add-cart="addCart" />
      </div>
      <div class="p-5 m-2 bg-orange-300 rounded-xl shadow-lg items-center ">
        <Cart :cart="cart" @add-cart="addCart" />
      </div>
    </div>
  </div>
</template>

