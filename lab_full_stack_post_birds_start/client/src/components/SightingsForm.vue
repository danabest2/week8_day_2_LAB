<template lang="html">
	<form id="sightings-form">
		<h2>Add a Sighting</h2>
		<div class="formWrap">
			<label for="species">Species:</label>
			<input type="text" id="species" />
		</div>
		<div class="formWrap">
			<label for="location">Location:</label>
			<input type="text" id="location" />
		</div>
		<div class="formWrap">
			<label for="date">Date:</label>
			<input type="date" id="date" />
		</div>

		<input type="submit" value="Save" id="save"/>
	</form>
</template>

<script>
import { eventBus } from '@main.js'
import SightingsService from '@/services/SightingsService.js'

export default {
  name: "sightings-form",
  data() {
    return {
      species: '',
      location: '',
      date: null
    }
  },
methods: {
  addSighting(e) {
    e.preventDefault()
    const sighting = {
      species: this.species,
      location: this.location,
      date: this.date
    }
  }
  SightingsService.postSighting(sighting)
  .then(res => eventBus.$emit('sighting-added', res))
}
}
</script>

<style lang="css" scoped>
h2 {
	margin: 10px 0;
	padding: 0;
}

form {
	width: 75%;
	margin: 0 auto;
	background: rgba(255, 255, 255, 0.7);
	padding: 20px;
	margin-bottom: 40px;
}

label {
	min-width: 100px;
	display: inline-block;
}

.formWrap {
	margin-bottom: 10px;
}
</style>
