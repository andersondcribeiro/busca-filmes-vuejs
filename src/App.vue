<template>
  <header>
    <router-link to="/">

    <!-- Título da página -->
    <h1><span>Busca</span>Filmes</h1> 
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<!-- Cabeçalho + fundo + H1  -->

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;

  &::selection {
    background: transparenttize(#5c5c59, 0.5);
  }

body {
  background-color: #f3f3f3;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #222222; 
  box-shadow: 0px 0px 6px rgba(0,0,0,0.1);

  h1{
    color: #f5c518e7;
    font-size: 28px;
  }

  span {
    color: #f5f5f5;
  }
}
  
}
 
</style>
