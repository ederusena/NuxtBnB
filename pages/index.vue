<template>
  <div>
    <div
      v-for="home in homes"
      :key="home.objectID"
      style="float: left; margin: 10px"
    >
    <!-- Prefetch foi desativado no nuxt.config.js  no-prefetch-->
      <NuxtLink :to="`/home/${home.objectID}`" >
        <HomeCard :home="home" />
      </NuxtLink>
    </div>
  </div>
</template>

<script>
import homes from '@/data/homes.json'

export default {
  data() {
    return {
      homes: homes.slice(0, 3),
    }
  },
  head() {
    return {
      title: 'HomePage',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'This is the home page',
        },
      ],
    }
  },
}
</script>
