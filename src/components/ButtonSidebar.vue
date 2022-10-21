<template>
  <button
    class="relative flex items-center gap-3 px-5 py-3 rounded-2xl bg-slate-100 shadow-lg border-gray-500 border-2 active:shadow-none active:top-1 duration-300 opacity-30"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "ButtonSidebar",
};
</script>
