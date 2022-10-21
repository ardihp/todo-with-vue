<template>
  <n-modal :show="visible" :on-mask-click="closeModal">
    <n-card
      style="width: 600px"
      title="What kind of thing would you like to do ?"
      :bordered="false"
      size="huge"
      role="dialog"
      aria-modal="true"
    >
      <template #header-extra>
        <p>
          Category : <span class="font-bold">{{ tab }}</span>
        </p>
      </template>
      <div class="flex flex-col gap-5">
        <input
          placeholder="write it here"
          class="py-2 w-full border-b-2 focus:outline-none"
          @change="setTodo"
          v-model="todo"
          v-on:keyup.enter="submitTodo"
        />
        <button
          class="py-2 bg-slate-400 text-white font-bold rounded-md disabled:bg-slate-200 disabled:cursor-not-allowed"
          @click="submitTodo"
          :disabled="todo === ''"
        >
          note now
        </button>
      </div>
      <template #footer>
        Remember to complete the to do you make here! 😎👌
      </template>
    </n-card>
  </n-modal>
</template>

<script>
import { defineComponent } from "vue";
import { NModal, NCard } from "naive-ui";

export default defineComponent({
  props: {
    visible: { type: Boolean },
    tab: { type: String },
  },
  data() {
    return { todo: "" };
  },
  components: {
    NModal,
    NCard,
  },
  methods: {
    setTodo(e) {
      this.todo = e.target.value;
    },
    submitTodo() {
      const lists = localStorage.getItem("lists");
      const data = {
        id: new Date(),
        todo: this.todo,
        type: this.tab,
        is_done: false,
      };

      if (this.todo) {
        localStorage.setItem(
          "lists",
          JSON.stringify([data, ...JSON.parse(lists)])
        );

        this.todo = "";
        this.closeModal();
      }
    },
    closeModal() {
      this.$emit("close");
    },
  },
});
</script>
