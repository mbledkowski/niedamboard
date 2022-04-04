<template>
  <article>
    <!--Title-->
    <header>
      <h2>λ hsp.sh /whois</h2>
    </header>
    <!--Content-->
    <section>
      <div v-for="(data, index) in dataArray" :key="index">
        <h3 v-if="index === 0">[ now ]</h3>
        <h3 v-else>[ last 8 hours ]</h3>
        <p>
          <span v-if="data.headcount === -1">?</span>
          <span v-else>{{ data.headcount }}</span> people:
          <span class="accent">[</span>
          <span v-for="(user, index) in data.users" :key="user">
            "{{ user }}"
            <span v-if="index + 1 !== data.users.length">,</span>
          </span>
          <span class="accent">]</span>
          <br />and
          <a v-if="index === 0" href="https://whois.at.hsp.sh/devices">
            <span v-if="data.unknown_devices === -1">?</span>
            <span v-else>{{ data.unknown_devices }}</span> unknown devices
          </a>
          <span v-else href="https://whois.at.hsp.sh/devices">
            <span v-if="data.unknown_devices === -1">?</span>
            <span v-else>{{ data.unknown_devices }}</span> unknown devices
          </span>
        </p>
      </div>
    </section>
    <footer>
      <p>
        site:
        <a class="accent" href="https://whois.at.hsp.sh/">whois.at.hsp.sh</a>
      </p>
    </footer>
  </article>
</template>

<script lang='ts'>
import { defineComponent } from "vue"

interface Props {
  dataArray: {
    headcount: number,
    users: Array<string>,
    unknown_devices: number,
  }[],
}

export default defineComponent({
  name: "hspWhois",
  data(): Props {
    return {
      dataArray: [{
        headcount: -1,
        users: [],
        unknown_devices: -1,
      },
      {
        headcount: -1,
        users: [],
        unknown_devices: -1,
      }]
    }
  },
  mounted() {
    this.fetchData()
    setInterval(() => {
      this.fetchData()
    }, 12000)
  },
  methods: {
    fetchData() {
      fetch("https://whois.at.hsp.sh/api/now").then(res => res.json()).then(res => this.dataArray[0] = res)
      fetch("https://whois.at.hsp.sh/api/now?hours=8").then(res => res.json()).then(res => this.dataArray[1] = res)
    }
  }
})
</script>

<style lang="scss">
</style>