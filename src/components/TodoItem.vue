<script setup>
const props = defineProps({
  todo: {
    type: String,
    required: true,
  },
})

const emit = defineEmits(['toggle-checkbox'])
const toggleCheckbox = (e)=>{

  emit('toggle-checkbox', {
    id: props.todo.id,
    checked:e.target.checked
  }) //함수 실행 | true false 여부가 넘어가야함 인풋에 변동사항 생기면 @change="toggleCheckbox"
}
</script>

<template>
  <div >
    <BFormCheckbox
      id="checkbox-1"
      v-model="status"
      name="checkbox-1"
      value="accepted"
      unchecked-value="not_accepted"
      @change="toggleCheckbox"
    >
     <span :class="todo.checked && 'muted'"> {{todo.title}}</span>
    </BFormCheckbox>
  </div>
</template>
<!-- //todo check의 값이true면 muted 클래스명을 추가 (밑줄) -->
<style scoped>
.muted{
  text-decoration: line-through;
}
</style>
