<template>
  <v-card
    class="mx-auto"
    max-width="700"
  >
    <v-img
      class="white--text align-end"
      height="200px"
      src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
    >
      <v-card-title dir="rtl">דווח על אירוע חדש</v-card-title>
    </v-img>

    <v-card-subtitle dir="rtl" class="pb-0">דיווח</v-card-subtitle>

    <v-card-text class="text--primary">
      <v-container>
      <v-layout row>
        <v-flex dir="rtl" md6 style="padding: 10px;">
          <v-text-field dir="rtl" required label="כותרת" v-model="name" ></v-text-field>
          <v-text-field dir="rtl" required label="פירוט" v-model="description"></v-text-field>
          <v-text-field dir="rtl" required label="Latitude" v-model="lat"></v-text-field>
        </v-flex>
        <v-flex md6 style="padding: 10px;">
          <v-text-field dir="rtl" required label="Longitude" v-model="lon"></v-text-field>
      <v-select
          :items="items"
          label="סוג האירוע"
          v-model="eventType"
        ></v-select><br />
        <v-slider dir="rtl"
        label="מספר משתתפים"
          min="1"
          max="50"
          v-model="slider"
          thumb-label="always"
        ></v-slider>
        </v-flex>
      </v-layout> 
    </v-container>
    </v-card-text>

    <v-card-actions dir="rtl">
      <v-btn color="green" @click="sendReport">
        שלח דיווח
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
    data() {
        return {
            items: [
                'פיגוע דקירה',
                'תאונת דרכים',
                'שריפה',
                'פיגוע ירי'
            ],
            eventType: '',
            lat: '',
            lon: '',
            name: '',
            description: '',
            slider: 0
        }
    },
    methods: {
        sendReport() {
            this.$socket.emit('new_event', "13:05:20, 13.5.20", this.name, this.lat, this.lon, this.eventType, this.slider, this.description);
            this.eventType = '';
            this.lat = '';
            this.lon = '';
            this.name = '';
            this.description = '';
            this.slider = 0;
            this.$router.push('/')
            //this.$socket.emit('new_event', JSON.stringify({timestamp: "13:05:20, 13.5.20", name: this.name, latitude: this.lat, longitude: this.lon, type_id: this.eventType, num_participants: this.slider, description: this.description}));
            //console.log([this.eventType, this.name, this.description, this.lat, this.lon, this.slider])
        }
    }
}
</script>

<style>

</style>