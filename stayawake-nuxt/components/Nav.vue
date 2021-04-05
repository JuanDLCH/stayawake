<template>
  <nav>
    <nuxt-link to="/"
      ><img src="@/static/img/stayawakelogo.svg" alt="logo" class="logo"
    /></nuxt-link>
    <ul>
      <li><nuxt-link to="/">Inicio</nuxt-link></li>
      <li><nuxt-link to="/#origen">Origen</nuxt-link></li>
      <li><nuxt-link to="/#objetivo">Objetivo</nuxt-link></li>
      <li><nuxt-link to="/#nosotros">Nosotros</nuxt-link></li>
      <li>
        <a href="mailto:stayawakeproject@yopmail.com">Contactanos</a>
      </li>
    </ul>
  </nav>
</template>

<style>
/* Barra de navegacion */
header {
  height: 100vh;
  width: 100%;
  position: relative;
}

.logo {
  height: 90%;
  width: 10%;
  margin: 5px;
}

nav {
  align-items: center;
  content: '';
  position: fixed;
  height: 10vh;
  bottom: 0;
  right: 0;
  left: 0;
  top: 0;
  background: rgba(0, 0, 0, 0.65);
  z-index: 4;
}
nav ul {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  list-style-type: none;
  margin-top: 0;
  height: 5vh;
}

nav li {
  margin: 7px;
}

nav a {
  color: white;
  text-decoration: none;
  font-size: 20px;
}

nav a:hover {
  font-size: 23px;
  color: rgb(184, 184, 184);
}
</style>