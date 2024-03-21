<template>
    <div>
      <h1>My Shopping Cart</h1>
      <div class="notification" v-if="showNotification">{{ notificationMessage }}</div>
      <table class="cart-table">
        <thead>
          <tr>
            <th>Product Name</th>
            <th>Product Price</th>
            <th>Quantity</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in cart" :key="index">
            <td>{{ item.product.name }}</td>
            <td>Php {{ item.product.price }}.00</td>
            <td>{{ item.quantity }}</td>
            <td>
              <button @click="removeFromCart(index)" class="cart-action-btn">
                <i class="fas fa-trash-alt"></i>
              </button>
              <button @click="increaseItem(index)" class="cart-action-btn">
                <i class="fas fa-plus"></i>
              </button>
              <button @click="decreaseItem(index)" class="cart-action-btn">
                <i class="fas fa-minus"></i>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: ['cart'],
    data() {
      return {
        showNotification: false,
        notificationMessage: ''
      };
    },
    methods: {
      removeFromCart(index) {
        this.$emit('remove-from-cart', index);
        this.showNotificationMessage('Item removed from cart');
      },
      increaseItem(index) {
        this.$emit('increase-item', index);
        this.showNotificationMessage('Item quantity increased');
      },
      decreaseItem(index) {
        this.$emit('decrease-item', index);
        this.showNotificationMessage('Item quantity decreased');
      },
      showNotificationMessage(message) {
        this.notificationMessage = message;
        this.showNotification = true;
        setTimeout(() => {
          this.hideNotification();
        }, 3000);
      },
      hideNotification() {
        this.showNotification = false;
        this.notificationMessage = '';
      }
    }
  };
  </script>
  
  <style scoped>
  /* column table */
  .cart-table {
    width: 100%;
    border-collapse: collapse;
  }
  
  /* table header */
  .cart-table th {
    background-color: #3d6f49; 
    color: white; 
    padding: 12px;
    text-align: left;
    border: 1px solid #3d6f49; /* dark green */
  }
  
  .cart-table td {
    padding: 12px;
    text-align: left;
    border: 1px solid #3d6f49; /* dark green */
  }

  .cart-action-btn {
  background-color: #3d6f49; /* dark green */
  color: white;
  border: none;
  padding: 6px 10px;
  margin-right: 5px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
  transition-duration: 0.4s;
}

.cart-action-btn i {
  font-size: 16px;
}

.cart-action-btn:hover {
  background-color: #2f5238; /* dark green */
}
  
.notification {
background-color: #4CAF50; /* Green */
color: white;
text-align: center;
padding: 10px;
margin-bottom: 15px;
border-radius: 5px;
}
</style>
  