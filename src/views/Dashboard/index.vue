<template>
  <section class="dashboard">
    <!-- NAVBAR -->
    <b-navbar class="navbar-default" toggleable="sm">

      <router-link :to="'/dashboard'" class="navbar-brand hidden-md-up">
        <b-nav-toggle target="nav_collapse">
          <icon class="nav-bars" name="bars"></icon>
        </b-nav-toggle>
        <img :src="storjLogo" alt="Storj" class="mobile-logo" />
      </router-link>

      <b-collapse is-nav id="nav_collapse">
        <b-nav class="nav navbar-nav navbar-left">
          <b-nav-item> 
            <img :src="storjLogo" alt="Storj" class="logo nav-logo hidden-sm-down" />
          </b-nav-item>
          <b-nav-item @click="navigateTo('Buckets')">Buckets</b-nav-item>
          <b-nav-item @click="navigateTo('Billing')">Billing</b-nav-item>
          <b-nav-item @click="navigateTo('Referrals')">Referrals</b-nav-item>
          <b-nav-item href="https://storj.readme.io/">Documentation</b-nav-item>
          <b-nav-item href="https://storj.github.io/bridge">API</b-nav-item>
          <b-nav-item href="https://storj.readme.io/discuss">Support</b-nav-item>
          <b-nav-item @click="navigateTo('Settings')">Settings</b-nav-item>
        </b-nav>

        <b-nav is-nav class="ml-auto">
          <b-nav-item @click="handleClick">Logout</b-nav-item>
        </b-nav>
      </b-collapse>

    </b-navbar>

    <!-- ROUTER VIEW FOR AUTHENTICATED VIEWS -->
    <router-view
      class="authenticated-views"
      keep-alive
      transition
      transition-mode="out-in"
    >
    </router-view>

  </section>
</template>

<script>
import 'vue-awesome/icons/bars';
import storjLogo from '../../../static/img/logo-blue.svg';
import { mapActions } from 'vuex';

export default {
  name: 'dashboard',

  data () {
    return {
      storjLogo
    };
  },

  methods: {
    ...mapActions([ 'logout' ]),

    handleClick () {
      this.logout()
        .then(() => this.$router.push({ name: 'Login' }))
        .catch(() => this.$router.push({ name: 'Login' }));
    },

    navigateTo (page) {
      this.$router.push({ name: page });
    }
  }
};
</script>

<style lang="scss" scoped>
  .dashboard {
    background: #f9f9f9;
    padding-bottom: 3em;
    height: 100%;
    width: 100%;
  }

  .dashboard > .navbar-default {
    margin-bottom: -1px;
    padding-bottom: 0;
  }

  .dashboard > .navbar-default .navbar-nav {
    padding-bottom: 0;
  }

  .navbar-logo {
    padding: 0px;
    margin: 0px;
  }

  .mobile-logo {
    height: 40px;
    width: auto;
    margin: 0px 80px; 
    display: inline-block;
  }

  .navbar-brand {
    margin: 5px;
  }

  .nav-link {
    margin: 0px;
    padding: 0px;
  }

  .authenticated-views {
    background: #f9f9f9;
    padding: 3rem;
  }

  .dashboard .nav-item {
    margin: 0 0.5rem;
    min-width: 80px;
  }

  .nav-item:hover {
    cursor: pointer;
  }

  .nav-bars {
    margin: 4px 0px 0px 0px;
  }
</style>
<!-- <style src="bootstrap/dist/css/bootstrap.css"></style>
<style src="bootstrap-vue/dist/bootstrap-vue.css"></style> -->
