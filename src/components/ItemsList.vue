<template>
  <div class="item">
    <img :src="items.src" />
    <p>{{ items.name }}</p>
    <p>${{ items.price }}</p>
    <button @click="itemDetails">Add to Cart</button>
  </div>
</template>

<script>
export default {
  props: ["items", "id"],
  emits: ["itemon-cart"],
  methods: {
    itemDetails() {
      this.$emit("itemon-cart", this.items, this.id);
    },
  },
};
</script>
<style scoped>
body {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}
* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}
img {
  width: 327px;
  height: 367px;
  display: block;
  margin: 0px auto;
  margin-top: 10px;
}

.item {
  border: 1px solid gray;
  background-color: #363531;
  color: white;
  text-align: center;
  margin: 10px 0px;
  width: 335px;
}
h2 {
  text-align: center;
}
ul {
  list-style: none;
}
button {
  background-color: green;
  padding: 5px;
  color: white;
  border: none;
  margin: 10px 0px;
  cursor: pointer;
}
</style>
