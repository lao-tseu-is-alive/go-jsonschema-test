<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
button{
  margin: 1rem;
}
</style>

<template>
  <div class="hello">
    <h4>User id : {{ id }}</h4>
    <form>
      <div class="six columns">
        <label for="nameInput">name</label>
        <input class="u-full-width" type="text" v-model="user.name"
               placeholder="Please, enter your name here... " id="nameInput">
      </div>
      <div class="six columns">
        <label for="emailInput">email</label>
        <input class="u-full-width" type="email" v-model="user.email"
               placeholder="Please, enter your email here..." id="emailInput">
      </div>
      <div class="six columns">
        <label for="usernameInput">username</label>
        <input class="u-full-width" type="text" v-model="user.username"
               placeholder="Please, enter your username here... " id="usernameInput">
      </div>
      <div class="six columns">
        <label for="isAdminInput" class="u-pull-left">Is user Administrator ?</label>
        <input class="u-pull-right" type="checkbox" v-model="user.username"
               placeholder="Please, enter your username here... " id="isAdminInput">
      </div>
      <button @click.prevent="save" class="button-primary">SAVE</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'User',
  props: {
    id: { type: Number, default: 0 },
  },
  data() {
    return {
      user: {
        id: 0, name: '', email: '', username: '', is_admin: false,
      },
    };
  },
  methods: {
    save() {
      this.$emit('save', this.user);
    },
  },
};
</script>
