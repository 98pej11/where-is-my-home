<template>
  <div>
    <b-navbar toggleable="lg" type="dark">
      <b-navbar-brand href="#">
        <router-link :to="{ name: 'main' }">
          <b-img
            :src="require('@/assets/ssafy_logo.png')"
            id="logo"
            class="d-inline-block align-top"
            alt="logo"
          ></b-img>
        </router-link>
      </b-navbar-brand>

      <b-collapse is-nav>
        <b-navbar-nav>

          <b-nav-item>
            <router-link :to="{ name: 'main' }" class="link">
              Main
            </router-link>
            <router-link :to="{ name: 'board' }" class="m-2 link">
              Board
            </router-link>
            <router-link :to="{ name: 'house' }" class="m-2 link">
              ApartInfo
            </router-link>
          </b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav>
          <b-nav-item right>
            <router-link :to="{ name: 'login' }" class="link">
              <b-icon icon="person-circle"> </b-icon> Member
            </router-link>
          </b-nav-item>
        </b-navbar-nav>
        
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "TheHeaderNavbar",
  data() {
    return {};
  },
};
</script>

<style scoped>
#logo {
  width: 100px;
}

.link {
  text-decoration: none;
  font-weight: bold;
  padding: 23px;
}

.navbar.navbar-dark.bg-dark{
    background-color: rgba(0, 0, 0, 0);
 }

 a{
  text-decoration: none;
  color: aliceblue;
 }
</style>