<template>
    <div>
      <h2>Shopping Cart</h2>
      <div v-if="cart.length === 0">Your cart is empty</div>
      <div v-else>
        <div v-for="item in cart" :key="item.product.id" class="cart-item">
          <h3>{{ item.product.name }}</h3>
          <p>{{ formatCurrency(item.product.price) }} x {{ item.quantity }}</p>
          <p>Total: {{ formatCurrency(item.product.price * item.quantity) }}</p>
          <button @click="removeFromCart(item.product)">Remove</button>
        </div>
      </div>
      <h3>Total: {{ formatCurrency(totalPrice) }}</h3>
        <button @click="checkout">Checkout</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cart: Array
    },
    computed: {
      totalPrice() {
        return this.cart.reduce((total, item) => total + item.product.price * item.quantity, 0);
      }
    },
    methods: {
      removeFromCart(product) {
        this.$emit('remove-from-cart', product);
      },
      checkout() {
        this.$emit('checkout');
      },
      formatCurrency(value) {
        return `$${value.toFixed(2)}`;
      }
    }
  };
  </script>
  
  <style>
  .cart-item {
    border: 1px solid #ddd;
    padding: 10px;
    margin-bottom: 10px;
  }
  </style>
  
  