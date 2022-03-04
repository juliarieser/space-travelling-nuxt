<template>
  <div class="container flow flex crew">
    <h1 class="numbered-title"><span>01</span> Pick your Destination</h1>
    <div v-if="member" class="img-container flex">
      <img class="member-picture" :src="member['webp-image'].guid" alt="" />
    </div>
    <div class="dot-indicators flex">
      <button
        v-for="(item, index) in crew"
        :key="index"
        @click="setMember(index)"
      ></button>
    </div>
    <div class="container flex member-info" v-if="member">
      <div class="uppercase ff-serif member-role">{{ member['role'] }}</div>
      <div class="uppercase ff-serif fs-700 member-name">
        {{ member['crew-name'] }}
      </div>
      <p class="text-accent">{{ member.bio }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      destinations: [],
    }
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/destination'
      )
      this.destinations = await response.json()
    },
  },
  mounted() {
    this.loadData()
    document.body.style.backgroundImage =
      "url('background-destination-mobile.jpg')"
  },
}
</script>

<style scoped>
.numbered-title {
  font-size: 16px;
}
</style>
