<template>
  <h1>PLANTARIA</h1>
  <div class="mainPlant">
    <section>
      <h2>OUR PLANTS</h2>
      <div class="flex-container">
        <ItemsList
          v-for="items in itemsArray"
          :key="items.id"
          :id="items.id"
          :items="items"
          @itemon-cart="itemonCart"
        />
      </div>
    </section>

    <section class="cartClass">
      <shoppingCart
        :getitemsonCart="getitemsonCart"
        :id="getitemsonCart.id"
        @delete-item="deleteItem"
        @get-quantity="getQuantity"
      />
    </section>
  </div>
</template>

<script>
import ItemsList from "./components/ItemsList.vue";
import shoppingCart from "./components/shoppingCart.vue";
export default {
  components: {
    ItemsList,
    shoppingCart,
  },
  data() {
    return {
      itemsArray: [
        {
          id: 1,
          name: "PLANT1",
          src: require("../src/assets/plant1.jpg"),
          price: 100,
          updatedPrice: 100,
          quantityOfItem: 1,
          quantity: true,
        },
        {
          id: 2,
          name: "PLANT2",
          src: require("../src/assets/plant2.jpg"),
          price: 112,
          updatedPrice: 112,
          quantityOfItem: 1,
          quantity: true,
        },
        {
          id: 3,
          name: "PLANT3",
          src: require("../src/assets/plant3.jpg"),
          price: 150,
          updatedPrice: 150,
          quantityOfItem: 1,
          quantity: true,
        },
        {
          id: 4,
          name: "PLANT4",
          src: require("../src/assets/plant4.jpg"),
          price: 90,
          updatedPrice: 90,
          quantityOfItem: 1,
          quantity: true,
        },
      ],
      getitemsonCart: [],
      showcart: false,
      totalAmount: 0,
    };
  },

  methods: {
    itemonCart(item) {
      const itemIndex = this.getitemsonCart.findIndex(
        (element) => element.id === item.id
      );
      if (itemIndex >= 0) {
        this.getitemsonCart[itemIndex].quantityOfItem++;
        this.getitemsonCart[itemIndex].updatedPrice =
          this.getitemsonCart[itemIndex].price *
          this.getitemsonCart[itemIndex].quantityOfItem;
      } else {
        this.getitemsonCart.push(item);
      }
      console.log(item);
    },
    getQuantity(id) {
      const itemIndex = this.getitemsonCart.findIndex((item) => item.id === id);
      this.getitemsonCart[itemIndex].updatedPrice =
        this.getitemsonCart[itemIndex].price *
        this.getitemsonCart[itemIndex].quantityOfItem;
    },
    deleteItem(id) {
      // const itemIndex = this.getitemsonCart.findIndex((item) => item.id === id);
      // this.getitemsonCart.splice(itemIndex, 1);
      let index = this.getitemsonCart.indexOf(id);
      this.getitemsonCart.splice(index, 1);
    },
  },
};
</script>
<style>
* {
  padding: 0px;
  margin: 0 !important;
  box-sizing: border-box;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
h1 {
  padding: 20px;
  background-color: green;
  color: white;
  text-align: center;
}
.flex-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: calc(100vw - 1em);
}
.mainPlant {
  display: flex;
}
h2 {
  text-align: center;
}
.cartImage {
  width: 80px;
  height: 80px;
}
button {
  background-color: green;
  padding: 5px;
  color: white;
  border: none;
  margin: 10px 0px;
  cursor: pointer;
}
.cartClass {
  position: absolute;
  left: 67%;
  background-color: #000000e0;
  color: white;
  padding: 2px;
  text-align: center;
}
</style>
