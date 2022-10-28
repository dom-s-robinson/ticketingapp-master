<script setup>
import { PencilIcon, XMarkIcon } from "@heroicons/vue/24/solid"
import { api } from "../../assets/api"
import { ref } from "vue"

const props = defineProps({ item: Object })
const emit = defineEmits(["removed"])
const cardText = ref(props.item.text)
const show = ref(false)

function remove() {
  api()
    .post("/delete_card", { card_id: props.item.id })
    .then((res) => {
      emit("removed", props.item.id)
      // listItems.value = listItems.value.filter((item) => item.id != id)
    })
}

function edit() {
  // alert("please work!")
  api()
    .post("/update_card_text", {
      card_id: props.item.id,
      text: cardText.value,
    })
    .then((res) => alert("edited"))
}
</script>

<template>
  <li class="w-full bg-white rounded py-2 px-1 my-3" v-bind="$attrs">
    <form @submit.prevent="edit" v-if="show">
      <input
        type="text"
        v-model="cardText"
        class="border border-gray-600 rounded p-2 outline-none focus:ring focus:ring-indigo-400"
      />
    </form>
    <p v-else class="text-gray-800">{{ props.item.text }}</p>
    <div class="flex items-center space-x-3">
      <XMarkIcon
        @click="remove"
        class="w-4 h-4 fill-gray-400 hover:fill-gray-800"
      />
      <PencilIcon
        @click="show = !show"
        class="w-4 h-4 fill-gray-400 hover:fill-gray-800"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped></style>
