<template>
    <div class="row card-items">
        <h1>Keranjang</h1>
        <div class="card col-12 mt-2" v-for="(item, index) in cart" :key="index">
            <div class="card-body">
                <h5 class="card-title">{{ item.name }}</h5>
                <p class="card-text">Rp.{{ item.harga }}</p>
                <form>
                    <input type="number"  name="quantity" min="1" :max="item.stok" value="1">
                </form>
                <button class="btn btn-danger mt-2" @click="removeItem(index)">Hapus dari Keranjang</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Cart',
    props: ['cart'],
    methods: {
        removeItem(index) {
            this.cart.splice(index, 1);
            localStorage.setItem('cart', JSON.stringify(this.cart));
            this.$emit('update:cart', this.cart);
        },
    },
};
</script>
