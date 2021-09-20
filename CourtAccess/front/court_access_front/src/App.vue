<template>


                                                  <!-- A Faire prochainement:
                                                  retirer player au besoin
                                                  SetItem plusieurs fois
                                                  tableau en 2 colonnes -->


 <!-- EXAMPLE::: Ici j importe Hello world<HelloWorld msg="Welcome to Your Vue.js App"/> -->
<!-- Ce que je veux: 
  Application faite pour les Personnes Non Adepte des technologies, DOnc doit etre Ultras Simplifie:
  App Pour Dispastcher les jouers sur terrains de tennis en double( Option par la suite pour simple?)
On enregistre les joueurs(Prenom + nom?, prenom seulement?,a terme peut aller piocher dans base de donnees avbec numero de license, donc faire apparatire Photo?)
pour les dispatcher: dabord dans un tableau, pour avoir une vue d ensemble( ou faire poper une fenetre ) (Selon quel ordre?)
et sur des terrains de tennis(designer) donc: en mode aleatoire. 
a noter que les noms peuvent survoler le terrain comme dans un double
on peut retirer et rajouter du monde a tout moment
et il faut un boutton , qui a une verification(Vous etes sur?) permettant de formater donnees.
Passer de l anglais au Francais
-->

<!-- Plan: 
0. Se logger en tant qu admin. ( poser la question a l admin si veut jouer!)
1. Formulaire: Tout en haut ( ou s enregistre les donnees? MySql car par la suite on peut lier avec des photos , des stats ...SCALABLE)
2. Tableau des joueurs sur 2 colones qui se remplissent l'une puis l autre pour avoir un equilibre
3. Joueur peut etre supprimer(animation comme iphone? glisser 
4. alert: "Vous etes sur de vouloir melanger? oui || non "



sur la gauche Ou au clique donnees apparaissent, comme (Veut jouer en simple, ne joue pas cette manche))
3. Un bouton "Melanger"
4. Terrain de tennis (une image, legerement 3d?) Varie en fonction du nombre de joueur, doit prendre en compte simple et impaire (joueur qui ne jouera pas)
5. Bouton "formater", avec (vous etes  sur)
-->
<div class="main">

         <div id="app" @keydown.enter="saveName">
  <p>
    <!-- ICI  retirer v-model=name dans le input-->
    Nom du Joueur <input  id="name">.
  </p>
  <p>
    <button @click="saveName">Sauver</button>
  </p>
 <table  class="tablePlayers">
        <tr class="tablePlayers_title">Nom Des Joueurs
          <th></th>
          <td id="listName"></td>
        </tr>
      </table>   

  <p><button @click="clear">Clear</button></p>
</div>






<!-- 
               <table class="textShadow profileInfo__table">
        <tr>
          <th>Prénom:</th>
          <td>{{ firstName }}</td>
        </tr>
        <tr>
          <th>Nom:</th>
          <td>{{ lastName }}</td>
        </tr>
        <tr>
          <th>Date d'inscription:</th>
          <td v-if="createdAt"> {{ createdAt.split("-")[2].split("T")[0] }}/{{ createdAt.split("-")[1] }}/{{ createdAt.split("-")[0] }}</td>
        </tr>
      </table>      -->

</div>

 
</template>

<script>
// EXAMPLE::: Import avec HELLO WORLD
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
     data () {
        return {
     name: ''
        }
      },
  beforeMount() {
        if (localStorage.getItem('player'))
            this.player = JSON.parse(localStorage.getItem('player'));
  },

  methods: {

    saveName() {
      if(localStorage.getItem('player') ==null){
        localStorage.setItem('player', '[]');
      }
    let newPlayer = document.getElementById('name').value;
    
    let oldPlayer = JSON.parse(localStorage.getItem('player'));

    let mydiv = document.getElementById("listName");
    let newcontent = document.createElement('div');
   
     // COMPARER DANS TABLEAU ET METTRE ALERT POUR NE PAS AVOIR DE DOUBLONS ou de champ vide
     if(oldPlayer.includes(newPlayer) || newPlayer == ""){
       alert("Joueur deja existant");
     }else{
       oldPlayer.push(newPlayer);
      localStorage.setItem('player', JSON.stringify(oldPlayer));
      
      newcontent.innerHTML += newPlayer + "<br/>";
      while (newcontent.firstChild) {
     mydiv.appendChild(newcontent.firstChild);
     }
     }
    },
 

    clear() { 
      localStorage.clear();
      document.getElementById("listName").innerHTML = "";
    }
  }
}

</script>

<style scoped lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.tablePlayers{
  display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    flex-wrap: wrap;
    align-content: space-around;
    align-items: center;
    
    }
</style>
