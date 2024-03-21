<template>
    <div>
      <h1>Available Products</h1>
      <div v-if="showNotification" class="notification">
        {{ notificationMessage }}
      </div>
      <table class="product-table">
        <thead>
          <tr>
            <th class="product-name">Product Name</th>
            <th class="product-price">Product Price</th>
            <th class="product-actions">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in products" :key="product.id">
            <td>{{ product.name }}</td>
            <td>Php {{ product.price }}.00</td>
            <td>
              <button @click="addToCart(product)" class="add-to-cart-btn">
                <i class="fa fa-shopping-cart"></i> Add to Cart
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: ['products'],
    data() {
      return {
        showNotification: false,
        notificationMessage: ''
      };
    },
    methods: {
      addToCart(product) {
        this.notificationMessage = `${product.name} is added to cart`;
        this.showNotification = true;
  
        setTimeout(() => {
          this.showNotification = false;
        }, 3000);
        this.$emit('add-to-cart', product);
      }
    }
  };
  </script>
  
  <style scoped>
  .notification {
    background-color: #4CAF50; /* Light green */
    color: white;
    text-align: center;
    padding: 10px;
    margin-bottom: 10px;
  }
  
  .product-table {
    width: 100%;
    border-collapse: collapse;
  }
  
  .product-table th,
  .product-table td {
    padding: 12px;
    text-align: left;
    border: 1px solid #7ebc89; /* light green */
  }
  
  .product-table th {
    background-color: #7ebc89; 
    color: white; 
  }
  
  .product-name {
    width: 50%; 
  }
  
  .product-price {
    width: 30%; 
  }
  
  .product-actions {
    width: 20%; 
  }
  
  .add-to-cart-btn {
    background-color: #7ebc89; /* Light green pastel color */
    color: white;
    border: none;
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    transition-duration: 0.4s;
    cursor: pointer;
    border-radius: 8px;
    border: 1px solid #a0d1b0; /* light green */
  }
  
  .add-to-cart-btn i {
    margin-right: 5px; 
  }
  
  .add-to-cart-btn:hover {
    background-color: #5aa477; /* Dark green */
  }
  </style>
  