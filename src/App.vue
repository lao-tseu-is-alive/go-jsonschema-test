<style lang="scss">

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 1rem;
  fieldset{
    border: solid 1px black;
    padding: 1.5rem;
  }
}
</style>

<template>
  <div class="container">
    <fieldset>
      <legend>User Form</legend>
      <user :id="1" @save="saveHandler"/>
    </fieldset>
  </div>
</template>

<script>
import user from './components/gouser/User.vue';
import './assets/skeleton.min.css';

export default {
  name: 'App',
  components: {
    user,
  },
  methods: {
    saveHandler(data) {
      console.log(data);
    },
  },
};
</script>
