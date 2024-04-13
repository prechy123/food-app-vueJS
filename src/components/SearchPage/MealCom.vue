<template>
  <a :href="url">
    <div className="search-component">
      <div className="search-img-d">
        <div className="search-img">
          <img :src="meal.strMealThumb" :alt="meal.strMeal" />
        </div>
        <h2>{{ meal.strMeal }}</h2>
      </div>
    </div>
  </a>
</template>

<script>
export default {
  name: "MealCom",
  data() {
    return {
        url: ''
    }
  },
  props: {
    meal: Object,
  },
  mounted() {
    this.url = "/product/" + this.meal.idMeal;
  }
};
</script>

<style scoped>
.search-component .search-img-d {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.search-component .search-img-d .search-img img {
  border-radius: 10px;
  width: 100px;
  height: 100px;
  background-color: var(--color1);
}
.search-component .search-img-d h2 {
  background-color: var(--color3);
  color: var(--color1);
  border-radius: 10px;
  padding: 10px;
}
</style>