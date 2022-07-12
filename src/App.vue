<template>

  <div id="app">

    <header>
      <PageHeader/>
    </header>

    <main>
      <MainSection/>
    </main>

  </div>

</template>

<script>

  import PageHeader from './components/PageHeader.vue';
  import MainSection from './components/MainSection.vue';

  export default {
    name: 'App',
    components: { PageHeader, MainSection }
  }

</script>

<style lang="scss">

   @import "./style/common.scss";

</style>
