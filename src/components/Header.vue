<template>
  <div class="flex justify-center pb-8">
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
