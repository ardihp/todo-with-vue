<template>
  <ButtonSidebar @click="handleTab('Today')">
    <ViewfinderIcon />
    <p class="mt-1">Today</p>
  </ButtonSidebar>
  <ButtonSidebar @click="handleTab('Upcoming')">
    <InboxIcon />
    <p class="mt-1">Upcoming</p>
  </ButtonSidebar>
  <ButtonSidebar @click="handleTab('Completed')">
    <CheckboxIcon />
    <p class="mt-1">Completed</p>
  </ButtonSidebar>
</template>

<script>
import ButtonSidebar from "./ButtonSidebar.vue";
import { InboxIcon, ViewfinderIcon, CheckboxIcon } from "vue-tabler-icons";

export default {
  name: "Sidebar",
  props: {
    handleTab: { type: Function },
  },
  components: {
    ButtonSidebar,
    InboxIcon,
    ViewfinderIcon,
    CheckboxIcon,
  },
};
</script>
