<template>
  <build-main>
    <template v-slot:aside>
      <menu-asite></menu-asite>
    </template>
    <template v-slot:main>
      <app-search></app-search>
      <router-view></router-view>
    </template>
  </build-main>
    
  
  
</template>

<script>
import MenuAsite from '../components/MenuAsite'
import BuildMain from '../components/BuildMain'
import Search from '../components/Search'
//import Dictionary from '../components/Dictionary'

export default {
  name: 'Home',
  components: {
    'menu-asite': MenuAsite,
    'build-main': BuildMain,
    'app-search': Search,
    //'dictionary': Dictionary,
  }
}
</script>
<style lang="sass" scoped>

</style>
