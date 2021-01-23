<template>
  <h1 class="myCart" @click="openCart">{{ countItems }}</h1>

  <table v-if="showCart">
    <tr>
      <!-- <th>Item Image</th> -->
      <th>Item</th>
      <th>Price</th>
      <th>Quantity</th>
      <th colspan="7">
        <button @click="closeCart" class="closeCart">x</button>
      </th>
    </tr>

    <tr v-for="getitemonCart in getitemsonCart" :key="getitemonCart.id">
      <td>
        <img class="cartImage" :src="getitemonCart.src" />
        {{ getitemonCart.name }}
      </td>
      <td>${{ getitemonCart.updatedPrice }}</td>
      <td>
        <input
          type="number"
          v-model="getitemonCart.quantityOfItem"
          @input="QuantityOftheItem(getitemonCart)"
          min="1"
        />
      </td>
      <td>
        <button @click="deleteItemonCart(getitemonCart)">Delete</button>
      </td>
    </tr>
    <tr>
      <td>Total:</td>
      <td>{{ getTotalAmount }}$</td>
    </tr>
    <tr>
      <td colspan="4">
        <button @click="checkOut" class="checkoutBtn">Check Out</button>
      </td>
    </tr>
  </table>
</template>

<script>
export default {
  props: ["getitemsonCart", "id"],
  emits: ["delete-item", "get-quantity"],
  data() {
    return {
      showCart: false,
      count: 0,
    };
  },
  computed: {
    getTotalAmount() {
      let total = 0;
      this.getitemsonCart.forEach((element) => {
        total += element.updatedPrice;
      });
      return total;
      // return this.getitemsonCart((acc, item) => acc + item.updatedPrice, 0);
    },
    countItems() {
      return this.getitemsonCart.length;
    },
  },
  methods: {
    QuantityOftheItem(getitemonCart) {
      this.$emit("get-quantity", getitemonCart.id);
    },
    deleteItemonCart(getitemonCart) {
      this.$emit("delete-item", getitemonCart.id);
    },
    openCart() {
      if (this.getitemsonCart.length === 0) {
        alert("Your Cart is Empty");
        this.showCart = false;
        return;
      }
      this.showCart = !this.showCart;
    },
    closeCart() {
      this.showCart = false;
    },
    checkOut() {
      if (this.getitemsonCart.length === 0) {
        return;
      }
      alert("Your order has been placed...Thanks for the shopping...");
    },
  },
};
</script>
<style scoped>
th {
  border-bottom: 1px solid white;
  width: 60px;
}
tr {
  border-bottom: 1px solid white;
}
table {
  /* width: 50%; */
  text-align: center;
  border-collapse: collapse;
}
input {
  width: 30px;
}
.myCart {
  padding: 10px;
  background-color: #000000c7;
  color: white;
  text-align: center;
  position: absolute;
  top: -70px;
  cursor: pointer;
}
.closeCart {
  padding: 5px;
  font-size: 20px;
  cursor: pointer;
}
</style>
