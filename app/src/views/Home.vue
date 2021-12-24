<template>
  <div class="home">
    <hspWhois />
    <github />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import hspWhois from "@/components/hspWhois.vue" // @ is an alias to /src
import github from "@/components/github.vue"

export default defineComponent({
  name: "Home",
  components: {
    hspWhois,
    github,
  },
})
</script>
