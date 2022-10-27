<script>
import {XMarkIcon} from "@heroicons/vue/24/solid"
import { api } from "../../assets/api"

const props = defineProps({item: Object})

function remove()
{
  remove (index) {
              item.$delete(item.finds, index)
  };
  api().post('/delete_card', {
    card_id: item.id
  }).then(res => alert("deleted"))
}

</script>

<template>
  <li class="w-full bg-white rounded py-2 px-1 my-3" v-bind="$attrs">
    <p class="text-gray-800">{{ props.item.text }}</p>
    <XMarkIcon
    class="w-8 h-8 fill-gray-400 hover:fill-gray-800"
        @click="remove"
       /> 
  </li>
</template>

<style lang="scss" scoped>

</style>


