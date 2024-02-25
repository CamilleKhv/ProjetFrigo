<script setup>
defineProps(["aliment"]);
defineEmits(["searchA"]);
</script>

<template>
  <div class="search">
    <h4 class="title">Rechercher un aliment: </h4>
    <form @submit.prevent="$emit('searchA', mot)" class="form">
      <input class="input" type="text" v-model="mot" placeholder="Rechercher ?" />
      <button class="send" type="submit">
        <img id="valider" src="./icons/send.png" alt="Bouton Valider">
      </button>
    </form>
  </div>
</template>

<style scoped>
.search {
  font-family: Arial, sans-serif;
  display: flex;
  align-items: center;
}

.title{
  padding-left:18px;
  padding-right:15px;
}

.form{
  display: flex;
}

.input {
  border: none;
  border-bottom: 5px solid steelblue;
  background-color: rgb(159, 202, 204);
  background-image: url('icons/search.png');
  background-size: 20%;
  background-position: right;
  background-repeat: no-repeat;
  font-size: 15px;
  padding-top: 15px;
  width: 150px;
  margin: auto;
  border-radius: 15px;
  height: 30px;
}

.send {
  border: none;
  padding: 15px;
  background: none;
  cursor: pointer;
}

.send:hover {
  transform: scale(1.2);
}

.input:hover {
  transform: scale(1.1);
}


#valider {
  width: 50px;
  height: 50px;
}

</style>