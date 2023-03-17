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
        items : [{ name: "Headphone", harga: 200000, stok: 25, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas" },
        { name: "Televisi", harga: 2000000, stok: 15, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas" },
        { name: "Kulkas", harga: 1500000, stok: 10, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas" },
        { name: "Laptop", harga: 7500000, stok: 5, deskripsi: "Barang murah sangat terjangkau dan sangat berkualitas" }],

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
  <div class="container-fluid">
    <div class="row">
        <h1 mb-2>Sistem Keranjang Sederhana</h1>
        <div class="col-6 items mx-2">
          <Items :items="items" :cart="cart" @add-cart="addCart"/>
        </div>
        <div class="col-5 cart mx-2">
          <Cart :cart="cart" @add-cart="addCart"/>
        </div>
      </div>
  </div>
</template>


