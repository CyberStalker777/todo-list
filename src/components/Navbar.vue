<template>
    <header class="header">
        <nav v-if="nav" class="nav">
            <button class="nav__lang" @click="switchLang">{{ $i18n.locale }}</button>
            <h1 class="nav__title">{{ $t('Notes') }}</h1>
            <button class="nav__search_icon" @click="nav = false">
                <img src="@/assets/img/search.svg" alt="Search">
            </button>
        </nav>

        <nav v-else class="nav__search">
            <button @click="nav = true">
                <img src="@/assets/img/back.svg" alt="back">
            </button>
            <input v-model="search" type="text" :placeholder="$t('Search')" autofocus>
            <button class="nav__search_close" @click="search = ''">
                <img src="@/assets/img/close.svg" alt="close">
            </button>
        </nav>

    </header>
</template>

<script>

export default {
    data() {
        return {
            nav: true,
            search: ''
        }
    },

    methods: {
        switchLang() {
            this.$i18n.locale === 'ru' ? this.$i18n.locale = 'eng' : this.$i18n.locale = 'ru'
            localStorage.lang = this.$i18n.locale
        }
    },

    watch: {
        search(newVal) {
            this.$emit('setSearch', newVal)
        }
    }
}
</script>
