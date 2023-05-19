<script setup>
    import { computed, defineEmits } from 'vue'

    const props = defineProps( {
        task: {
            type: Object,
            required: true
        }
    } )

    const iconTaskState = computed( () => props.task.status ? 'bi-hand-thumbs-up-fill' : 'bi-hand-thumbs-down-fill' )
    const taskText = computed( () => props.task.status ? 'text-decoration-line-through' : '' )
    
    const emit = defineEmits( [
        'delete',
        'changeStatus'
    ] )
</script>

<template>
    <div class="col-md-6 col-lg-4 col-xl-3">
        <div class="card text-bg-dark mb-3 ff-shadows rounded-0">
            <div class="card-header d-flex justify-content-between p-0">
                <div class="header-button position-relative ms-1">
                    <i class="bi bi-pin-angle-fill position-absolute top-50 start-50 translate-middle" />
                </div>
                <div class="header-button position-relative">
                    <button class="btn btn-dark w-100 h-100 rounded-0" @click="emit( 'changeStatus', { ...props.task, status: !props.task.status } )">
                        <i class="bi position-absolute top-50 start-50 translate-middle" :class="iconTaskState" />
                    </button>
                </div>
            </div>
            <div class="card-body">
                <p class="card-text" :class="taskText">
                    {{ props.task.description }}
                </p>
            </div>
            <div class="card-footer p-0">
                <button class="btn btn-dark w-100 rounded-0" type="button" @click="emit( 'delete', props.task )"><i class="bi bi-trash-fill" /> Delete</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    ::selection {
        background: #ffffff;
        color: var(--black);
    }

    .header-button {
        height: 30px!important;
        width: 30px!important;
    }
</style>