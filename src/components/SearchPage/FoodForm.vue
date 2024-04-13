<template>
  <form @submit.prevent="handleSubmit">
    <div className="inputs">
      <div className="input-text">
        <input
          type="text"
          name="foodName"
          className="search-bar"
          required
          v-model="foodName"
        />
        <span>Enter food</span>
      </div>
      <div className="submit">
        <input type="submit" value="Search" className="submit" />
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "FoodForm",
  data() {
    return {
        foodName: ""
    }
  },
  methods: {
    handleSubmit() {
        this.$emit('formSubmitted', this.foodName)
        this.foodName = ""
    }
  }
};
</script>

<style scoped>
#search-page form {
  background-color: var(--color1);
  width: 40%;
  height: 16vh;
  border-radius: 0 0 10px 10px;
  padding-bottom: 10px;
}
#search-page form .inputs {
  display: grid;
  place-items: center;
  margin-top: 20px;
}
#search-page form .input-text {
  position: relative;
}
#search-page form .input-text input {
  width: 250px;
  height: 30px;
  padding: 5px;
  outline: none;
  border: 1px solid black;
  border-radius: 10px;
}
#search-page form .input-text span {
  position: absolute;
  left: 0;
  padding: 5px;
  pointer-events: none;
  transition: 0.75s;
}
#search-page form .inputs .input-text input:valid ~ span,
#search-page form .inputs .input-text input:focus ~ span {
  color: var(--color3);
  transform: translateX(8px) translateY(-12px);
  padding: 0 10px;
  background-color: var(--color1);
  letter-spacing: 0.1rem;
  border-left: 2px solid var(--color3);
  border-right: 2px solid var(--color3);
}
#search-page form .submit {
  margin-top: 2px;
  padding: 5px 10px;
  background-color: transparent;
  border-radius: 10px;
  cursor: pointer;
  transition: 500ms;
}
#search-page form .submit:hover {
  border-radius: 5px;
}
@media screen and (max-width: 674px) {
  #search-page form .input-text input {
    width: 80%;
  }
}
</style>