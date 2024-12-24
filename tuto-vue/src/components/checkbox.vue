<template>
    <label>  
        <input type="checkbox" @change="onChange" >{{label}}
        </input>
    </label>
</template>

<script setup>
const props= defineProps({
    label: String
})

// les evenements
const emits=defineEmits(['checked','unchecked'])
const onChange=(event)=>{
    if (event.currentTarget.checked)
        emits('checked',event.currentTarget)
    else
    emits ('unchecked',event.currentTarget)  
}
</script>