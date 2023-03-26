<template>
    <h1 class="text-2xl font-bold text-center text-slate-800">Keranjang</h1>
    <div class="p-5 rounded-lg bg-orange-100 shadow-lg m-2 flex" v-for="(item, index) in cart" :key="index">
        <div class="text-lg">
            <img :src="item.img">
            <h5>{{ item.name }}</h5>
            <p class="font-bold">Rp.{{ item.harga }}</p>
            <button class="bg-gray-300 rounded-md px-2 py-1 mr-1 text-xl font-bold" @click="reduceQuantity(index)"><svg
                    xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-5 h-5 inline-block">
                    <path fill-rule="evenodd" d="M3.75 12a.75.75 0 01.75-.75h15a.75.75 0 010 1.5h-15a.75.75 0 01-.75-.75z"
                        clip-rule="evenodd" />
                </svg>
            </button>
            <input class="border-2 rounded-lg p-1 text-center" type="number" name="quantity"
                :value="item.quantity < item.stok ? item.quantity : item.stok" min="1" :max="item.stok" readonly>
            <button class="bg-gray-300 rounded-md px-2 py-1 ml-1 text-xl font-bold" @click="addQuantity(index)"><svg
                    xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-5 h-5 inline-block">
                    <path fill-rule="evenodd"
                        d="M12 3.75a.75.75 0 01.75.75v6.75h6.75a.75.75 0 010 1.5h-6.75v6.75a.75.75 0 01-1.5 0v-6.75H4.5a.75.75 0 010-1.5h6.75V4.5a.75.75 0 01.75-.75z"
                        clip-rule="evenodd" />
                </svg>
            </button>
            <br>
            <button class="bg-red-600 text-white rounded-lg px-2 py-3 shadow-lg mt-2 hover:bg-red-800 hover:ring-4 hover:ring-red-300" @click="removeItem(index)">Hapus dari
                Keranjang</button>
        </div>
    </div>
</template>

<script>
import Swal from 'sweetalert2';
export default {
    name: 'Cart',
    props: ['cart'],
    methods: {
        removeItem(index) {
            this.cart.splice(index, 1);
            localStorage.setItem('cart', JSON.stringify(this.cart));
            this.$emit('update:cart', this.cart);
            Swal.fire({
                icon: 'success',
                title: 'Barang berhasil dihapus dari keranjang',
                showConfirmButton: false,
                timer: 1500
            });
        },
        addQuantity(index) {
            const quant = this.cart[index];
            if (quant.quantity <= quant.stok) {
                this.cart[index].quantity++;
            }
        },
        reduceQuantity(index) {
            const quant = this.cart[index];
            if (quant.quantity > 1) {
                this.cart[index].quantity--;
            }
        },
    },
};
</script>
