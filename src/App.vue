<template>
  <v-app id="app">
    <NavDesktop />
    <v-main class="body">
      <div id="gradientHeader" class="noDark"></div>

      <div class="cornerIcons fRight">
        <v-card
          class="cornerIcon circle dispflexcenter shadow box"
          @click.stop="drawer = !drawer"
        >
          <v-tooltip bottom>
            <template v-slot:activator="{ on, attrs }">
              <span v-bind="attrs" v-on="on"
                ><v-icon id="notifications">mdi-bell</v-icon></span
              >
            </template>
            <span>Notifications</span>
          </v-tooltip>
        </v-card>
        <v-card
          class="cornerIcon circle dispflexcenter shadow box"
          @click.stop="drawer1 = !drawer1"
        >
          <v-tooltip bottom>
            <template v-slot:activator="{ on, attrs }">
              <span v-bind="attrs" v-on="on"
                ><v-icon id="profile">mdi-account-circle</v-icon></span
              >
            </template>
            <span>My Account</span>
          </v-tooltip>
        </v-card>
        <v-card
          class="cornerIcon circle dispflexcenter shadow box"
          @click="darkMode"
        >
          <v-tooltip bottom>
            <template v-slot:activator="{ on, attrs }">
              <span v-bind="attrs" v-on="on"
                ><v-icon id="darkMode">dark_mode</v-icon></span
              >
            </template>
            <span>Dark Mode</span>
          </v-tooltip>
        </v-card>
      </div>

      <v-navigation-drawer
        id="notificationsDrawer"
        v-model="drawer"
        fixed
        temporary
        hide-overlay
        top
        right
        height="200"
        class="box"
      >
        <v-list-item-group v-model="group" class="flexcol">
          <div>
            <h3 align="center">You have no new notifications.</h3>
          </div>
          <hr class="line" />
          <h3 class="tcenter">...</h3>
          <hr class="line" />
          <v-list-item align="bottom">
            <router-link id="view" class="RedBtn" to="/Extras/MyProfile">
              View All
            </router-link>
          </v-list-item>
        </v-list-item-group>
      </v-navigation-drawer>

      <v-navigation-drawer
        id="profileDrawer"
        v-model="drawer1"
        fixed
        temporary
        hide-overlay
        top
        right
        height="300"
        class="box"
      >
        <v-list-item-group v-model="group1">
          <div class="flex center">
            <h3>Welcome!</h3>
          </div>
          <hr class="line" />
          <div class="flex center">
            <h3>Domains</h3>
          </div>
          <div id="domain" class="flex spaceBetween">
            <img id="domainImg" src="./assets/logoT.svg" alt="domain image" />
            <p class="flex vcenter">Someone@something.com</p>
          </div>
          <v-list-item class="flex spaceBetween">
            <v-icon class="dark">mdi-plus-thick</v-icon>
            <router-link to="/Setup/DomainsAndPages" class="dark">
              Add Domain</router-link
            >
          </v-list-item>
          <hr class="line" />
          <v-list-item class="flex spaceBetween">
            <v-icon class="dark">mdi-account</v-icon>
            <router-link to="/Extras/MyProfile" class="dark">
              My Profile
            </router-link>
          </v-list-item>
          <v-list-item class="flex spaceBetween">
            <v-icon class="dark">mdi-lifebuoy</v-icon>
            <router-link to="/" class="dark"> Help Guides </router-link>
          </v-list-item>
          <v-list-item class="flex spaceBetween">
            <v-icon class="dark">mdi-logout</v-icon>
            <router-link to="/" class="dark"> Logout </router-link>
          </v-list-item>
        </v-list-item-group>
      </v-navigation-drawer>

      <router-view class="router" />
    </v-main>
    <NavMobile />
  </v-app>
</template>

<script>
import NavDesktop from "./components/Navigation/NavDesktop.vue";
import NavMobile from "./components/Navigation/NavMobile.vue";
//import NavMobile from './components/Navigation/NavMobile'

export default {
  name: "App",

  components: {
    NavDesktop,
    NavMobile,
    //NavMobile
  },

  data: () => ({
    drawer: false,
    group: null,
    drawer1: false,
    group1: null,
    
  }),
  

  watch: {
    group() {
      this.drawer = false;
      this.drawer1 = false;
    },
  },

  methods: {
    darkMode: function (e) {
      if (e) {
        document.documentElement.classList.toggle("darkMode");

        document.querySelectorAll(".noDark").forEach((result) => {
          result.classList.toggle("noDarkMode");
        });
      }
    },
  },
};
</script>

<style lang="scss">
@import "./src/styles/styles.scss";
@import url("https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;700&display=swap");

#app {
  font-family: "Quicksand", sans-serif;
  font-smooth: always;
}

.theme-dark {
  background-color: rgb(80, 80, 80) !important;
}
:root {
  transition: 0.3s;
}
.body {
  background: map-get($cs, bg);
  margin-left: 350px;
  overflow: hidden;
  @media (max-width: $md) {
    margin-left: 0px !important;
  }
  @media (max-width: $lg) {
    margin-left: 200px;
  }
  #gradientHeader {
    position: absolute;
    width: 120%;
    left: -10%;
    z-index: 0;
    height: 250px;
    background-image: linear-gradient(
      map-get($cs, purple1),
      map-get($cs, button)
    );
    border-radius: 0% 0% 100% 100% / 0% 0% 100% 100%;

    @media (max-width: $md) {
      height: 200px !important;
    }
  }
  #notificationsDrawer {
    border-radius: 10px 0 0 10px;
  }
  #profileDrawer {
    border-radius: 10px 0 0 10px;
    #domain {
      padding: 0 10px;
    }
    #domainImg {
      border-radius: 5px;
      width: 30px;
      height: 30px;
      padding: 5px 1px 1px 1px;
    }
  }
  .cornerIcons {
    position: fixed;
    z-index: 3;
    right: 6%;
    display: flex;
    justify-content: space-between;
    @media (min-width: $md) {
      width: 120px !important;
    }
    .cornerIcon {
      margin-left: 0.5em;
      margin-top: 2em;
      @media (max-width: $md) {
        font-size: $medium;
        width: 35px;
        height: 35px;
      }

      #notifications {
        color: map-get($cs, button);
        width: 50px;
      }
      #profile {
        color: map-get($cs, accept);
        width: 50px;
      }
      #darkMode {
        color: map-get($cs, purple1);
        width: 50px;
      }
    }
  }
  .router {
    overflow-x: hidden !important;
    position: relative;
    z-index: 2;
    animation: appear 0.2s ease;
  }
}

/* DRAWERS of Notifications & Profile corner buttons */
.v-navigation-drawer {
  margin-top: 70px;
}
.v-list-item {
  padding: 0 10px;
  justify-content: center;
  a {
    text-decoration: none;
    color: map-get($cs, primary);
  }
}
.v-application p {
  margin: 5px 5px 5px 0;
}

/* pop up windows grow bigger after breakpoint $sm*/
.v-dialog {
  @media (min-width: $sm) {
    width: 600px !important;
  }
}
</style>
