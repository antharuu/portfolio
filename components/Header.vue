<template>
  <div class="header">
    <h1>Antharuu</h1>
    <div class="header__info-panels">

      <div class="panel-container">
        <InfoPanel :isActive="activePanel.current === 1" name="Grand maître CSS 🎨"
                   @mouseenter="setActivePanel(1)" @mouseleave="switchPanelInterval"
        >Véritable Van Gogh du CSS, mon intégration est
          impeccable et mon code optimisé. Par contre, pour ce qui est de la conception graphique, c'est plus proche de
          Picasso.
        </InfoPanel>
      </div>

      <div class="panel-container">
        <InfoPanel :isActive="activePanel.current === 2" name="Paladin de l'Ordre du PHP 🐘"
                   @mouseenter="setActivePanel(2)" @mouseleave="switchPanelInterval">L'ordre du PHP a besoin de tous
          notre
          soutien. Les temps sont durs et
          l'Empire JS prend le pouvoir !
        </InfoPanel>
      </div>

      <div class="panel-container">
        <InfoPanel :isActive="activePanel.current === 3" name="Roi slime 👑"
                   @mouseenter="setActivePanel(3)" @mouseleave="switchPanelInterval">Je gère et m'occupe de la
          communauté
          de création du jeu vidéo appelée
          "Jardin des devs", tous réuni sur un serveur discord créé par mes soins.
        </InfoPanel>
      </div>

      <div class="panel-container">
        <InfoPanel :isActive="activePanel.current === 4" name="Auteur trop ambitieux 🦋"
                   @mouseenter="setActivePanel(4)" @mouseleave="switchPanelInterval">J'ai depuis des années comme projet
          d'écrire mon roman et visual novel,
          mais il est clair que je suis trop ambitieux pour le temps et le talent que j'ai.
        </InfoPanel>
      </div>

    </div>
  </div>
</template>

<script setup>

import {defineNuxtComponent} from "nuxt/app";

defineNuxtComponent({
  name: "Header"
});

const nbPanels = 4;

let activePanel = reactive({current: 0})

let i = null;

function switchPanelInterval() {
  i = setInterval(() => {

    activePanel.current++;
    if (activePanel.current > nbPanels) {
      activePanel.current = 1;
    }
  }, 3000)
}

switchPanelInterval()

function setActivePanel(panelID) {
  clearInterval(i)
  activePanel.current = panelID;
}

</script>

<style lang="scss">
@import "~/assets/css/base.scss";

html, body{
  background-color: $c-white;
  color: $c-black;
}

.header {
  user-select: none;
  width: 100vw;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  h1 {
    font-size: clamp(12px, 10vw, 92.38px);
    line-height: .5em;
    text-transform: uppercase;
  }

  &__info-panels {
    @media screen and (min-width: $bp-md) {
      gap: 1em;
      row-gap: 0;
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: center;
    }
  }
}
</style>
