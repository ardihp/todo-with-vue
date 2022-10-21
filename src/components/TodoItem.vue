<template>
  <div class="relative flex items-center">
    <div
      :class="{
        ['item-today']: tab === 'Today',
        ['item-upcoming']: tab === 'Upcoming',
        ['item-completed']: tab === 'Completed',
      }"
      class="flex items-center justify-between p-4 rounded-xl font-bold cursor-pointer w-full"
      @click="handleCheck(data)"
    >
      <div class="flex items-center gap-4">
        <input
          ref="checkbox"
          type="checkbox"
          :class="{
            ['check-today']: tab === 'Today',
            ['check-upcoming']: tab === 'Upcoming',
            ['check-completed']: tab === 'Completed',
          }"
          :checked="data.is_done"
          class="appearance-none bg-white border-2 rounded-lg w-6 h-6 cursor-pointer"
          @click="handleCheck"
        />
        <p :class="{ ['line-through']: data.is_done === true }" class="mt-1">
          {{ data.todo }}
        </p>
      </div>
    </div>
    <div
      :class="{
        ['text-rose-600']: tab === 'Today',
        ['text-amber-600']: tab === 'Upcoming',
        ['text-emerald-600']: tab === 'Completed',
      }"
      class="z-10 absolute right-4 cursor-pointer"
      @click="handleDelete(data)"
    >
      <TrashIcon />
    </div>
  </div>
</template>

<script>
import { TrashIcon } from "vue-tabler-icons";

export default {
  name: "TodoItem",
  props: {
    tab: { type: String },
    data: { type: Object },
  },
  components: {
    TrashIcon,
  },
  methods: {
    handleCheck(data) {
      const lists = JSON.parse(localStorage.getItem("lists"));
      const filteredList = lists.find((item) => item.id === data.id);
      const dataReplace = [{ ...filteredList, is_done: !filteredList.is_done }];
      localStorage.setItem(
        "lists",
        JSON.stringify(
          lists.map(
            (item) => dataReplace.find((obj) => obj.id === item.id) || item
          )
        )
      );

      this.$emit("onDelete");
    },
    handleDelete(data) {
      const lists = JSON.parse(localStorage.getItem("lists"));
      const filteredList = lists.filter((item) => item.id !== data.id);
      localStorage.setItem("lists", JSON.stringify(filteredList));

      this.$emit("onDelete");
    },
  },
};
</script>

<style>
.item-today {
  @apply bg-rose-100 border-2 border-rose-300 text-rose-600 shadow-lg shadow-rose-100;
}
.item-upcoming {
  @apply bg-amber-100 border-2 border-amber-300 text-amber-600 shadow-lg shadow-amber-100;
}
.item-completed {
  @apply bg-emerald-100 border-2 border-emerald-300 text-emerald-600 shadow-lg shadow-emerald-100;
}
.check-today {
  @apply border-rose-300 checked:bg-rose-200;
}
.check-upcoming {
  @apply border-amber-300 checked:bg-amber-200;
}
.check-completed {
  @apply border-emerald-300 checked:bg-emerald-200;
}
</style>
