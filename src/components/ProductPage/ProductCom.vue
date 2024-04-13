<template>
  <div className="product-component">
    <div>
      <h1>{{ meal.strMeal }}</h1>
      <em>{{ meal.strCategory }}</em>
      <br />
      <em>{{ meal.strArea }}</em>
      <p>{{ meal.strInstructions }}</p>
      <button @click="handleAddClick" className="save-food">
        <span></span> <p>Save Food</p>
      </button>
      <template v-if="loading">
        <h1 class="loading">Hold on, food is saving<span></span></h1>
      </template>
      <template v-if="success">
        <h1 className="success">
          Added Successfully 👍 <a href="/account">View now</a>
        </h1>
      </template>
      <template v-if="error">
        <h1 className="error">
          Login/signup to Account <a href="/account">Click here</a>
        </h1>
      </template>
    </div>
    <img
      className="mealimg"
      :src="meal.strMealThumb"
      width="500"
      :alt="meal.strMeal"
    />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "productComponent",
  props: ["meal"],
  data() {
    return {
      loading: false,
      success: false,
      error: false,
    };
  },
  methods: {
    handleAddClick() {
      this.loading = true;
      const token = localStorage.getItem("token");
      axios
        .post("https://foodapp-api-41m2.onrender.com/add", {
          token: token,
          mealId: this.meal.idMeal,
        })
        .then((res) => {
          this.loading = false;
          const message = res.data.message;
          if (message === "account not found") {
            this.error = true
          } else {
            this.success = true
          }
        })
        .catch((error) => {
          this.error = true;
          this.loading = false;
        });
    },
  },
};
</script>

<style scoped>
.product-component {
  display: grid;
  grid-template-columns: auto auto;
  grid-template-rows: auto;
  gap: 20px;
}
.product-component img {
  border-radius: 10px;
}
.product-component .save-food {
  position: relative;
  margin-top: 20px;
  padding: 10px;
  border-radius: 15px;
  overflow: hidden;
  background-color: transparent;
  cursor: pointer;
  border: 1px solid var(--color2);
  transition: 1500ms;
}
.product-component span {
  position: absolute;
  left: 0;
  top: 0;
  height: 0;
  width: 100%;
  background-color: #3a1a1a;
  transition: 1500ms;
  z-index: 2;
}
.product-component .save-food:hover {
  border: 2px solid var(--color2);
  color: var(--color1);
  border-radius: 5px;
}
.product-component .save-food:hover span {
  height: 100%;
}
.product-component .save-food:hover p {
  position: relative;
  z-index: 3;
  color: white;
}
span {
  height: 10px;
  width: 80px;
  display: block;
  background-color: var(--color3);
  animation: loading-span 1s ease-out infinite alternate;
}
@keyframes loading-span {
  from {
    width: 80px;
  }
  to {
    width: 200px;
  }
}
.product-component div .success {
  border: 2px solid rgb(12, 255, 12);
  background-color: rgb(67, 161, 67);
  padding: 10px;
  color: white;
  pointer-events: none;
  margin-top: 10px;
}
.product-component div .error {
  border: 2px solid rgb(252, 0, 0);
  background-color: rgb(196, 83, 83);
  padding: 10px;
  color: white;
  pointer-events: none;
  margin-top: 10px;
}
.product-component div .error a {
  pointer-events: all;
  color: black;
}
.product-component div .success a {
  pointer-events: all;
  color: black;
}
@media screen and (max-width: 674px) {
  .product-component img {
    width: 300px;
  }
}
@media screen and (max-width: 465px) {
  .product-component img {
    width: 50px;
  }
}
</style>