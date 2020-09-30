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
      <div class="row">
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
      </div>
      <div class="row">
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
      </div>
      <div class="twelve columns">
      <button @click.prevent="save" class="button-primary">SAVE</button>
      <button @click.prevent="checkDataValidation" class="button-primary">VALIDATE</button>
      </div>
    </form>
    <div class="twelve columns">
      <template v-if="isValid">
        DATA IS VALID !
      </template>
      <template v-else>
        DATA IS INVALID ! {{errMessage}}
      </template>
    </div>
  </div>
</template>

<script>
import Ajv from 'ajv';

const ajv = new Ajv();
const userSchema = require('./gouser.schema.json');
// const userValidation = ajv.compile(userSchema);
let userValidation = null;

export default {
  name: 'User',
  props: {
    id: { type: Number, default: 0 },
  },
  data() {
    return {
      isValid: false,
      errMessage: '',
      user: {
        id: 0, name: '', email: '', username: '', is_admin: false,
      },
    };
  },
  mounted() {
    this.user.id = this.id; // get initial id property
    console.log('userSchema', userSchema);
    if (ajv.validateSchema(userSchema)) {
      console.log('Schema is valid !');
      userValidation = ajv.compile(userSchema);
    } else {
      console.warn('Schema is invalid !');
      console.warn(ajv.errors);
    }
  }, // end of mounted
  methods: {
    save() {
      this.$emit('save', this.user);
    },
    checkDataValidation() {
      if (userValidation(this.user)) {
        console.log('DATA IS VALID');
        this.isValid = true;
        console.log(JSON.stringify(this.user, null, 2));
      } else {
        console.warn('DATA IS INVALID');
        this.isValid = false;
        console.log(JSON.stringify(this.user, null, 2));
        const err = userValidation.errors[0];
        console.log(JSON.stringify(err, null, 2));
        this.errMessage = `${err.dataPath} : ${err.message}`;
      }
    },
  }, // end of methods
};
</script>
