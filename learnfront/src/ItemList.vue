
<script setup>
defineProps(['items', 'title']);
</script>

<template>
    <h1>{{ title }}</h1>
    <ul>
        <li v-for="item in items" :key="item.id" :class="item.importance">
            {{ item.text }} - {{ item.importance }}
            <input type="checkbox" v-model="item.isDone">
        </li>
    </ul>
</template>

<style scoped>
.high {
    color: red;
}

.medium {
    color: orange;
}

.low {
    color: green;
}
</style>
