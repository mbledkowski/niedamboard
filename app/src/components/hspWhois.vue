<template>
  <!--Title-->
  <h2>λ hsp.sh /whois</h2>
  <!--Content-->
  <p>{{ data.headcount }} people: <span class="accent">[</span>
    <span v-for="(user, index) in data.users" :key="user">"{{user}}"<span v-if="index+1 !== data.users.length">, </span></span>
    <span class="accent">]</span>
  <br> and <a href="https://whois.at.hsp.sh/devices">{{data.unknown_devices}} unknown devices</a>
  </p>
  <p>site: <a class="accent" href="https://whois.at.hsp.sh/">whois.at.hsp.sh</a></p>
</template>

<script lang='ts'>
import { defineComponent } from "vue"

interface Props {
  data: {
    headcount: number,
    users: Array<string>,
    unknown_devices: number,
  }
}

export default defineComponent({
  name: "hspWhois",
  data(): Props {
    return {
      data: {
        headcount: 0,
        users: [],
        unknown_devices: 0,
      }
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      await fetch("https://whois.at.hsp.sh/api/now").then(res => res.json()).then(res => this.data = res)
    }
  }
})
</script>

<style lang="scss">
</style>