<template>
    <div class="notes__item">
        <div class="notes__item_top" :class="{ between: !view }">
            <h3 class="notes__item_top-title">{{ note.title }}</h3>
            <p class="notes__item_top-date">{{ note.date }}</p>
        </div>
        <p class="notes__item_text">{{ note.text }}</p>
        <div class="notes__item_btns">
            
            <button class="notes__item_btns-btn edit" @click="$emit('change', note.id)">
                <img src="@/assets/img/pens.svg" alt="">
                <span>{{$t('Edit')}}</span>
            </button>

            <button class="notes__item_btns-btn del" @click="$emit('delNote', note.id)">
                <img src="@/assets/img/basket.svg" alt="">
                <span>{{$t('Delete')}}</span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            typeof: Object
        },
        view: {
            typeof: Boolean
        }
    }
}
</script>
