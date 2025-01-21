<script setup>
import { reactive } from 'vue';
  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Criar portifílio',
        finalizada: true,
      },
      {
        titulo: 'Preparar a janta',
        finalizada: false,
      },
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default: 
        return estado.tarefas;
    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="max-w-screen-lg m-auto">
    <header class="p-5 mb-4 mt-4 bg-gray-100 shadow rounded">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa()" class="mx-auto mb-4">
      <div class="flex justify-between">
        <div class="w-[60%]">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="w-full p-2  rounded border-2 border-blue-500" type="text" placeholder="Digite aqui a descrição">

        </div>
        <div class=" flex gap-5">
            <button class="btn bg-blue-500 hover:bg-blue-600 text-white" type="submit">Cadastrar tarefa</button>
            <select @change="evento => estado.filtro = evento.target.value" class="btn bg-gray-100 shadow hover:bg-gray-200 text-center" >
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Pendentes</option>
              <option value="finalizadas">Finalizadas</option>
            </select>
        </div>
      </div>
    </form>
    <ul class="space-y-2">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked"  :checked="tarefa.finalizada" :id="tarefa.titulo" class="mr-3" type="checkbox">
        <label :class="{ done: tarefa.finalizada }"> 
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>