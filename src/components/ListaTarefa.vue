<script setup>
    const props = defineProps(['tasks'])
</script>

<template>
    <ul class="list-group mt-4"> <!-- create a 'v-if' for message if there are pending tasks -->
        <li class="list-group-item" v-for="task in props.tasks">
            <input @change="event => task.completed = event.target.checked" :checked="task.completed"
                :id="task.title" type="checkbox">
            <label :class="{ done: task.completed }" class="ms-3" :for="task.title">
                {{ task.title }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through; /* strike-through */
    }
</style>