<template>
  <div class="hello">
      <nav class="nav-extended indigo px-3">
    <div class="nav-wrapper">
      <router-link :to="{name: 'home'}" class="brand-logo"><small>Ninja<b>Smoothies</b></small></router-link>
      <a href="#" data-target="mobile-demo" class="sidenav-trigger"><i class="material-icons">menu</i></a>
    </div>
    <div class="nav-content pt-4 mt-3">
      <router-link class="btn-floating btn-large halfway-fab pink waves-effect waves-light" :to="{name: 'add'}">
        <i class="material-icons">add</i>
      </router-link>
    </div>
  </nav>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
}
</script>
