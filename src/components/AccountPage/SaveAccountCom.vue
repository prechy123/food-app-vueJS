<template>
  <section id="saved-content">
    <div className="content-container" v-if="foods.length > 0">
      <template v-for="food in foods" :key="food.stringValue">
        <FoodCom
          :foodId="food.stringValue"
          :time="food.timeStampValue"
          @deleteFood="handleDeleteFood"
        />
      </template>
    </div>
    <div className="log-out">
      <a href="/account" @click="handleOnClickLogOut">
        <span></span>
        Log-Out
      </a>
    </div>
  </section>
</template>

<script>
import axios from "axios";
import FoodCom from "./FoodCom.vue";
export default {
  components: { FoodCom },
  data() {
    return {
      foods: [],
      userId: "",
    };
  },
  methods: {
    handleOnClickLogOut() {
      localStorage.removeItem("token");
    },
    handleDeleteFood(foodId) {
      const selectedFoodId = parseInt(foodId);
      this.foods = this.foods.filter(
        (food) => food.stringValue !== selectedFoodId
      );
      axios.post("https://foodapp-api-41m2.onrender.com/delete", {
        selectedFoodId,
        userId: this.userId,
      });
    },
  },
  mounted() {
    const tokenData = localStorage.getItem("token");
    const userId = JSON.parse(atob(tokenData.split(".")[1])).userId;
    this.userId = userId;
    axios
      .get("https://foodapp-api-41m2.onrender.com/getFoods", {
        params: {
          userId,
        },
      })
      .then((res) => {
        this.foods = res.data.foods;
      });
  },
};
</script>

<style scoped>
#saved-content {
  width: 100vw;
  width: 100dvw;
  height: calc(100vh - 144px);
  height: calc(100dvh - 144px);
  padding: 20px;
  overflow-y: scroll;
  background-color: var(--color3);
  position: relative;
}
#saved-content .log-out {
  position: absolute;
  top: 20px;
  right: 20px;
}
#saved-content .log-out a {
  text-decoration: none;
  background-color: transparent;
  border: 1px solid red;
  padding: 10px;
  color: black;
  position: relative;
  z-index: 3;
}
#saved-content .log-out a span {
  position: absolute;
  width: 100%;
  height: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background-color: rgb(190, 94, 94);
  transition: height 1s ease;
}
#saved-content .log-out a:hover span {
  height: 100%;
}
#saved-content .content-container {
  width: 100%;
  overflow-y: scroll;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}
</style>