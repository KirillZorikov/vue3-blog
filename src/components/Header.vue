<template>
  <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container">
      <router-link :to="{name: 'Home'}" class="navbar-brand mr-5"><span style="color:red">Ya</span>Tube</router-link>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
              aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <form class="form-inline my-2 my-lg-0" @submit.prevent="handleSearch">
          <input v-model="search" required class="form-control mr-1" type="text" placeholder="Поиск по сайту">
          <button class="btn btn-outline-secondary my-2 my-sm-0" type="submit">Поиск</button>
        </form>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item mr-5">
            <router-link class="nav-link" :to="{name: 'AddPost'}">Добавить пост</router-link>
          </li>
          <li class="nav-item dropdown">
            <div class="btn-group open">
              <template v-if="currentUser">
                <router-link class="btn btn-primary"
                   :to="{name: 'Profile', params: {username: currentUser.username}}">
                  <i class="fa fa-user fa-fw"></i>
                  {{ currentUser.username }}
                </router-link>
                <a class="btn btn-primary dropdown-toggle"
                   data-toggle="dropdown">
                </a>
                <ul class="dropdown-menu">
                  <li>
                    <router-link :to="{name: 'ChangePassword'}">
                      <i class="fa fa-key fa-fw"></i>
                      Изменить пароль
                    </router-link>
                  </li>
                  <li>
                    <router-link :to="{name: 'Logout'}">
                      <i class="fa fa fa-sign-out-alt fa-fw"></i>
                      Выйти
                    </router-link>
                  </li>
                </ul>
              </template>
              <template v-else>
                <router-link :to="{name: 'Login'}" class="btn btn-primary text-light">
                  <i class="fa fa-user fa-fw"></i>
                  Вход
                </router-link>
                <a class="btn btn-primary dropdown-toggle"
                   data-toggle="dropdown">
                </a>
                <ul class="dropdown-menu">
                  <li>
                    <router-link :to="{name: 'Login'}">
                      <i class="fa fa fa-sign-in-alt fa-fw"></i>
                      Войти
                    </router-link>
                  </li>
                  <li>
                    <router-link :to="{name: 'Register'}">
                      <i class="fa fa-pencil-alt fa-fw"></i>
                      Регистрация
                    </router-link>
                  </li>
                </ul>
              </template>
            </div>
          </li>
        </ul>

      </div>
    </div>
  </nav>

</template>

<script>
export default {
  name: "Nav",
  data() {
    return {
      search: ''
    }
  },
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
  },
  methods: {
    handleSearch(){
      this.$router.push({name: 'Search', query:{search: this.search}});
      this.search = '';
    }
  }
}
</script>

<style scoped>

</style>