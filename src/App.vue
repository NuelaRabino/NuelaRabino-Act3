<template>
  <div>
    <div class="add-product-container">
      <h2>Add Product:</h2>
      <div class="input-container">
        <input type="text" v-model="newProductName" placeholder="Product Name" class="input-field">
      </div>
      <div class="input-container">
        <input type="number" v-model="newProductPrice" placeholder="Price" class="input-field">
      </div>
      <button @click="addProduct" class="add-product-btn">Create</button>
    </div>

    <product-list :products="products" @add-to-cart="addToCart"></product-list>

    <shopping-cart :cart="cart" @remove-from-cart="removeFromCart" @increase-item="increaseItem" @decrease-item="decreaseItem"></shopping-cart>

    <p>______________________________</p>
    <p>Total: Php {{ total }}.00</p>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Huawei MateBook D 16', price: 68999 },
        { id: 2, name: 'Glorious Model D Gaming Mouse', price: 2590 },
        { id: 3, name: 'Logitech MX Keys Keyboard', price: 5950 },
        { id: 4, name: 'SAMSUNG 27" LS27C330GAEXXP IPS Monitor', price: 7770 },
        { id: 5, name: 'Logitech H390 Headphones', price: 1341 },
        { id: 6, name: 'Black Mouse Pad', price: 150 },
        { id: 7, name: 'Logitech Z213 Multimedia Speaker', price: 1999 },
        { id: 8, name: 'Clip Mic Black', price: 108 },
        { id: 9, name: 'Serenzo Blower Fan Air', price: 3999 },
        { id: 10, name: 'Lenovo Laptop Charger 20V 3.25A Usb Type', price: 6999 }
      ],
      cart: [],
      newProductName: '',
      newProductPrice: ''
    };
  },
  computed: {
    total() {
      return this.cart.reduce((acc, item) => acc + (item.product.price * item.quantity), 0);
    }
  },
  methods: {
    addProduct() {
      const name = this.newProductName.trim();
      const price = parseFloat(this.newProductPrice);
      
      if (name && price > 0) {
        const newProduct = {
          id: this.products.length + 1,
          name: name,
          price: price
        };
        this.products.push(newProduct);
        this.newProductName = '';
        this.newProductPrice = '';
      }
    },
    addToCart(product) {
      const index = this.cart.findIndex(item => item.product.id === product.id);
      if (index !== -1) {
        this.cart[index].quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    increaseItem(index) {
      this.cart[index].quantity++;
    },
    decreaseItem(index) {
      if (this.cart[index].quantity > 1) {
        this.cart[index].quantity--;
      }
    }
  }
};
</script>

<style scoped>
.add-product-container {
  text-align: center;
  margin-bottom: 20px;
}

.input-container {
  margin-bottom: 10px;
}

.input-field {
  padding: 10px;
  border: 2px solid #3d6f49; /*dark green */
  border-radius: 4px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}

.add-product-btn {
  background-color: #3d6f49; /*dark green */
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
  transition-duration: 0.4s;
}

.add-product-btn:hover {
  background-color: #2f5238; /*dark green */
}
</style>
