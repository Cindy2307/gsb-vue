<template>
  <main class="mx-auto d-flex align-items-center">
    <div class="container login-container">
      <div class="row">
        <div class="col-3"></div>
        <div class="col-6 login-form-1 center px-5 py-4">
          <h3 class="text-center text-white mb-5">Modifier un utilisateur</h3>
          <form @submit.prevent="modifierUtilisateur()">
            <div class="form-group row">
              <p class="col-6 d-flex flex-column">
                <label class="text-white">Nom:</label>
                <input
                  type="text"
                  name="nom"
                  id="nom"
                  placeholder="Nom"
                  v-model="nom"
                />
              </p>
              <p class="col-6 d-flex flex-column">
                <label class="text-white">Prénom:</label>
                <input
                  type="text"
                  name="prenom"
                  id="prenom"
                  placeholder="Prénom"
                  v-model="prenom"
                />
              </p>
            </div>
            <div class="form-group">
              <p id="parAdresse" class="d-flex flex-column">
                <label class="text-white">Adresse:</label>
                <input
                  class="w-100"
                  coltype="text"
                  name="adresse"
                  id="adresse"
                  placeholder="Adresse"
                  v-model="adresse"
                />
              </p>
            </div>
            <div class="form-group row">
              <p class="col-6 d-flex flex-column">
                <label class="text-white">Code postal:</label>
                <input
                  type="text"
                  name="CP"
                  id="CP"
                  placeholder="Code Postal"
                  v-model="codePostal"
                />
              </p>
              <p class="col-6 d-flex flex-column">
                <label class="text-white">Ville:</label>
                <input
                  type="text"
                  name="ville"
                  id="ville"
                  placeholder="Ville"
                  v-model="ville"
                />
              </p>
            </div>
            <div class="form-group row">
              <p class="col-6 d-flex flex-column">
                <label class="text-white">Date de naissance:</label>
                <input
                  type="date"
                  name="date"
                  id="dateNaissance"
                  placeholder="Date de naissance"
                  v-model="dateNaissance"
                />
              </p>
            </div>
            <div class="form-group d-flex mt-4">
              <button
                type="submit"
                id="modifier"
                class="btnSubmit d-block m-auto rounded-pill bg-transparent text-primary px-3 py-2 border-primary fs-5"
              >
                Modifier
              </button>
              <button
                type="submit"
                id="annuler"
                class="btnSubmit d-block m-auto rounded-pill bg-transparent text-danger px-3 py-2 border-danger fs-5"
                @click="annuler()"
              >
                Annuler
              </button>
            </div>
          </form>
        </div>
        <div class="col-3"></div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";

export default {
  name: "CreerUtilisateur",
  data() {
    return {
      login: "",
      password: "",
      nom: "",
      prenom: "",
      adresse: "",
      codePostal: "",
      ville: "",
      dateNaissance: "",
    };
  },
  methods: {
    modifierUtilisateur: async function () {
      await axios(
        "https://localhost/gsb/" +
          localStorage.getItem("route") +
          "/" +
          localStorage.getItem("utilisateurId"),
        {
          method: "PUT",
          withCredentials: true,
          headers: {
            "Content-Type": "application/json",
          },
          data: {
            login: localStorage.getItem("utilisateurId"),
            nom: this.nom,
            prenom: this.prenom,
            adresse: this.adresse,
            codePostal: this.codePostal,
            ville: this.ville,
            dateNaissance: this.dateNaissance,
          },
        }
      ).then((response) => {
        let data = response.data;
        localStorage.setItem("utilisateurId", data.login);
        this.$router.push("/ficheUtilisateur");
      });
    },
    annuler: function () {
      this.$router.push("/ficheUtilisateur");
    },
  },
};
</script>

<style scoped>
main {
  width: 80%;
  height: 90vh;
}

.login-form-1 {
  background-color: rgba(0, 0, 0, 0.37);
}

button {
  width: 40%;
}
</style>