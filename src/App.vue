<template>
  <div id="app">
    <b-container>
      <b-row>
        <b-col
          cols="12"
        >
          <div id="nav" class="d-flex justify-content-center align-items-center py-4">
            <router-link to="/">Test-1</router-link> |
            <router-link to="/test2">Test-2</router-link>
          </div>
        </b-col>
      </b-row>
    </b-container>
    <router-view />
  </div>
</template>

<style lang="scss">
@import "./assets/sass/main";
</style>
