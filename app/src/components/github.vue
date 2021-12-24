<template>
  <!--Title-->
  <h2>λ github /profile</h2>
  <!--Content-->
  <!--Image-->
  <img :src="data.avatar_url" alt="{{data.name}}'s GitHub profile picture">
  <p>
    {{ data.name }} <span class="accent">[</span> {{data.login}} <span class="accent">]</span>
  </p>
  <p>
    site: <a class="accent" :href="data.html_url">github.com/{{data.login}}</a>
  </p>
</template>

<script lang='ts'>
import { defineComponent } from "vue"

interface Props {
  data: {
    login: string,
    id: number,
    node_id: string,
    avatar_url: string,
    gravatar_id: string,
    url: string,
    html_url: string,
    followers_url: string,
    following_url: string,
    gists_url: string,
    starred_url: string,
    subscriptions_url: string,
    organizations_url: string,
    repos_url: string,
    events_url: string,
    received_events_url: string,
    type: string,
    site_admin: boolean,
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
  }
}

export default defineComponent({
  name: "hspWhois",
  data(): Props {
    return {
      data: {
        login: "mbledkowski",
        id: 23295125,
        node_id: "MDQ6VXNlcjIzMjk1MTI1",
        avatar_url: "https://avatars.githubusercontent.com/u/23295125?v=4",
        gravatar_id: "",
        url: "https://api.github.com/users/mbledkowski",
        html_url: "https://github.com/mbledkowski",
        followers_url: "https://api.github.com/users/mbledkowski/followers",
        following_url: "https://api.github.com/users/mbledkowski/following{/other_user}",
        gists_url: "https://api.github.com/users/mbledkowski/gists{/gist_id}",
        starred_url: "https://api.github.com/users/mbledkowski/starred{/owner}{/repo}",
        subscriptions_url: "https://api.github.com/users/mbledkowski/subscriptions",
        organizations_url: "https://api.github.com/users/mbledkowski/orgs",
        repos_url: "https://api.github.com/users/mbledkowski/repos",
        events_url: "https://api.github.com/users/mbledkowski/events{/privacy}",
        received_events_url: "https://api.github.com/users/mbledkowski/received_events",
        type: "User",
        site_admin: false,
        name: "Maciej Błędkowski",
        company: "Looking for a job (front-end)",
        blog: "linkedin.com/in/mbledkowski",
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
        updated_at: "2021-12-23T22:25:55Z"
      }
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      await fetch("https://api.github.com/user/23295125").then(res => res.json()).then(res => this.data = res)
    }
  }
})
</script>

<style lang="scss">
</style>