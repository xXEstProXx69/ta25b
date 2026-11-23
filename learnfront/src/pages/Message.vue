<script setup>
import Message from '../components/Message.vue';
</script>

<template>
    <section class="section">
        <div class="container">
            <h1 class="title">Message Demo</h1>
            <p class="subtitle">Reusable Message Component</p>

            <Message type="success" text="Operation completed successfully!"/>

            <Message type="danger" text="Something went wrong!"/>

            <Message type="warning" text="Please check your input!"/>

            <Message type="info" text="Welcome to the application!"/>
        
        </div>
    </section>
</template>