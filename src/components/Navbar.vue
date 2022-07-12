<template>
   <header class="header">
       <transition name="header__notes">
           <div class="header__notes" v-show="header === true">
                <button @click="changeLang"  class="header__lang" v-if="lang == 'ru'">UZ</button>
                <button @click="changeLang" class="header__lang" v-else>RU</button>
                <h1 class="header__title">{{ words.appbartitle[lang]    }}</h1>
                <button class="header__search" @click="header = false">
                    <img src="@/assets/img/search.png" alt="">
                </button>
            </div>
       </transition>
       <transition name="header__form">
           <form class="header__form" v-show="header === false" >
                <a href="#!" class="back" @click.prevent="header = true, search = ''">
                    <img src="@/assets/img/back.svg" alt="">
                </a>
                <input  
                    type="text" 
                    :placeholder="words.appbarseacrch[lang]" 
                    class="header__input" 
                    v-model="search"
                >
                <a href="#!" class="header__close" @click.prevent="search = ''">
                    <img src="@/assets/img/cancel.png" alt="">
                </a>
            </form>
       </transition>
   </header>
</template>
<script>
export default {
    name: 'Navbar',
    data() {
        return {
            header: true,
            search: '',
         
        }
    },
    inject: ['words'],
    props: {
        lang: String,
    },
    watch: {
        search(val){
            this.$emit('getSearch', val);
        },
    },
    methods: {
        changeLang() {
            this.$emit('changeLang', this.lang == 'ru' ? 'uz' : 'ru')
        }
    }
}
</script>

<style>

.header {
    padding: 17px 20px;
    background: #f3edf7;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, .25), 0px 1px 3px rgba(0, 0, 0, .3);
    position: relative;
    overflow: hidden;
    height: 74px
}



.header__notes-enter-active,
.header__notes-leave-active {
    transition: .5s linear
}

.header__notes-enter-from,
.header__notes-leave-to {
    opacity: 0;
    transform: translateY(-200px)
}

.header__notes-enter-to,
.header__notes-leave-from {
    opacity: 1;
    transform: translateY(0px)
}
.header__lang {
    font-size: 22px;
    font-weight: bold;
}
.header__title {
    font-size: 22px;
    line-height: 28px;
    text-align: center;
    color: #1c1b1f
}

.header__search {
    cursor: pointer;
    background: transparent
}

.header__notes,
.header__form {
    display: flex;
    justify-content: space-between;
    align-items: center
}

.header__form-enter-active,
.header__form-leave-active {
    transition: .5s linear
}

.header__form-enter-from,
.header__form-leave-to {
    opacity: 0;
    transform: translateY(200px)
}

.header__form-enter-to,
.header__form-leave-from {
    opacity: 1;
    transform: translateY(0px)
}

.header__input {
    display: block;
    width: 90%;
    font-size: 16px;
    line-height: 20px;
    color: #000;
    background: transparent
}

.header__input::-moz-placeholder {
    color: #9d9d9d
}

.header__input:-ms-input-placeholder {
    color: #9d9d9d
}

.header__input::placeholder {
    color: #9d9d9d
}

button,
input{
    outline: none;
    border: none;
}

</style>