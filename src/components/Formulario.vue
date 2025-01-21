<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa" class="mx-auto mb-4">
        <div class="flex justify-between">
        <div class="w-[60%]">
            <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required class="w-full p-2  rounded border-2 border-blue-500" type="text" placeholder="Digite aqui a descrição">

        </div>
        <div class=" flex gap-5">
            <button class="btn bg-blue-500 hover:bg-blue-600 text-white" type="submit">Cadastrar tarefa</button>
            <select @change="props.trocarFiltro" class="btn bg-gray-100 shadow hover:bg-gray-200 text-center" >
                <option value="todas">Todas tarefas</option>
                <option value="pendentes">Pendentes</option>
                <option value="finalizadas">Finalizadas</option>
            </select>
        </div>
        </div>
    </form>
</template>