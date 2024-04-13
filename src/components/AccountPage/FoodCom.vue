<template>
  <div className="content-container-child" v-if="food">
    <a :href="url">
      <div className="img">
        <img :src="food.strMealThumb" :alt="food.strMeal" />
      </div>
      <p>{{ food.strCategory }}</p>
      <h1>{{ food.strMeal }}</h1>
      <p>{{ formatedDate() }}</p>
    </a>
    <button @click="handleDelete"><span></span>Delete</button>
  </div>
</template>

<script>
import { formatDistanceToNow } from "date-fns";
import axios from "axios"
export default {
  name: "FoodCom",
  props: ["foodId", "time"],
  data() {
    return {
      food: [],
      url: "",
    };
  },
  methods: {
    handleDelete() {
      this.$emit("deleteFood", this.foodId);
    },
    formatedDate() {
      return formatDistanceToNow(new Date(this.time), { addSuffix: true });
    },
  },
  mounted() {
    axios
      .get(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${this.foodId}`)
      .then((res) => {
        this.food = res.data.meals[0];
      });
    this.url = `/product/${this.foodId}`;
  },
};
</script>

<style scoped>
a {
  text-decoration: none;
}

.content-container-child {
  display: flex;
  flex-direction: column;
  gap: 10px;
  
}
.content-container-child h1 {
  background-color: var(--color1);
  color: white;
  padding: 10px;
  border-radius: 10px;
}
.content-container-child p {
  color: black;
}
.content-container-child .img {
  width: 100%;
  height: 80px;
  /* background-color: var(--color1); */
  display: flex;
  justify-content: space-between;
  align-items: last baseline;
}
.content-container-child img {
  border-radius: 20px;
  width: 80px;
}
.content-container-child button {
  width: 90px;
  height: 30px;
  background-color: transparent;
  border: 1px solid red;
  border-radius: 20px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
}
.content-container-child button span {
  position: absolute;
  width: 100%;
  height: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background-color: rgb(190, 94, 94);
  transition: height 1s ease;
}
.content-container-child button:hover span {
  height: 100%;
}
</style>