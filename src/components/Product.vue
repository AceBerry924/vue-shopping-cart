<template>
  <div class="w-full">
    <div class="flex">
      <div class="w-1/3 text-xs text-gray-400 lg:w-9/20">
        <figure class="flex flex-col lg:flex-row lg:items-center flex-nowrap">
          <div class="grid mb-2 border border-gray-300 rounded lg:mb-0 lg:mr-4 w-18 h-18">
            <img
              class="object-cover w-full h-full"
              :src="require('@/assets/images/' + imageUrl + '')"
              alt="item-avatar"
            />
          </div>
          <div>
            <h2 class="text-base font-bold text-indigo-600 normal-case">{{ title }}</h2>
            <p class="tracking-wide">Product code: {{ code }}</p>
          </div>
        </figure>
      </div>

      <div class="flex items-center justify-center w-3/12 text-xs text-gray-400 uppercase lg:w-1/5">
        <button
          @click="removeFromCart(code)"
          class="h-10 px-2 text-xl font-extrabold text-indigo-600 border-0 focus:outline-none"
        >
          -
        </button>
        <input
          class="w-10 h-10 px-3 py-2 text-sm leading-tight text-center text-gray-700 border rounded appearance-none focus:outline-none focus:shadow-outline"
          type="text"
          :value="productQuantity(code)"
        />
        <button
          @click="addToCart(code)"
          class="h-10 px-2 text-xl font-extrabold text-indigo-600 border-0 focus:outline-none"
        >
          +
        </button>
      </div>

      <div class="flex items-center justify-center w-3/12 text-xs text-gray-400 uppercase lg:w-1/5">
        <span class="text-base text-black">
          {{ currency(parseFloat(price)) }}
        </span>
      </div>

      <div class="flex items-center justify-center w-1/6 text-xs text-gray-400 uppercase lg:w-3/10">
        <span class="text-base text-black">
          {{ currency(price * productQuantity(code)) }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import { currency } from '@/utils/currency';
import { mapState, mapGetters, mapActions } from 'vuex';

export default {
  name: 'product',
  props: {
    code: String,
    title: String,
    price: String,
    imageUrl: String,
  },
  computed: {
    ...mapState(['cart', 'products']),
    ...mapGetters(['productQuantity']),
  },
  methods: {
    ...mapActions(['addToCart', 'removeFromCart']),
  },
  setup() {
    return {
      currency,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
