<template>
    <body>
        <div class="footer">
            <div class="left">
                <h2>Merci d'utiliser le frigo de Camille!</h2>
                <p>Vous voulez vous regaler avec vos aliments? Regardez les recettes Marmiton!</p>
            </div>
            <div class="right">
                <p>Liste de recettes Marmiton</p>
                <ul>
                    <li><a href="https://www.marmiton.org/recettes/recette_tarte-aux-pommes_18588.aspx" target="_blank">Tarte aux pommes</a></li>
                    <li><a href="https://www.marmiton.org/recettes/recette_gratin-de-brocolis-facile_18753.aspx" target="_blank">Gratin de brocolis</a></li>
                    <li><a href="https://www.marmiton.org/recettes/recette_poulet-basquaise_16969.aspx" target="_blank">Poulet basquaise</a></li>
                </ul>
            </div>
        </div>
    </body>
</template>
  
<style scoped>
.footer {
    background: rgb(50, 50, 50);
    padding-top: 10px;
    font-family: Arial, sans-serif;
    font-size: 15px;
    color: bisque;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.left {
    text-align: center;
    padding-left: 70px;
    flex: 1;
}

.right {
    flex: 1;
    padding-left:150px;
}

a {
    color: bisque;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}
</style>
  