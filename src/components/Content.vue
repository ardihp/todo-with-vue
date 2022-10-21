<template>
  <div
    class="grid grid-cols-1 md:grid-cols-8 xl:grid-cols-10 max-w-screen-xl w-full mx-auto p-6 md:p-10"
  >
    <div class="flex flex-wrap md:flex-col md:col-span-2 gap-4 md:gap-6">
      <Sidebar :handleTab="handleTab" :tab="tab" />
    </div>
    <div
      class="flex flex-col md:col-span-6 xl:col-span-8 gap-8 pt-6 md:pt-0 md:pl-10 pr-0"
    >
      <div class="flex justify-between">
        <div class="flex flex-col gap-2">
          <p class="text-2xl font-bold">{{ tab }}</p>
          <p>
            total data:
            {{ lists?.length || 0 }}
          </p>
        </div>
        <div class="flex gap-5 items-center">
          <div
            class="flex items-center w-48 gap-4 py-3 px-4 border-2 h-12 rounded-xl focus-within:border-gray-500 duration-300"
          >
            <SearchIcon class="text-gray-500" />
            <input
              class="mt-1 w-full focus:outline-none"
              placeholder="Search"
              @change="handleSearch"
              v-model="query"
            />
          </div>
          <div
            class="border-2 border-gray-300 hover:border-gray-500 p-2 rounded-xl cursor-pointer duration-300"
            @click="handleModal"
          >
            <PencilPlusIcon class="text-gray-500" />
          </div>
        </div>
      </div>
      <div v-if="lists.length" class="flex flex-col gap-5">
        <div v-for="item in lists" :key="item.id">
          <TodoItem :tab="tab" :data="item" @onDelete="handleAfterDelete" />
        </div>
      </div>
      <div v-else>
        <p>Tidak ada data.</p>
      </div>
    </div>
    <ModalCreate :visible="showModal" :tab="tab" @close="handleModal" />
  </div>
</template>

<script>
import Sidebar from "./Sidebar.vue";
import { SearchIcon, PencilPlusIcon } from "vue-tabler-icons";
import TodoItem from "./TodoItem.vue";
import ModalCreate from "./ModalCreate.vue";

export default {
  name: "Content",
  components: {
    Sidebar,
    SearchIcon,
    TodoItem,
    PencilPlusIcon,
    ModalCreate,
  },
  methods: {
    handleTab(data) {
      this.tab = data;
    },
    handleModal() {
      this.showModal = !this.showModal;
    },
    handleAfterDelete() {
      this.lists = JSON.parse(localStorage.getItem("lists")).filter(
        (item) => item.type === this.tab
      );
    },
    handleSearch(e) {
      this.query = e.target.value;
    },
  },
  data() {
    return {
      tab: "Today",
      showModal: false,
      lists: [],
      query: "",
    };
  },
  watch: {
    showModal: {
      handler() {
        this.lists = JSON.parse(localStorage.getItem("lists")).filter(
          (item) => item.type === this.tab
        );
      },
      immediate: true,
    },
    tab: {
      handler() {
        this.lists = JSON.parse(localStorage.getItem("lists")).filter(
          (item) => item.type === this.tab
        );
      },
      immediate: true,
    },
    query: {
      handler() {
        this.lists = JSON.parse(localStorage.getItem("lists")).filter(
          (item) =>
            item.type === this.tab &&
            item.todo.toLowerCase().includes(this.query.toLowerCase())
        );
      },
      immediate: true,
    },
  },
};
</script>
