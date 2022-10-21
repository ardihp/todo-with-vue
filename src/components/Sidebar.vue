<template>
  <ButtonSidebar
    :class="{ ['opacity-100 bg-slate-600 text-white']: tab === 'Today' }"
    @click="handleTab('Today')"
  >
    <ViewfinderIcon />
    <p class="mt-1">Today</p>
  </ButtonSidebar>
  <ButtonSidebar
    :class="{ ['opacity-100 bg-slate-600 text-white']: tab === 'Upcoming' }"
    @click="handleTab('Upcoming')"
  >
    <InboxIcon />
    <p class="mt-1">Upcoming</p>
  </ButtonSidebar>
  <ButtonSidebar
    :class="{ ['opacity-100 bg-slate-600 text-white']: tab === 'Completed' }"
    @click="handleTab('Completed')"
  >
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
    tab: { type: String },
  },
  components: {
    ButtonSidebar,
    InboxIcon,
    ViewfinderIcon,
    CheckboxIcon,
  },
};
</script>
