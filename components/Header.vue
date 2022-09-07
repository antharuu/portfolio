<template>
  <div class="header">
    <h1>Antharuu</h1>
    <div class="header__info-panels">

      <template v-for="(panel, index) in panels">
        <div class="panel-container" @mouseenter="setActivePanel(index)" @mouseleave="switchPanelInterval">
          <InfoPanel :isActive="activePanel === index" :name="panel.title" :emoji="panel.emoji">
            {{ panel.descr }}
          </InfoPanel>
        </div>
      </template>

    </div>
  </div>
</template>

<script>

const nbPanels = 4
let i = null

export default {
  name: 'Header',
  data: () => {
    return {
      panels: [
        {
          title: 'Grand maître CSS',
          emoji: '🎨',
          descr: 'Véritable Van Gogh du CSS, mon intégration est impeccable et mon code optimisé. Par contre, pour ce qui est de la conception graphique, c\'est plus proche de Picasso.'
        },
        {
          title: 'Paladin de l\'Ordre du PHP',
          emoji: '🐘',
          descr: 'L\'ordre du PHP a besoin de tous notre soutien. Les temps sont durs et l\'Empire JS prend le pouvoir !'
        },
        {
          title: 'Roi slime',
          emoji: '👑',
          descr: 'Je gère et m\'occupe de la communauté de création du jeu vidéo appelée "Jardin des devs", tous réuni sur un serveur discord créé par mes soins.'
        },
        {
          title: 'Auteur trop ambitieux',
          emoji: '🦋',
          descr: 'J\'ai depuis des années comme projet d\'écrire mon roman et visual novel, mais il est clair que je suis trop ambitieux pour le temps et le talent que j\'ai.'
        },
      ],
      activePanel: 0
    }
  },
  methods: {
    switchPanelInterval () {
      i = setInterval(() => {
        this.activePanel++
        if (this.activePanel > nbPanels) {
          this.activePanel = 1
        }
      }, 3000)
    },
    setActivePanel (panelID) {
      clearInterval(i)
      this.activePanel = panelID
    }
  },
  mounted () {
    this.switchPanelInterval()
  }
}
</script>

<style lang="scss">

html, body {
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
