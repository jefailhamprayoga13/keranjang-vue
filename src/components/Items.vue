<template>
    <div class="row card-items">
        <h2>Daftar Barang</h2>
        <div class="card col-5 me-2 mt-2 " v-for="(item,index) in items" :key="index">
                <div class="card-body">
                    <h5 class="card-title">{{ item.name }}</h5>
                    <p class="card-text">{{ item.harga }}</p>
                    <p class="card-text">{{ item.deskripsi }}</p>
                    <button class="btn btn-primary" @click="addCart(index)">+ Keranjang</button>
                </div>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'Items',
        props: ['items', 'cart'],
        data(){
            return{
                cart : [],
            };
        },

        mounted() {
        const storedCart = localStorage.getItem('cart');
        if (storedCart) {
            this.cart = JSON.parse(storedCart);
        }
    },

        methods : {
            addCart(index){
                const item = this.items[index];
                this.$emit('add-cart', item);
            },

            
            
        },
    };
</script>

<style>

</style>