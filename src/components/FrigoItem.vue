<script setup>
defineProps(["aliment"]);
defineEmits(["deleteA", "searchA", "moreA", "lessA"])
</script>


<template>
        <div class="show">
            {{ aliment.afficherNom() }}
            {{ aliment.afficherQte() }}<br>
            <img :src="aliment.photo" style="width: 100px; height: 100px;" />
        </div>
        <div class="feat">
            <button @click="$emit('deleteA', aliment.id)" class="button">
                <img id="delete" src="./icons/delete.png" alt="Bouton Supprimer">
            </button>
            <button @click="$emit('lessA', aliment)" class="button">
                <img id="less" src="./icons/less.png" alt="Bouton Moins">
            </button>
            <button @click="$emit('moreA', aliment)" class="button">
                <img id="more" src="./icons/more.png" alt="Bouton Plus">
            </button>
        </div>
</template>

<style scoped>
.show {
    font-family: Arial, sans-serif;
    margin-top: 20px;
}

#delete, #more, #less {
    width: 20px;
    height: 20px;
}

#delete:hover, #more:hover, #less:hover {
  transform: scale(1.25); 
}
.button {
    border: none;
    background: none; 
    cursor: pointer;
    padding: 0; 
    margin-left:8px;
}
</style>

