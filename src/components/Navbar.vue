<template>
    <header class="header">
        <Transition name="header">
            <div class="header__content" v-show="header == true">
                <button class="header__lang">ru</button>
                <h1 class="header__title">Заметки</h1>
                <button class="header__search" @click="header = false">
                    <img src="@/assets/img/search.svg" alt="">
                </button>
            </div>
        </Transition>
        <Transition name="header">
        <div class="header__form" v-show="header == false">
            <button class="header__back" @click="header=true">
                <img src="@/assets/img/back.svg" alt="">
            </button>
            <input v-model="search" type="text" class="header__input container" placeholder="Поиск...">
            <button class="header__clear" @click="search=''">
                <img src="../assets/img/close.svg" alt="">
            </button>
        </div>
        </Transition>
    </header>
</template>

<script>
export default {
    data(){
        return {
            header: true,
            search: ''
        }
    }
}
</script>

<style lang="scss">
.header-enter-active,
.header-leave-active {
  transition: 0.5s ease;
}

.header-enter-from,
.header-leave-to {
  transform: translateY(-200px);
}

.header {
    background: #F3EDF7;
    box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.30), 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    padding: 14px 16px;
    height: 70px;
    display: flex;
    flex-direction: column;
    justify-content: center;

    &__content, &__form {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-grow: 1;
    }
    
    &__lang {
        text-transform: uppercase;
        font-weight: 500;
        font-size: 22px;
    }
    
    &__title {
        font-size: 22px;
        line-height: 28px;
        font-weight: 400;
        color: #1C1B1F;
    }
    
    &__input {
        line-height: 20px;
        
        &::placeholder {
            color: #9D9D9D;
        }
    }
}

</style>