<template>
  <header>
    <router-link to="/">
      <h1><span>Movie</span>App</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  color: #d7d7d7;

  &::selection {
    background: transparentize($color: #59ffa1, $amount: 0.5);
  }
}

body {
  background-color: #2b516c;
}

a {
  text-decoration: none;
}

h1 {
  font-size: 2rem;
  color: rgb(3, 193, 246);
  cursor: pointer;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 20px;
}

@media only screen and (min-width:1024px){
  h1{
    font-size: 3rem;
  }
  h3{
    font-size: 1.8rem !important;
  }
  p{
    font-size: 1.2rem !important;
  }
}
</style>
