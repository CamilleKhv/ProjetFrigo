<script setup>
import { reactive, onMounted } from "vue";
import aliment from "../aliment.js";
import FrigoItem from "./FrigoItem.vue";
import FrigoForm from "./FrigoForm.vue";
import FrigoSearch from "./FrigoSearch.vue";


const listeA = reactive([]);
const rechercheA = reactive([])
// -- l'url de l'API
const url = "https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/15/produits";


// -- req AJAX pour récupérer les aliments
//    et les stocker dans le state listeA
function getAliments() {
  const fetchOptionsget = { method: "GET" };
  fetch(url, fetchOptionsget)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      let textHTML = ""
      // -- vider la liste des aliments
      listeA.splice(0, listeA.length);
      // pour chaque donnée renvoyée par l'API
      //  créer un objet instance de la classe aliment
      //  et l'ajouter dans la liste listeA
      dataJSON.forEach((v) => listeA.push(new aliment(v.id, v.nom, v.qte, v.photo)));
    })
    .catch((error) => console.log(error));
}


// -- handle pour supprimer une chose à partir de l'id de l'aliment
function handlerDelete(id) {
  console.log(id);
  const fetchOptionsdelete = {
    method: "DELETE",
  };
  // -- l'id de l'aliment à supprimer doit être
  //  ajouté à la fin de l'url
  fetch(url + "/" + id, fetchOptionsdelete)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getAliments();
      handlerSearch(); // si l'aliment est supprimé dans la recherche, il est supprimé aussi de l'API
    })
    .catch((error) => console.log(error));
}


// -- handle pour ajouter une nouvelle chose à partir du libelle saisi dans le formulaire
function handlerAdd(nom, qte, photo) {
  console.log(nom);
  console.log(qte);
  console.log(photo);

  // fenetre pop-up si le nom et/ou la qte incorrecte(s)
  if (nom === "") {
    console.error("Le nom de l'aliment ne peut pas être vide.");
    alert("Le nom de l'aliment ne peut pas être vide.");
    return;
  }

  if (qte < 1 || qte === null) {
    console.error("La quantité ne peut pas être négative ou nulle.");
    alert("La quantité ne peut pas être négative ou nulle.");
    return;
  }

  let photoUrl;
  // si l'aliment fait partie de l'API de base, alors la photo est ajoutée automatiquement
  if (nom === "lait" || nom === "Tomates" || nom === "Jambon") {
    photoUrl = "https://webmmi.iut-tlse3.fr//~pecatte//frigo//public//images//" + nom;
  } else {
    photoUrl = photo;
  }
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptionspost = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify({ nom: nom, qte: qte, photo: photoUrl }),
  };
  fetch(url, fetchOptionspost)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getAliments();
    })
    .catch((error) => console.log(error));
}


// handle pour rechercher avec un mot clef
function handlerSearch(mot) {
  console.log(mot);
  const fetchOptions = {
    method: "GET"
  }
  fetch(url + "?search=" + mot, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      rechercheA.splice(0, rechercheA.length);
      // si la recherche est vide, alors rien n'est affiché
      if (mot === "") {
        rechercheA.value = [];
      } else {
        dataJSON.forEach((v) => rechercheA.push(new aliment(v.id, v.nom, v.qte, v.photo)));
        // pas de résultat
        /*if (rechercheA.length === 0) {
          console.error("Aucun résultat");
          //alert("Aucun résultat.");
        }*/
      }
    })
    .catch((error) => console.log(error));
}


// handle pour ajouter une quantité
function handlerMore(al) {
  console.log(al);
  al.augmenterStock();

  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({ id: al.id, nom: al.nom, qte: al.qte, photo: al.photo }),
  };
  fetch(url, fetchOptions)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON);
      getAliments();
    })
    .catch((error) => console.log(error));
}


// handler pour enlever une quantité
function handlerLess(al) {
  console.log(al);
  al.enleverStock();
  // si la quantité est nul ou négative, alors on supprime l'aliment
  if (al.qte < 1) {
    handlerDelete(al.id);
  } else {
    let myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    const fetchOptions = {
      method: "PUT",
      headers: myHeaders,
      body: JSON.stringify({ id: al.id, nom: al.nom, qte: al.qte, photo: al.photo }),
    };
    fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        getAliments();
      })
      .catch((error) => console.log(error));
  }

}

// -- fonction du cycle de vie du composant
// exécutée 1 seule fois à la création
onMounted(() => {
  getAliments();
});
</script>


<template>
  <h1 class="frigoTitle">Mon frigo</h1>
  <div class="item">
    <h3>Liste des aliments présents</h3>
    <ul>
      <FrigoItem v-for="aliment of listeA" 
      :key="aliment.id" 
      :aliment="aliment" 
      @deleteA="handlerDelete"
      @lessA="handlerLess" 
      @moreA="handlerMore" />
    </ul>
    <FrigoForm @addA="handlerAdd" />
  </div>
  <div class="search">
    <FrigoSearch @searchA="handlerSearch" />
    <ul>
      <FrigoItem v-for="aliment of rechercheA" 
      :key="aliment.id" 
      :aliment="aliment" 
      @deleteA="handlerDelete"
      @lessA="handlerLess" 
      @moreA="handlerMore" />
    </ul>
  </div>
</template>


<style scoped>
.frigoTitle {
  position: absolute;
  padding-top: 70px;
  left: 20vw;
}

.frigoTitle:hover {
  animation: fondre 5s ease-in-out infinite;
}

.item {
  margin-left: auto;
  margin-right: 30px;
  padding-top: 7px;
  padding-bottom: 7px;
  width: 50%;
  height: 100%;
  background: rgba(129, 186, 189, 0.8);
  border-radius: 50px;
  text-align: center;
  padding-bottom: 20px;
}

.search {
  position: sticky;
  bottom: 0;
  left: 10px;
  width: 400px;
  background: rgb(130, 177, 177);
  border-radius: 60px;
  text-align: center;
}


@keyframes fondre {
  0% {
    transform: scaleY(1);
  }

  25% {
    transform: scaleY(0.8) skewY(5deg);
    color: orange;
  }

  50% {
    transform: scaleY(1.2) skewY(-5deg);
    color: rgb(159, 202, 204);
  }
}
</style>