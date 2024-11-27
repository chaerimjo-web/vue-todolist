<script setup>
import { ref } from 'vue';

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['toggle-checkbox'],['todo-delete'])

const isChecked = ref(props.todo.checked);

const toggleCheckbox = (e)=>{

  emit('toggle-checkbox', {
    id: props.todo.id,
    checked:e.target.checked
  }) //함수 실행 | true false 여부가 넘어가야함 인풋에 변동사항 생기면 @change="toggleCheckbox"
}
const todoDelete = ()=>{

  emit('todo-delete', {
    id: props.todo.id,
  })
}
</script>

<template>
  <div class="d-flex gap-3 align-items-center mt-3">
    <BFormCheckbox
      :id="`{checkbox-${todo.id}}`"
      v-model="isChecked"
      :name="`{checkbox-${todo.id}}`"
      value="accepted"
      @change="toggleCheckbox"
    >
     <span :class="{muted: todo.checked}"> {{todo.title}}</span>
    </BFormCheckbox>
    <BButton variant="danger" size="sm" @click="todoDelete">삭제</BButton>
  </div>
</template>
<!-- //todo check의 값이true면 muted 클래스명을 추가 (밑줄) -->
<style scoped>
.muted{
  text-decoration: line-through;
}
</style>
