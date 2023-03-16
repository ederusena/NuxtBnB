<template>
  <div>
    <div style="display: flex">
      <img
        v-for="image in home.images"
        :key="image"
        style="width: 200px; margin: 2px"
        :src="image"
        alt="something"
      />
      <br />
    </div>
    {{ home.title }}<br />
    ${{ home.pricePerNight }} / night<br />
    <img src="/images/marker.svg" width="20" height="20" />{{
      home.location.address
    }}
    {{ home.location.city }} {{ home.location.state }} {{ home.location.country
    }}<br />
    <img src="/images/star.svg" width="20" height="20" />{{ home.reviewValue
    }}<br />
    {{ home.guests }} guests, {{ home.bedroomsguests }} rooms,
    {{ home.beds }} beds, {{ home.bathrooms }} bath<br />
    <div ref="map" class="h-[800px] w-[800px]"></div>
  </div>
</template>

<script>
import homes from '@/data/homes.json'

export default {
  data() {
    return {
      home: {},
    }
  },
  head() {
    return {
      title: this.home.title,
      script: [
        {
          src: `https://maps.googleapis.com/maps/api/js?key=${process.env.GOOGLE_API}&Libraries=places`,
          hid: 'map',
          defer: true,
        },
      ],
    }
  },
  mounted() {
    const mapOptions = {
      zoom: 18,
      center: new window.google.maps.LatLng(
        this.home._geoloc.lat,
        this.home._geoloc.lng
      ),
      disableDefaultUI: true,
      zoomControl: true,
    }
    const map = new window.google.maps.Map(this.$refs.map, mapOptions)
    const position = new window.google.maps.LatLng(
      this.home._geoloc.lat,
      this.home._geoloc.lng
    )

    const marker = new window.google.maps.Marker({
      position,
      map,
      title: this.home.title,
    })

    marker.setMap(map)
  },
  created() {
    const home = homes.find((home) => home.objectID === this.$route.params.id)
    this.home = home
  },
}
</script>

<style lang="scss" scoped></style>
