<template>
  <footer>
    <div className="img">
      <a href="https://www.instagram.com/prec__hy/"
        ><img :src="facebook" alt="facebook" width=30
      /></a>
      <a href="https://github.com/prechy123"
        ><img :src="github" alt="github" width=30
      /></a>
      <a href="https://www.instagram.com/prec__hy/"
        ><img :src="instagram" alt="instagram" width=30
      /></a>
      <a href="https://www.instagram.com/prec__hy/"
        ><img :src="linkedin" alt="linkedin" width=30
      /></a>
    </div>
    <div>
      <p>Bamidele Precious - {{date()}}</p>
    </div>
  </footer>
</template>

<script>
import facebook from "../assets/facebook.png";
import github from "../assets/github.png";
import instagram from "../assets/instagram.png";
import linkedin from "../assets/linkedin.png";
export default {
  name: "Footer",
  data() {
    return {
      facebook,
      github,
      instagram,
      linkedin,
    };
  },
  methods: {
    date() {
        return new Date().getFullYear()
    }
  }
};
</script>

<style scoped>
footer {
    width: auto;
    height: auto;
    display: flex;
    justify-content: space-between;
    padding: 12px;
    background-color: var(--color1);
    overflow: hidden;
}
footer .img {
    width: 15%;
    display: flex;
    gap: 15px;
    justify-content: space-between;
}
@media screen and (max-width: 336px) {
    footer .img {
        gap: 10px   ;
    }
}

</style>