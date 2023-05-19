<script setup>
    import { computed, ref } from 'vue'
    import Task from '@/components/Task.vue'

    const sequence = ref( 1 )
    const task = ref( '' )
    const taskList = ref( [] )
    const percentTaskCompleted = computed( () => ( ( ( taskList.value.filter( ts => ts.status ).length / taskList.value.length ) * 100 ) || 0 ).toFixed( 2 ) )

    const includeTask = () => {
        if ( !task.value.trim() ) return

        const newTaskList = [ ...taskList.value ]

        newTaskList.push( {
            id: sequence.value++,
            description: task.value,
            status: false
        } )

        taskList.value = [ ...newTaskList ]
        task.value = ''
    }
</script>

<template>
    <div class="container">
        <h1 class="mt-5 fs-5rem text-center"> Task To Do</h1>

        <div class="row justify-content-center mt-5">
            <div class="col-md-6 justify-content-center">
                <div class="row g-0">
                    <div class="col-lg-7 col-xl-9">
                        <input class="w-100 ff-shadows border border-black px-3 py-2" type="text" placeholder="Things" 
                            v-model.trim="task"
                            @keydown="$event.key === 'Enter' && includeTask()"
                        />
                    </div>
    
                    <div class="col-lg-5 col-xl-3">
                        <button class="btn btn-dark ff-shadows rounded-0 px-5 h-100 w-100" type="button" @click="includeTask"><i class="bi bi-plus ff-shadows" /> Include</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="row justify-content-center mt-2">
            <h4 class="text-center">{{ percentTaskCompleted }}% completed tasks</h4>
        </div>

        <div class="row mt-5">
            <Task
                v-for="( taskItem, index ) in [ ...taskList ].sort( ( a, b ) => b.id - a.id )"
                :key="index"
                :task="taskItem"
                @changeStatus="changedTask => taskList = [ ...taskList ].map( ts => ts.id === changedTask.id ? changedTask : ts )"
                @delete="deletedTask => taskList = [ ...taskList ].filter( ts => ts.id !== deletedTask.id )"
            />
        </div>
    </div>
</template>