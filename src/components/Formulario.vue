<script setup>
    const props = defineProps(['addTask', 'taskTemp', 'changeFilter', 'editTaskTemp'])
</script>

<template>
    <form @submit.prevent="props.addTask"> <!-- updates the page with the change -->
        <div class="row">
            <div class="col">
                <input :value="props.taskTemp" @change="props.editTaskTemp" required
                    type="text" placeholder="Enter task description" class="form-control">
            </div>

            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Add</button>
            </div>

            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-control">
                    <option value="all">All tasks</option>
                    <option value="pending">Pending</option>
                    <option value="completed">Completed</option>
                </select>
            </div>
        </div>
    </form>
</template>

<style>
    @media (max-width: 768px) {
        button {
            margin-bottom: 20px;
        }
    }

    @media (max-width: 1023px) {
        form > .row{
            display: block;
        }

        .col input {
            width: 70%;
            margin-bottom: 15px;
        }

        div > button {
            margin-bottom: 30px;
        }

        div.col-md-2 {
            width: 40%;
        }
    }
</style>