<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="/"><h3>Gadget Management</h3></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <template v-if="$auth.loggedIn">
            <b-nav-item href="/dashboard"><span class=" btn btn-info">Dashboard</span></b-nav-item>
            <b-nav-item href="/gadgets"><span class=" btn btn-warning">Gadgets</span></b-nav-item>
            <b-nav-item href="#" @click.prevent="onLogout"><span class=" btn btn-danger">Logout</span></b-nav-item>
          </template>
          <template v-else>
            <b-nav-item href="/register"><span class=" btn btn-success">Register</span></b-nav-item>
            <b-nav-item href="/login"><span class=" btn btn-primary">Login</span></b-nav-item>
          </template>  
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  methods: {
    async onLogout() {
      await this.$auth.logout()
    }
  }
}
</script>

<style>
</style>