<template>
  <section id="home" variants="{sectionVariants}">
    <div className="l-side">
      <h1><span>Welcome to </span>Culinary App</h1>
      <p>
        Experience a culinary adventure like no other with the Meal App,
        offering an exclusive collection of top-notch recipes sourced from
        diverse corners of the world. Elevate your cooking endeavors by
        accessing a wide array of high-quality recipes, thoughtfully curated to
        represent global flavors and gastronomic delights.
      </p>
    </div>
    <div className="r-side">
      <div className="grid-container">
        <div className="grid-item-1"></div>
        <div className="grid-item-2"></div>
        <div className="grid-item-3"></div>
        <div className="grid-item-4"></div>
        <div className="grid-item-5"></div>
        <div className="grid-item-6"></div>
        <div className="grid-item-7"></div>
        <div className="grid-item-7"></div>
      </div>
    </div>
  </section>
</template>

<script>
export default {};
</script>

<style scoped>
#home {
    position: relative;
    width: 100vw;
    width: 100dvw;
    height: calc(100vh - 144px);
    height: calc(100dvh - 144px);
    display: flex;   
    background-color: var(--color3);
    overflow: hidden;
}
#home .l-side {
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 20px;
}
#home .l-side h1 {
    text-transform: uppercase;
    font-size: 2rem;
}
#home .l-side h1 span{
    display: block;
    text-transform: capitalize; 
    font-size: 1.5rem;
    font-style: italic;
}
#home .r-side {
    width: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}
#home .r-side .grid-container {
    width: 70%;
    height: 80%;
    display: grid;
    grid-template-columns: auto auto;
    grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    gap: 10px;
    cursor: grab;
}
#home .r-side .grid-container > *{
    background-color: var(--color1);
    border-radius: 10px;
    cursor: pointer;
    transition: filter 500ms ease-in-out, transform 500ms ease-in-out;
}
#home .r-side .grid-container:hover > *:not(:hover) {
    filter: blur(4px);
    transform: scale(0.9);
}
#home .r-side .grid-container .grid-item-1{
    grid-row: span 2;
}
#home .r-side .grid-container .grid-item-3{
    grid-row: span 3;
}
#home .r-side .grid-container .grid-item-4{
    grid-row: span 3;
}
#home .r-side .grid-container .grid-item-5{
    grid-row: span 3;
}
#home .r-side .grid-container .grid-item-6{
    grid-row: span 3;
}
#home .r-side .grid-container .grid-item-7{
    grid-row: span 2;
}
#home .r-side .grid-container .grid-item-8{
    grid-row: span 1;
}


@media screen and (max-width: 674px) {
    #home .l-side{
        width: 100%;
    }
    #home .r-side{
        display: none;
    }
}
</style>