<template>
    <header class="app-header navbar b-b-0">
        <button class="navbar-toggler mobile-sidebar-toggler d-lg-none" @click="toggleSidebar" type="button">
            <span class="navbar-toggler-icon"></span>
        </button>
        <a class="navbar-brand" v-bind:class="{sidebarClosed: toggle}">
            <div class="avatar-wrapper">
                <div class="avatar-picture mr-3">
                    <avatar :username="`${$store.state.auth.user.firstname} ${$store.state.auth.user.lastname}`"></avatar>
                </div>
                <div class="avatar-name">
                     <router-link :to="`/admin/users/${$store.state.auth.user._id}`">{{ $store.state.auth.user.firstname }} {{ $store.state.auth.user.lastname }}</router-link>
                </div>
            </div>
        </a>
        
        <button class="navbar-toggler sidebar-toggler d-md-down-none h-100 px-3" @click="toggleSidebar" type="button">
            <span class="navbar-toggler-icon"></span>
        </button>
        <ul class="nav navbar-nav d-md-down-none d-none mr-auto">
            <form class="form-inline px-4">
                <i class="fa fa-search"></i>
                <input class="form-control" type="text" placeholder="Search..."/>
            </form>
        </ul>
        <ul class="nav navbar-nav d-md-down-none ml-4 mr-auto">
            <li class="nav-item">
                <img src="../../assets/img/Logo-WM-Gelb.gif" height="15px"/>
            </li>
        </ul>
        <ul class="nav navbar-nav ml-auto">
            <li class="nav-item nav navbar-nav mr-auto" >
                <form class="form-inline px-4">
                    <i class="ca ca-search ca-2x"></i>
                    <input class="form-control" type="text" placeholder="Suchen...">
                </form>
            </li>
            <li class="nav-item dropdown d-md-down-none" @click="logout()">
                <button class="nav-link" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
                    <i class="ca ca-logout-3 ca-2x"></i>
                </button>
            </li>
        </ul>
    </header>
</template>

<script>
  import Avatar from 'vue-avatar'
  export default {
    name: 'layout-header',
    data () {
      return {
        toggle: false
      }
    },
    components: {
      Avatar
    },
    methods: {
      toggleSidebar () {
        this.toggle = !this.toggle
        this.$emit('toggleSidebar')
      },
      logout () {
        console.log('Logout?')
        this.$store.dispatch('auth/logout')
          .then(() => this.$router.push('/login'))
      }
    }
  }
</script>
