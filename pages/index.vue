<template>
  <!-- Ürünler -->
  <div class="app">
    <div class="product-container">
      <div class="baslik1">
        <p>Ürünler</p>
      </div>
      <div v-for="ürün in ürünler" :key="ürün.id" class="product">
        <p>{{ ürün.name }} - ${{ ürün.price }}</p>
        <p><img :src="require('@/assets/' + ürün.image)" :alt="ürün.name" style="width: 100px; height: auto;"></p>
        <button class="ürünbuton" @click="addToCart(ürün)">Sepete Ekle</button>
      </div>
    </div>
    <div>
        <!-- Sepet -->
        <div class="sepet">
          <h2>Sepetim</h2>
          <ul>
            <li class="sepetim" v-for="item in cart" :key="item.id">
              {{ item.name }} - ${{ item.price }}
              <button class="sepetbuton" @click="removeFromCart(item)">Kaldır</button>
            </li>
          </ul>
          <p class="sepetfiyat">Tutar: ${{ total }}</p>
        </div>
      </div>
    </div>
</template>

<script>
import '@/pages/style.css'; 

export default {
  data() {
    return {
      ürünler: [
        { id: 1, name: 'Fender American Professional II Telecaster Rosewood - Dark Night Elektro Gitar', price: 300, image: 'ürün1.jpeg' },
        { id: 2, name: 'Marshall Code50 1x12” 50w Dijital Kombo Elektro Gitar Amfisi', price: 600, image: 'ürün2.jpeg' },
        { id: 3, name: 'Iphone 13', price: 1000, image: 'ürün3.jpeg' },
        { id: 3, name: 'LG TV', price: 2000, image: 'ürün4.jpeg' }
      ],
      cart: []
    };
  },
  computed: {
    total() {
      return this.cart.reduce((acc, item) => acc + item.price, 0);
    }
  },
  methods: {
    addToCart(ürün) {
      this.cart.push(ürün);
    },
    removeFromCart(item) {
      const index = this.cart.indexOf(item);
      if (index > -1) {
        this.cart.splice(index, 1);
      }
    }
  }
};
</script>
