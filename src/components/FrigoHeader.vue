<template>
  <div class="header">
    <div class="title">
      <h1>Mon frigo</h1>
      <p>Un petit creux? Découvrez ce que votre frigo contient</p>
    </div>
  </div>
</template>
  
<style scoped>
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.title {
  background: rgba(27, 28, 31, 0.9);
  border-radius: 50px;
  padding: 20px;
  font-family: Arial, sans-serif;
  color: bisque;
  text-align: center;
}


@keyframes go-down {
  0% {
    transform: translateY(0%);
  }
  100% {
    transform: translateY(100%);
    opacity: 0.2;
    filter: blur(5px)
  }
}

.title:hover {
  animation: go-down 3s ease-in-out infinite alternate;
}
</style>
