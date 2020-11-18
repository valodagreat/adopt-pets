<template>
  <div class="home">
    <h1>Adopt a New Best Friend</h1>
    <h4>Total pets available is {{animalCount}}</h4>
    <button class="btn btn-primary" @click="togglePetForm">
      Add New Pet
    </button>
    <b-container>
    <b-form @submit.prevent="onSubmit" v-if="showPetForm">
      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          required
          placeholder="Enter Pet's name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.species"
          :options="['cats','dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Gender:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.gender"
          :options="['male','female']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Breed:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.breed"
          required
          placeholder="Enter Pet's Breed"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Note or Attribute:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.notes"
          required
          placeholder="Enter Pet's note"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="number"
          v-model="form.age"
          required
          placeholder="Pet's Age"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Color:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.color"
          :options="['black','white','gray','brown']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Location:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.location"
          :options="['fourside','threed']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Weight:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="number"
          v-model="form.weight"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      form: {
        name: '',
        age: 0,
        species: null,
        color: null,
        gender: null,
        location: null,
        weight: 0,
        notes: '',
        breed: ''
      }
    }
  },
  computed: {
    ...mapGetters(['animalCount'])
  },
  methods: {
    ...mapActions(['addPet']),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    onSubmit () {
      const { species, name, age, color, gender, location, weight, notes, breed } = this.form
      const payload = {
        species,
        pet: {
          name,
          age,
          color,
          gender,
          location,
          weight,
          notes,
          breed
        }
      }
      this.addPet(payload)

      this.form = {
        name: '',
        age: 0,
        species: null
      }

      this.togglePetForm()
    }
  }
}
</script>

<style >
  .container{
    padding: 20px;
    padding-top: 30px;
  }
  form{
    max-width: 70vw !important;
  }
</style>
