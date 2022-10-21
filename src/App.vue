<template>
  <Content />
</template>

<script>
import Content from "@/components/Content.vue";

export default {
  name: "App",
  components: {
    Content,
  },
  beforeMount() {
    const lists = localStorage.getItem("lists");
    lists === null ? localStorage.setItem("lists", JSON.stringify([])) : lists;
  },
};
</script>
