<template>
  <section id="search-page">
    <div>
      <FoodForm @formSubmitted="handleFormSubmitted" />
      <div className="component">
        <template v-if="loading">Loading...</template>
        <template v-if="errorMessage">{{ errorMessage }}</template>
        <template v-if="mealsArray">
          <template v-for="meal in mealsArray" :key="meal.idMeal">
            <MealCom :meal="meal" />
          </template>
        </template>
      </div>
    </div>
  </section>
</template>

<script>
import FoodForm from "@/components/SearchPage/FoodForm.vue";
import axios from "axios";
import MealCom from "@/components/SearchPage/MealCom.vue";
export default {
  components: { FoodForm, MealCom },
  name: "SearchView",
  data() {
    return {
      foodName: "",
      mealsArray: [],
      loading: false,
      errorMessage: "",
    };
  },
  methods: {
    handleFormSubmitted(data) {
      this.foodName = data;
    },
  },
  watch: {
    foodName(newFood) {
      this.loading = true;
      axios
        .get("https://www.themealdb.com/api/json/v1/1/search.php?s=" + newFood)
        .then((res) => {
          this.loading = false;
          this.mealsArray = [...res.data.meals];
        })
        .catch(() => {
          this.loading = false;
          this.errorMessage =
            "Out food database is limited try another. Try something simpler e.g chicken, rice, e.t.c.";
        });
    },
  },
};
</script>

<style scoped>
#search-page {
  width: 100vw;
  width: 100dvw;
  height: calc(100vh - 144px);
  height: calc(100dvh - 144px);
  background-color: var(--color3);
}
#search-page div {
  display: flex;
  flex-direction: column;
  align-items: center;
}
#search-page .component {
  width: 100%;
  height: calc(100vh - 240px);
  /* width: 100dvw; */
  /* height: auto; */
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  overflow-y: scroll;
  padding: 20px;
}
#search-page .component a {
  text-decoration: none;
  color: white;
}
#search-page .component:hover > *:not(:hover) {
  transition: filter 5s ease-in-out;
  filter: grayscale(50%);
}

@media screen and (max-width: 674px) {
  #search-page form .input-text input {
    width: 80%;
  }
  #search-page .component {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
}
</style>