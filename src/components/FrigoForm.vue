<script setup>
import { ref } from "vue";
// -- donnée réactive pour la saisie du libellé
const nom = ref("");
const qte = ref("");
const photo = ref("");
defineEmits(["addA"]);

const resetForm = () => {
  nom.value = "";
  qte.value = "";
  photo.value = "";
}
</script>


<template>
  <body class="form">
    <h4>Ajouter un aliment au frigo: </h4>
    <form @submit.prevent="$emit('addA', nom, qte, photo); resetForm()" class="formInput">
      <div class="input">
        <input class="inputA" type="text" v-model="nom" placeholder="Aliment ?"/> 
        <input class="inputQ" type="text" v-model="qte" placeholder="Quantité ?"/> 
        <input class="inputP" type="text" v-model="photo" placeholder="Photo ?" title="Ajouter un lien vers une photo pour un meilleur visuel!" />
      </div>
      <!-- Bouton Valider -->
      <button class="send" type="submit"> 
        <img id ="valider" src="./icons/send.png" alt="Bouton Valider">
      </button>
    </form>
  </body>
</template>


<style scoped>

.form{
  margin-left: 25px;
  background-color: rgba(108, 154, 156, 0.025);
}

.formInput{
  padding-left: 40px;
  display: flex;
  justify-content: center;
}

.input{
  display: flex;
  flex-direction: column;
}

.inputA, .inputQ, .inputP {
  border: none;
  border-bottom: 5px solid steelblue;
  background-color: rgb(159, 202, 204);
  background-image: url('icons/food.png');
  background-size: 20%;
  background-position: right;
  background-repeat: no-repeat;
  padding-top: 15px;
  width: 150px;
  border-radius: 10px;
  margin-bottom: 10px;
}

.send {
  border: none;
  padding: 15px;
  background: none;
  cursor: pointer;
  align-self: flex; 
}

#valider {
  width: 50px;
  height: 50px; 
}

.send:hover {
  transform: scale(1.2); 
}

.inputA:hover, .inputQ:hover, .inputP:hover {
  transform: scale(1.1); 
}

</style>