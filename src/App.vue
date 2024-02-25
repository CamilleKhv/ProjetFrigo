<script setup>
import FrigoHeader from "./components/FrigoHeader.vue";
import FrigoFooter from "./components/FrigoFooter.vue";
import Frigo from "./components/Frigo.vue";

const scrollToFeatures = () => {
  const featuresElement = document.querySelector(".features");
  featuresElement.scrollIntoView({ behavior: 'smooth' });
};

</script>

<template>
  <body>
    <div class="header">
      <FrigoHeader />
      <div class="scroll">
        <button class="fonction" @click="scrollToFeatures">
          <img id="click" src="./components/icons/click.png" title="Découvrez toutes les fonctionalités!">
        </button>
      </div>
    </div>
    <div class="features">
      <Frigo />
    </div>
    <div class="footer">
      <FrigoFooter />
    </div>
  </body>
</template>


<style>
body {
  margin: auto;
  background-color: rgb(50, 50, 50);
  font-family: Arial, sans-serif;
}


.header {
  background-image: url('components/icons/kitchen.jpg');
  background-size: cover;
  width: 100%;
  height: 110vh;
  background-position: center;
}


.scroll {
  margin-top: -33vh;
  margin-left: 14vw;
}


#click {
  width: 8vw;
}


.fonction {
  border: none;
  background: none;
  cursor: pointer;
  padding: 0;
  animation: moveUpDown 2s ease-in-out infinite;
}


.features {
  margin: 0px;
  background-image: url('components/icons/fridge2.jpg');
  background-repeat: no-repeat;
  background-position: left;
  background-color: rgb(159, 202, 204);
  height: 180%;
  width: 100vw;
  transition: background-image 0.5s ease-in-out;
  padding-bottom: 10px;
}


.features:hover {
  background-image: url('components/icons/fridge.jpg');
  background-size: auto;
  background-color: rgb(159, 202, 204);
}


@keyframes moveUpDown {
  0% {
    transform: translateY(-10px);
  }

  50% {
    transform: translateY(10px);
  }

  100% {
    transform: translateY(-10px);
  }
}

</style>