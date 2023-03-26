<template>
    <h2 class="text-2xl font-bold text-center text-slate-800">Daftar Barang</h2>
    <div class="p-5 rounded-lg bg-orange-100 shadow-lg m-2 flex" v-for="(item, index) in items" :key="index">
        <div class="text-lg ">
            <img :src="item.img">
            <h5>{{ item.name }}</h5>
            <p class="font-bold">Rp.{{ item.harga }}</p>
            <p>{{ item.deskripsi }}</p>
            <button class="bg-green-600 text-white rounded-lg px-2 py-3 shadow-lg hover:bg-green-800 hover:ring-4 hover:ring-green-300" @click="addCart(index)">+ Keranjang</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Items',
    props: ['items', 'cart'],
    data() {
        return {
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
        addCart(index) {
            const item = this.items[index];
            this.$emit('add-cart', item);
        },



    },
};
</script>

<style></style>