<template>
    <div>
      <h2>Product List</h2>
      <div v-for="product in products" :key="product.id" class="product">
        <h3>{{ product.name }}</h3>
        <p>{{ formatCurrency(product.price) }}</p>
        <div>
          <button @click="updateQuantity(product, product.quantity - 1)">-</button>
          <span>{{ product.quantity }}</span>
          <button @click="updateQuantity(product, product.quantity + 1)">+</button>
        </div>
        <button @click="addToCart(product)">Add to Cart</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      products: Array
    },
    methods: {
      updateQuantity(product, quantity) {
        if (quantity < 1) {
          quantity = 1;
        }
        product.quantity = quantity;
      },
      addToCart(product) {
        this.$emit('add-to-cart', product);
      },
      formatCurrency(value) {
        return `$${value.toFixed(2)}`;
      }
    }
  };
  </script>
  
  <style>
  .product {
    border: 1px solid #ddd;
    padding: 10px;
    margin-bottom: 10px;
  }
  </style>
  
  
  