<template>
  <div>
    <!-- Product Listings -->
    <div class="product-list">
      <div v-for="product in products" :key="product.id" class="product">
        <p>{{ product.name }} - ₱{{ product.price }}</p>
        <button @click="addToCart(product)">Add to Cart</button>
      </div>

    </div>

    <!-- Shopping Cart -->
    <div class="cart">
      <h2>Shopping Cart</h2>
      <div v-if="cart.length === 0" class="empty-cart">Cart is empty</div>
      <div v-else>
        <div v-for="(item, index) in cart" :key="index" class="cart-item">
          <p>{{ item.product.name }} - ₱{{ item.product.price }} x {{ item.quantity }}</p>
          <button @click="removeFromCart(index)" class="remove-button">Remove</button>
          <input type="number" v-model="item.quantity" min="1" @input="updateQuantity(index)" class="quantity-input">
        </div>
        <p class="total-price">Total: ₱{{ totalPrice }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { id: 1, name: 'Adobo', price: 150 },
        { id: 2, name: 'Sinigang', price: 200 },
        { id: 3, name: 'Lechon Kawali', price: 250 },
        { id: 4, name: 'Kare-Kare', price: 180 },
        { id: 5, name: 'Pancit Palabok', price: 120 },
        { id: 6, name: 'Halo-Halo', price: 100 },
        { id: 7, name: 'Lumpiang Shanghai', price: 130 },
        { id: 8, name: 'Tapsilog', price: 90 },
        { id: 9, name: 'Chicken Adobo', price: 170 },
        { id: 10, name: 'Bangus Belly', price: 190 },
        { id: 11, name: 'Puto Bumbong', price: 80 },
        { id: 12, name: 'Tinolang Manok', price: 160 },
        { id: 13, name: 'Bicol Express', price: 210 },
        { id: 14, name: 'Ginataang Kalabasa', price: 140 },
        { id: 15, name: 'Crispy Pata', price: 280 },
        { id: 16, name: 'Sisig', price: 220 }
      ],
      cart: []
    };
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => {
        return total + item.product.price * item.quantity;
      }, 0);
    }
  },
  methods: {
    addToCart(product) {
      const found = this.cart.find(item => item.product.id === product.id);
      if (found) {
        found.quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index) {
      const quantity = parseInt(this.cart[index].quantity);
      if (quantity <= 0) {
        this.cart.splice(index, 1);
      }
    }
  }
};
</script>

<style scoped>
.product-list {
  display: flex;
  flex-wrap: wrap;
}

.product {
  margin: 9px;
  padding: 10px;
  border: 1px solid #1b3ac5;
}

.cart {
  margin-top: 10px;
  background-color: #ac111e;
  text-align: center;
  padding: 20px;
}

.cart-item {
  margin-bottom: 10px;
  border-bottom: 1px solid #fff;
  padding-bottom: 10px;
}

.remove-button {
  background-color: #fff;
  color: #f87a03;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

.quantity-input {
  margin-left: 10px;
  padding: 5px;
  width: 40px;
}

.empty-cart {
  color: #fff;
  font-style: italic;
}

.total-price {
  font-weight: bold;
  margin-top: 10px;
}
</style>
