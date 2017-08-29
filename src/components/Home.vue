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
            placeholder="Ronaldo Fenômeno" 
            required
            v-model="name" 
          />
        </div>
      </div>
      <div class="row justify-center">
        <div class="col-12">
          <q-btn @click="addPlayer">Adicionar</q-btn>
          <q-btn @click="getPlayers">Recarregar</q-btn>
        </div>
      </div>
      <hr>
      <div class="row">
        <div class="col-12">
          <q-list highlight>
          <q-list-header>Jogadores</q-list-header>
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
  QItem
  // LocalStorage
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
    QItem
    // LocalStorage
  },
  data () {
    return {
      name: '',
      players: []
    }
  },
  computed: {
  },
  methods: {
    launch (url) {
      openURL(url)
    },
    addPlayer () {
      if (localStorage.players === undefined) {
        localStorage.setItem('players', '')
      }

      let players = localStorage.players.split(',')

      players.pop(this.name)
      console.log(players, this.name)
      localStorage.setItem('players', players.join())

      this.getPlayers()
    },
    getPlayers () {
      this.players = localStorage.players
      console.log(this.players)
    }
  }
}
</script>

<style lang="stylus">
  .content
    margin 1rem
</style>
