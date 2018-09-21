
<template>
  <div>
    <article v-for="(locations, idx) in locations" :key="idx">
    <img :src="locations.images">
    <h1>{{ locations.name }}</h1>
     </article>
  <form @submit="addLocation(name, images)">
    <input v-model="name" placeholder="Location Name">
    <input v-model="images" placeholder="Location Image URL">
    <button type="submit">Add New Location</button>
    <button @click="deleteLocation(locations.id)">
  </button>
  </form>
  </div>
</template>

<script>
import { db } from '../main'
export default {
  data () {
    return {
      locations: [],
      name: '',
      images: ''
    }
  },
  firestore () {
    return {
      locations: db.collection('locations').orderBy('createdAt')
    }
  },
  methods: {
    addLocation (name, images) {
      const createdAt = new Date()
      db.collection('locations').add({ name, images, createdAt })
    },
    deleteLocation (id) {
      db.collection('locations').doc(id).delete()
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
