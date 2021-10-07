<template>
<header>
  <router-link to="/">
  <h1><span>Vue</span>Movies</h1>
  </router-link>
</header>
<main>
  <router-view/>
</main>
</template>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Lucida Sans', sans-serif;
}

body{
  background-color:#FAFAFA;
}
a{
  text-decoration: none;
}

header{
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.625rem 1rem;
  background-color: #2C3D4E;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 1rem;
}

h1{
  color:white;
  font-size: 2rem;
  span{
    color: #42b883

  }
}
</style>
