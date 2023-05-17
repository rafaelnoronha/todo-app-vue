<script setup>
    import { onMounted, ref } from 'vue'

    import ContentCenter from '@/components/ContentCenter.vue'
    import Task from '@/components/Task.vue'

    const task = ref( '' )
    const taskList = ref( [] )

    const includeTask = () => {
        const newTaskList = taskList.value

        newTaskList.push( {
            description: task,
            status: 0
        } )

        taskList.value = newTaskList
        task.value = ''
    }

    onMounted( () => {
        console.log( taskList.value )
    } )

</script>

<template>
    <div class="container">
        <ContentCenter>
            <h1 class="mt-5 fs-5rem text-center"> Task To Do</h1>

            <div class="row justify-content-center mt-5">
                <div class="col-md-6 d-flex justify-content-center">
                    <div class="col-md-8">
                        <input class="w-100 ff-shadows border border-black px-3 py-2" type="text" placeholder="Things" v-model="task" />
                    </div>

                    <div class="col-md-4">
                        <button class="btn btn-dark ff-shadows rounded-0 px-5 h-100" type="button" @click="includeTask"><i class="bi bi-plus ff-shadows" /> Include</button>
                    </div>
                </div>
            </div>

            <div class="row mt-5">
                <Task v-for="(task, index) in taskList" :key="index">{{ task.description }}</Task>
            </div>

        </ContentCenter>
    </div>
</template>