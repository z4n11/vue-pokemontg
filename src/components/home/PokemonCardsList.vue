<template>
  <div :class="$style.pokemonListLayout">
    <div
      v-for="pokemonCard in searchPokemons"
      :key="pokemonCard.id"
    >
      <PokemonCard :pokemonData="pokemonCard" />
    </div>
  </div>
</template>

<script>
import PokemonCard from './PokemonCard.vue'
import { mapState } from 'vuex'
export default {
  components: {
    PokemonCard
  },
  props: {
    searchData: {
      type: String,
      required: true
    }
  },
  computed: {
    ...mapState(['pokemonCards']),
    searchPokemons () {
      if (this.pokemonCards.length > 0) {
        return this.pokemonCards.filter(
          pokemonCard =>
            !this.searchData ||
            pokemonCard.name.toLowerCase().includes(this.searchData.toLowerCase()) ||
            pokemonCard.types.map(type => type.toLowerCase()).includes(this.searchData.toLowerCase())
        )
      } else {
        return []
      }
    }
  }
}
</script>

<style lang="scss" module>
.pokemonListLayout {
  display: flex;
  flex-wrap: wrap;
  overflow: auto;
  justify-content: center;
}
.listBackground {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
