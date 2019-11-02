<template>
  <div id="app">

    <div id="nav">
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a class="navbar-brand"><router-link to="/">Hangry</router-link></a>
        <!-- <router-link to="/about">About</router-link> -->
        <router-link to="/recipe-form">Add Recipes</router-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
      </nav>
    </div>
    <router-view/>
  </div>
</template>

  <style>
    a{
      color: whitesmoke;
    }
    body{
      margin: 0;
      padding: 0;
      height: 100vh;
      width: 100vw;
    }

</style>
