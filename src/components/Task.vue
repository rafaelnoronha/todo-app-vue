<script setup>

</script>

<template>
    <div class="col-md-3">
        <div class="card text-bg-light mb-3 ff-shadows rounded-0">
            <div class="card-header d-flex justify-content-between p-0">
                <div class="header-button position-relative ms-1">
                    <i class="bi bi-pin-angle-fill position-absolute top-50 start-50 translate-middle" />
                </div>
                <div class="header-button position-relative">
                    <button class="btn btn-light w-100 h-100 rounded-0">
                        <i class="bi bi-hand-thumbs-down-fill position-absolute top-50 start-50 translate-middle" />
                    </button>
                </div>
            </div>
            <div class="card-body">
                <p class="card-text">
                    <slot />
                </p>
            </div>
            <div class="card-footer p-0">
                <button class="btn btn-dark w-100 rounded-0" type="button"><i class="bi bi-trash-fill" /> Exclude</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    ::selection {
        background: #ffffff;
        color: #212529;
    }

    .header-button {
        height: 30px!important;
        width: 30px!important;
    }
</style>