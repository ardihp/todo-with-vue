<template>
  <div class="flex justify-center py-8 px-10 shadow-md shadow-slate-300 border-b-2 border-gray-400">
    <div class="max-w-screen-xl mx-auto w-full flex justify-center">
      <div class="text-xl font-bold flex gap-1 items-end text-gray-500">
        Todo <ChecklistIcon size="36" /> Check
      </div>
    </div>
  </div>
</template>

<script>
import { ChecklistIcon } from "vue-tabler-icons";

export default {
  components: {
    ChecklistIcon,
  },
};
</script>
