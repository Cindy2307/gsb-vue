<template>
  <header
    class="d-flex justify-content-between align-items-center p-2 bg-white"
  >
    <img
      src="../assets/img/logo-gsb.png"
      id="logo"
      alt="logo"
      @click="rediriger"
    />
    <div
      class="d-flex justify-content-end align-items-center"
      id="connexion"
      v-if="getLogin && getLogin !== 'null'"
    >
      <div class="fs-5 mr-5 text-primary" id="pseudo">
        Bonjour, {{ getLogin }}
      </div>
      <i
        id="deconnexion"
        class="fas fa-power-off fs-5 text-primary"
        @click="logout"
      ></i>
    </div>
  </header>
</template>

<script>
import axios from "axios";

export default {
  name: "Header",
  methods: {
    logout: async function () {
      await axios
        .get("https://localhost/gsb/logout", {
          withCredentials: true,
        })
        .catch((e) => {
          console.log(e);
        })
        .then(() => {
          localStorage.clear();
          this.$store.dispatch("setLogin", null);
          this.$router.push("/");
        });
    },
    rediriger: function () {
      switch (localStorage.getItem("role")) {
        case "VIS":
          this.$router.push("/rapportsVisiteur");
          break;
        case "RC":
          this.$router.push("/rapportRedacteurListe");
          break;
        case "RH":
          this.$router.push("/utilisateurs");
          break;
      }
    },
  },
  computed: {
    getLogin: function () {
      return this.$store.getters.getLoginFromStore;
    },
  },
};
</script>

<style scoped>
img {
  width: 3%;
}
#deconnexion:hover {
  color: #dc3545 !important;
}
#connexion div {
  padding-right: 10px;
  font-weight: bold;
}
#deconnexion,
#logo {
  cursor: pointer;
}
input:focus,
textarea:focus,
button:focus,
select:focus {
  outline: 0;
}
</style>