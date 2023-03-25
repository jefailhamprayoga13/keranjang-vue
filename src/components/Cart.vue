<template>
        <h1 class="text-2xl font-bold text-center">Keranjang</h1>
        <div class="p-5 rounded-lg bg-white shadow-lg m-2 flex" v-for="(item, index) in cart" :key="index">
            <div class="text-lg">
                <img :src="item.img">
                <h5>{{ item.name }}</h5>
                <p class="font-bold">Rp.{{ item.harga }}</p>
                    <input class="border-2 rounded-lg p-1 text-center" type="number"  name="quantity" min="1" :max="item.stok" value="1">
                    <br>
                    <button class="bg-red-600 text-white rounded-lg px-2 py-3 shadow-lg mt-2" @click="removeItem(index)">Hapus dari Keranjang</button>
            </div>
        </div>
</template>

<script>
export default {
    name: 'Cart',
    props: ['cart'],
    data(){
        return{
        };
    },
    methods: {
        removeItem(index) {
            this.cart.splice(index, 1);
            localStorage.setItem('cart', JSON.stringify(this.cart));
            this.$emit('update:cart', this.cart);
        },

    },
};
</script>
