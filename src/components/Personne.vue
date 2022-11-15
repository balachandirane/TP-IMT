<template>
  <div v-if="currentPersonne">
    <div class="form-group">
      <label for="id">ID</label>
      <input type= "text" readony class= "form-control" id= "id"
      v-model= "currentPersonne.id"
      />
         </div>
    <div class="form-group">
    <label for="surname">Prénom</label>
    <input type="text" class="form-control" id="surname"
    v-model= "currentPersonne.surname"
      />
     </div>
     <div class="form-group">
    <label for="name">Nom</label>
    <input type="text" class="form-control" id="name"
    v-model= "currentPersonne.name"
      />
     </div>
     <div class="form-group">
    <label for="phone">Téléphone</label>
    <input type="text" class="form-control" id="phone"
    v-model= "currentPersonne.phone"
      />
     </div>
     <div class="form-group">
    <label for="city">Ville</label>
    <input type="text" class="form-control" id="city"
    v-model= "currentPersonne.city"
      />
    </div>
    </div>

    <!-- A INCLURE DANS LE FORM -->
    <button class="badge badge-danger mr-2"
      @click="deletePersonne"
    >
      Supprimer
    </button>

    <!-- A INCLURE DANS LE FORM -->
    <button type="submit" class="badge badge-success"
      @click="updatePersonne"
    >

      Modifier
    </button>
    <p>{{ message }}</p>
    
</template>

<script>
import PersonneDataService from "../services/PersonneDataService";

export default {
  name: "personne",
  data() {
    return {
      currentPersonne: null,
      message: ''
    };
  },
  methods: {
    getPersonne(id) {
      // A COMPLETER
      PersonneDataService.get(id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    updatePersonne() {
      // A COMPLETER
            PersonneDataService.update(this.currentPersonne)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },

    deletePersonne() {
      // A COMPLETER
                  PersonneDataService.delete(this.currentPersonne.id)
        .then(response => {
          this.currentPersonne = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    }
  },
  mounted() {
    this.message = '';
    this.getPersonne(this.$route.params.id);
  }
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>
