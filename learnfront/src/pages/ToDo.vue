<script setup>
import { computed, ref } from 'vue';
import ItemList from '../components/ItemList.vue';

let message = ref('');
let newImportance = ref('');
let i = 1;

let items = ref([
    { id: i++, text: 'Piim', isDone: false, importance: 'low' },
    { id: i++, text: 'Viin', isDone: true, importance: 'high' },
    { id: i++, text: 'Õlu', isDone: false, importance: 'medium' },
    { id: i++, text: 'Sai', isDone: true, importance: 'low' },
]);

function add() {
    if (message.value.trim() !== '' && newImportance.value !== '') {
        items.value.push({ id: i++, text: message.value.trim(), isDone: false, importance: newImportance.value });
        message.value = '';
        newImportance.value = '';
    }
}

const importanceOrder = { high: 3, medium: 2, low: 1 };

let sortedItems = computed(() =>
    [...items.value].sort(
        (itemA, itemB) =>
            importanceOrder[itemB.importance] -
            importanceOrder[itemA.importance]
    )
);

let doneItems = computed(() =>
    sortedItems.value.filter(item => item.isDone)
);

let toDoItems = computed(() =>
    sortedItems.value.filter(item => !item.isDone)
);
</script>

<template>
    <div class="container content mt-2">
        <div class="field">
            <div class="control">
                <input v-model="message" @keydown.enter="add" class="input" type="text" placeholder="Add item">
            </div>
        </div>

        <div class="field has-addons">
            <div class="control is-expanded">
                <div class="select is-fullwidth">
                    <select v-model="newImportance">
                        <option value="" disabled>Select importance</option>
                        <option value="low">Low</option>
                        <option value="medium">Medium</option>
                        <option value="high">High</option>
                    </select>
                </div>
            </div>

            <div class="control">
                <button @click="add" class="button is-info">Add</button>
            </div>
        </div>

        <ItemList :items="sortedItems" title="All items" />
        <ItemList :items="doneItems" title="Done items" />
        <ItemList :items="toDoItems" title="ToDo items" />
    </div>
</template>