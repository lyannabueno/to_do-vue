<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa"> <!--atualiza a página com a mudança-->
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    type="text" placeholder="Digite a descrição da tarefa" class="form-control">
            </div>

            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>

            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style>
    @media (max-width: 1023px) {
        form > .row{
            display: block;
        }

        .col input {
            width: 70%;
            margin-bottom: 15px;
        }

        button {
            margin-bottom: 30px;
        }

        div.col-md-2 {
            width: 35%;
        }
    }
</style>