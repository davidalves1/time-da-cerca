<template>
  <q-layout ref="layout" view="lHh Lpr fff">
    <q-toolbar color="positive">
      <q-toolbar-title>Time da Cerca</q-toolbar-title>
    </q-toolbar>
    <div class="content">
      <div class="row">
        <div class="col-12">
          <q-input 
            type="text" 
            stack-label="Nome do jogador" 
            placeholder="Ex: Ronaldo Fenômeno" 
            required
            v-model="name" 
          />
        </div>
      </div>
      <div class="row text-center">
        <div class="col-12">
          <q-btn @click="addPlayer">Adicionar</q-btn>
        </div>
      </div>
      <q-item-separator />
      <div class="row options text-center">
        <div class="col-12">
          <q-btn @click="getPlayers">Jogadores</q-btn>
          <q-btn @click="sortTeams">Sortear Times</q-btn>
        </div>
      </div>
      <div class="row">
        <div class="col-12" v-if="showPlayers">
          <q-list highlight>
            <q-list-header>Jogadores</q-list-header>
            <q-item-separator />
            <q-item v-for="player in players" :key="name.id">
              {{player}}
            </q-item>
          </q-list>
        </div>
        <div class="col-12" v-if="showTeams">
          <q-list highlight>
            <q-list-header>Times</q-list-header>
            <q-item-separator />
            <q-item v-for="player in players" :key="name.id">
              {{player}}
            </q-item>
          </q-list>
        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
import {
  // event,
  openURL,
  QInput,
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItemSeparator,
  QItem,
  Toast,
  LocalStorage
} from 'quasar'

export default {
  name: 'index',
  components: {
    QInput,
    QLayout,
    QToolbar,
    QToolbarTitle,
    QBtn,
    QIcon,
    QList,
    QListHeader,
    QItemSeparator,
    QItem,
    Toast,
    LocalStorage
  },
  data () {
    return {
      name: '',
      players: [],
      teams: [],
      showPlayers: true,
      showTeams: false
    }
  },
  mounted () {
    this.getPlayers()
  },
  computed: {
  },
  methods: {
    launch (url) {
      openURL(url)
    },
    addPlayer () {
      if (this.name === '' || this.name === undefined) {
        Toast.create.negative('Informe um nome para o jogador')
        return
      }

      if (localStorage.getItem('players') === null) {
        localStorage.setItem('players', this.name)
        this.getPlayers()
        return
      }

      let players = localStorage.getItem('players')

      players = players.split(',')

      players.push(this.name)
      localStorage.setItem('players', players)

      this.getPlayers()
      this.name = ''
    },
    getPlayers () {
      let players = localStorage.getItem('players')

      if (players === null || players === undefined) {
        this.players = ['Nenhum jogador na lista']
        return
      }

      this.players = players.split(',')

      this.showPlayers = true
      this.showTeams = false

      return this.players
    },
    sortTeams () {
      this.showTeams = true
      this.showPlayers = false

      let lista = [1, 2, 3, 4, 5, 6, 7, 8, 9]
      let lista2 = lista.sort(() => Math.random() - 0.5)

      console.log(lista2)
    }
  }
}
</script>

<style lang="stylus">
  .content
    margin 1rem

  .options
    margin 1rem auto
</style>
