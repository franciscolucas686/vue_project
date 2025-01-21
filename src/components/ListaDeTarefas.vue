<script setup>
const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="space-y-2">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" class="mr-3" type="checkbox">
            <label :class="{ done: tarefa.finalizada }">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>