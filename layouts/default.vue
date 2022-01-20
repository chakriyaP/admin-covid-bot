<template>
  <v-app>
    <v-app-bar fixed app elevation="0">
      <a href="/" @click="checkPath('/#home')">
        <img
          class="mx-2"
          src="~assets/logo.png"
          height="auto"
          width="60"
          contain
        />
      </a>
      <h2>Covid-19 Tracker</h2>
      <v-spacer />
      <a
        v-for="(item, i) in items"
        @click="checkPath(item.path)"
        :key="i"
        :href="item.path"
        :target="item.target"
        :class="`menu-item item-desktop ${i === index ? 'active' : ''}`"
      >
        <span v-if="!item.list">
          {{ item.list ? "" : item.title }}
        </span>
      </a>
      <v-btn icon @click.stop="rightDrawer = !rightDrawer" class="item-mobile">
        <v-icon color="white">mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer v-model="rightDrawer" temporary fixed>
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i">
          <a
            :href="item.path"
            style="width: 100%"
            :class="`menu-item ${i === index ? 'active' : ''}`"
            @click="checkPath(item.path)"
            :target="item.target"
          >
            <v-list-item-title v-if="!item.list">
              {{ item.title }}</v-list-item-title
            >
          </a>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <Nuxt />
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span> COPYRIGHT © 2022 </span>
    </v-footer>
  </v-app>
</template>

<script>
import routers from "./router";
import { mdiAccount } from "@mdi/js";
export default {
  data() {
    return {
      fixed: false,
      id: "",
      index: 0,
      items: routers,
      miniVariant: false,
      title: "Vuetify.js",
      rightDrawer: false,
      icons: {
        mdiAccount,
      },
    };
  },
  methods: {
    checkPath(path) {
      // if (
      //   this.getPath().includes("pledge") ||
      //   this.getPath().includes("move-finance")
      // ) {
      //   window.open(window.location.origin + this.getPath());
      // }
      this.items.forEach((item, index) => {
        if (path) {
          if (path === item.path) this.index = index;
        } else {
          if (this.getPath().includes(item.path)) this.index = index;
        }
      });
    },
    getPath() {
      const path = window.location.pathname;
      const hash = window.location.hash;
      return "/" + path.slice(1) + hash;
    },
  },
  async mounted() {
    this.checkPath();
  },
};
</script>
<style scoped lang="scss">
.item-desktop {
  display: none;
  transition: all 0.2s ease;
  @media screen and (min-width: 769px) {
    display: block;
    transition: all 0.2s ease;
  }
}

.item-mobile {
  display: block;
  transition: all 0.2s ease;
  color: $primary-background-color;
  @media screen and (min-width: 769px) {
    display: none;
    transition: all 0.2s ease;
  }
}

.menu-item {
  color: $primary-background-color;
  font-size: 1.2rem;
  margin-right: 1rem;
  text-decoration: none;
  transition: all 0.2s ease;

  &.active {
    color: $primary-color;
    padding: 0 10px;
    border-radius: 4px;
    background-color: $primary-background-color;
    @media screen and (max-width: 769px) {
      padding: 0.5rem 1rem;
    }
  }
  &:hover {
    color: $text-color;
    text-decoration: none;
    transition: all 0.2s ease;
  }
}

.span {
  color: white;
  &.ative {
    color: $primary-color;
  }
}

::v-deep .v-toolbar__content,
::v-deep .v-navigation-drawer__content {
  background-color: #96c5cb;
  color: white;
}

::v-deep .v-footer {
  background-color: $primary-color;
  justify-content: center;
  color: white;
  span {
    font-weight: 600;
  }
}
::v-deep .v-sheet.v-footer:not(.v-sheet--outlined) {
  text-align: center;
}
</style>