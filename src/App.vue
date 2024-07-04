<template>
  <div id="app">
    <h1>Shopping Cart</h1>
    <ProductList :products="products" @add-to-cart="addToCart" />
    <ShoppingCart :cart="cart" @remove-from-cart="removeFromCart" @checkout="checkout" />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  name: 'App',
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Product 1', price: 10, quantity: 1 },
        { id: 2, name: 'Product 2', price: 20, quantity: 1 },
        { id: 3, name: 'Product 3', price: 30, quantity: 1 }
      ],
      cart: []
    };
  },
  created() {
    this.loadCart();
  },
  methods: {
    addToCart(product) {
      const cartItem = this.cart.find(item => item.product.id === product.id);
      if (cartItem) {
        cartItem.quantity += product.quantity;
      } else {
        this.cart.push({ product: { ...product }, quantity: product.quantity });
      }
      this.saveCart();
    },
    removeFromCart(product) {
      const index = this.cart.findIndex(item => item.product.id === product.id);
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
      this.saveCart();
    },
    checkout() {
      alert('Checkout not implemented');
    },
    saveCart() {
      localStorage.setItem('cart', JSON.stringify(this.cart));
    },
    loadCart() {
      const cart = localStorage.getItem('cart');
      if (cart) {
        this.cart = JSON.parse(cart);
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
