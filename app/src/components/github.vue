<template>
  <article>
    <!--Title-->
    <header>
      <h2>λ github /profile</h2>
    </header>
    <!--Content-->
    <section>
      <!--Image-->
      <img
        :src="dataArray[0].avatar_url"
        alt="{{dataArray[0].name}}'s GitHub profile picture"
        width="189"
      />
      <!--About-->
      <h3>[ about ]</h3>
      <p>
        {{ dataArray[0].name }}
        <span class="accent">@</span>
        {{ dataArray[0].login }}
        <br />
        {{ dataArray[0].bio }}
        <br />
        {{ dataArray[0].company }}; {{ dataArray[0].location }}
        <br />site:
        <a :href="`https://${dataArray[0].blog}`">{{ dataArray[0].blog }}</a>; hireable
        <span v-if="!dataArray[0].hireable" class="accent">n't</span>
        <br />
        {{ dataArray[0].followers }} followers; {{ dataArray[0].public_repos }} repos; {{ dataArray[0].public_gists }} gists
        <br />last activity:
        <span v-if="lastActivity === -1">?</span>
        <span v-else>{{ Math.floor(lastActivity / 60) }} hours and {{ lastActivity % 60 }} minutes ago</span>
      </p>
    </section>
    <!--Activity-->
    <section>
      <h3>[ activity ]</h3>
      <div v-for="(event, index) in dataArray[1].slice(0, 4)" :key="index">
        <p>{{ event.type.slice(0, event.type.length - 5) }} {{ event.repo.name }}</p>
        <div v-if="event.payload.commits">
          <p v-for="(commit, index) in event.payload.commits.slice(0, 2)" :key="commit.sha">
            <a :href="commit.url" >{{ commit.sha.slice(0, 6) }}: "{{ commit.message }}"</a>
            <span v-if="index === 1 && event.payload.commits.length !== 2"> and {{event.payload.commits.length-2}} more</span>
          </p>
        </div>
      </div>
    </section>
    <!--Site-->
    <footer>
      <p>
        site:
        <a class="accent" :href="dataArray[0].html_url">github.com/{{ dataArray[0].login }}</a>
      </p>
    </footer>
  </article>
</template>

<script lang='ts'>
import { defineComponent } from "vue"

import dayjs from "dayjs"

interface Props {
  dataArray: [{
    login: string,
    avatar_url: string,
    html_url: string,
    name: string,
    company: string,
    blog: string,
    location: string,
    email: string | null,
    hireable: boolean,
    bio: string,
    twitter_username: string | null,
    public_repos: number,
    public_gists: number,
    followers: number,
    following: number,
    created_at: string,
    updated_at: string,
  }, {
    type: string,
    repo: {
      name: string,
    },
    payload: {
      commits?: {
        sha: string,
        message: string,
        url: string,
      }[],
    },
  }[]],
  lastActivity: number,
}

export default defineComponent({
  name: "hspWhois",
  data(): Props {
    return {
      dataArray: [{
        login: "mbledkowski",
        avatar_url: "https://avatars.githubusercontent.com/u/23295125",
        html_url: "https://github.com/mbledkowski",
        name: "Maciej Błędkowski",
        company: "N/A",
        blog: "mble.dk",
        location: "Gdańsk, Poland",
        email: null,
        hireable: true,
        bio: "Front-end developer",
        twitter_username: null,
        public_repos: 46,
        public_gists: 6,
        followers: 11,
        following: 120,
        created_at: "2016-11-06T15:05:52Z",
        updated_at: "2021-12-23T22:25:55Z",
      }, [{
        type: "",
        repo: {
          name: "",
        },
        payload: {
        },
      }]],
      lastActivity: -1,
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      const profile = async () => {
        await fetch("https://api.github.com/user/23295125").then(res => res.json()).then(res => this.dataArray[0] = res)
        this.lastActivity = dayjs().diff(dayjs(this.dataArray[0].updated_at), 'minutes')
      }
      fetch("https://api.github.com/user/23295125/events").then(res => res.json()).then(res => this.dataArray[1] = res)
      profile()
    },
  },
})
</script>

<style lang="scss">
</style>