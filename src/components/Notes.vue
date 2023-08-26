<template>
    <div class="notes container">
        <div class="notes__top">
            
            <h2 class="notes__top_title">{{ notes.length > 0 ? $t('AllNotes') : $t('NoNotes') }}</h2>
            
            <button @click="view = !view" class="notes__top_btn">
                <img v-show="view" src="@/assets/img/list.svg" alt="list">
                <img v-show="!view" src="@/assets/img/layout.svg" alt="layout">
                <span>{{ view ? $t('List') : $t('Grid') }}</span>
            </button>
        </div>


        <div class="notes__list" :class="{ active: !view }">
            
            <NotesItem 
            v-for="note in notes" 
            :key="note.id" 
            :note="note" 
            :view="view"
            @delNote="$emit('delNote', note.id)"
            @change="$emit('change', note.id)"
            />
        </div>

    </div>
</template>

<script>
import NotesItem from './NotesItem.vue';

export default {
    data() {
        return {
            view: true,
        };
    },
    components:
    {
        NotesItem
    },
    props: {
        notes: {
            typeof: Array
        }
    }
}
</script>
