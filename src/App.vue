<template>
  <v-app>
    <v-app-bar
      fixed
      color="#fcb69f"
      dark
      shrink-on-scroll
      src="https://static.bandainamcoent.eu/high/dragon-ball/dragonball-fighters-z/00-page-setup/dbfz_banner.jpg"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(60,30,50,1), rgba(128,20,40,.2)"
        ></v-img>
      </template>

      <v-toolbar-title>Esferas del Dragón</v-toolbar-title>

      <v-spacer></v-spacer>
      <v-btn
        v-if="currentUser"
        class="ma-2"
        color="orange"
        @click="onLogoutClick"
      >
        Cerrar Sesión
      </v-btn>
    </v-app-bar>
    <v-container style="height: 150px;"></v-container>

    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
import Axios from "axios";
import { mapState, mapActions } from "vuex";

export default {
  name: "App",

  components: {},

  data: () => ({
    charImgUrl: ""
  }),

  methods: {
    ...mapActions(["logout"]),

    getRandomDBCharacterImgUrl: async function() {
      const base_url = "https://dragon-ball-api.herokuapp/api/character/";
      const url = base_url + this.getRandomDBCharacter();
      let res = await Axios.get(url);

      return res.data.image;
    },
    getRandomDBCharacter: () => {
      const characterList = ["Goku", "Gohan", "Vegeta"];
      return characterList[Math.floor(Math.random() * characterList.length)];
    },
    onLogoutClick: function() {
      this.logout();
    }
  },

  computed: mapState(["currentUser"]),

  mounted: function() {}
};
</script>
