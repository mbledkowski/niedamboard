<template>
  <div class="home">
    <hspWhois />
    <github />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import github from "@/components/github.vue"

export default defineComponent({
  name: "Home",
  components: {
    github,
  },
})
</script>
