<template>
<div>
  <header>
    <router-link to="/">
    <h1 class="app-title">Popular movies</h1>
    </router-link>
  </header>
  <main>
    <router-view/>
  </main>
</div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Roboto+Condensed');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
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
.app-title{
  color: white;
}

</style>
