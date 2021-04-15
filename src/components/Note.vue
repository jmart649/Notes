<template>
    <div class="bg-blue-300 rounded text-center p-2 space-y-2">
        <h3 class="text-2xl font-bold tracking-wide" >{{ $props.note.title }}</h3>
        <p class="text-sm font-medium" >
            {{ $props.note.content }}
        </p>
        <div class="flex justify-end space-x-2" >
            <button @click="editNote(note)" class="hover:text-green-800" ><mdi-file-document-edit-outline /></button>
            <button @click="removeNote($props.note.id)" class="hover:text-red-800" ><mdi-delete /></button>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmit } from 'vue'
import { remove, showToggle, noteToEdit } from '~/helpers/useNotes'
defineProps({
  note: Object,
  default: {
    id: 0,
    title: '',
    content: '',
  },
})
const emit = defineEmit(['deleted'])
const removeNote = async id => {
  await remove(id)
  emit('deleted')
}
const editNote = note => {
  noteToEdit.value = note
  showToggle()
}
</script>