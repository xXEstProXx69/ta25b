<script setup>
defineProps({
    type: {
        type: String,
        required: true,
        validator(value) {
            return ['success', 'danger', 'warning', 'info'].includes(value);
        }
    },
    text: {
        type: String,
        required: true
    }
});
</script>

<template>
    <div class="notification" :class="`is-${type}`">
        {{ text }}
    </div>
</template>