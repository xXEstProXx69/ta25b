
<script setup>
import { computed, ref } from 'vue';
import ItemList from './ItemList.vue';

let message = ref('');
let importance = ref('medium');
let i = 1;
let items = ref([
    {id: i++, text: 'Kohukesed', isDone: false, importance: 'high'},
    {id: i++, text: 'coca cola', isDone: true, importance: 'low'},
    {id: i++, text: 'suhkur', isDone: false, importance: 'medium'},
    {id: i++, text: 'Või', isDone: true, importance: 'high'},
]);

function add(){
  if(message.value.trim() !== '') {
    items.value.push({
        id: i++,
        text: message.value.trim(),
        isDone: false,
        importance: importance.value
    });
  }
  message.value = '';
}

function getImportance(value) {
    if(value === 'high') return 1;
    if(value === 'medium') return 2;
    return 3;
}

let allItems = computed(() => [...items.value].sort((a, b) =>
    getImportance(a.importance) - getImportance(b.importance)
));

let doneItems = computed(() => allItems.value.filter(item => item.isDone));
let toDoItems = computed(() => allItems.value.filter(item => !item.isDone));

let highItems = computed(() =>
    allItems.value.filter(item => item.importance === 'high')
);

let mediumItems = computed(() =>
    allItems.value.filter(item => item.importance === 'medium')
);

let lowItems = computed(() =>
    allItems.value.filter(item => item.importance === 'low')
);
</script>

<template>
    <div class="container content mt-2">
        <div class="field has-addons">
            <div class="control is-expanded">
                <input @keydown.enter="add" v-model="message" class="input" type="text" placeholder="Add item">
            </div>
            <div class="control">
                <div class="select">
                    <select v-model="importance">
                        <option value="high">High</option>
                        <option value="medium">Medium</option>
                        <option value="low">Low</option>
                    </select>
                </div>
            </div>
            <div class="control">
                <button @click="add" class="button is-info">
                    Add
                </button>
            </div>
        </div>
        
        <ItemList :items="allItems" title="All items"></ItemList>
        <ItemList :items="doneItems" title="Done items"></ItemList>
        <ItemList :items="toDoItems" title="ToDo items"></ItemList>
        <ItemList :items="highItems" title="High importance"></ItemList>
        <ItemList :items="mediumItems" title="Medium importance"></ItemList>
        <ItemList :items="lowItems" title="Low importance"></ItemList>
    </div>
</template>

<style></style>
