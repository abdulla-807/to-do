<template>
    <div class="card">
        <div :class="{card__content: !grid}">
            <h3 class="card__title">{{ note.title }}</h3>
            <p class="card__date">{{ note.date }}</p>
        </div>
        <p class="card__desc">{{ note.desc }}</p>
        <div class="card__controls">
            <button class="card__btn" @click="$emit('changeNote')">
                <img src="../assets/img/edit.svg" alt="">
                <span>{{ words.editbtn[lang] }}</span>
            </button>
            <button @click="$emit('delNote')" class="card__btn card__btn_red">
                <img src="../assets/img/delete.svg" alt="">
                <span>{{ words.deledit[lang] }}</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        props:{
            grid: Boolean,
            note: Object,
            lang: String
        }, 
        inject: ['words']
    }
</script>

<style lang="scss">
.card {
    border-radius: 16px;
    background: linear-gradient(0deg, rgba(103, 80, 164, 0.05) 0%, rgba(103, 80, 164, 0.05) 100%), #FFFBFE;
    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15), 0px 1px 2px 0px rgba(0, 0, 0, 0.30);
    padding: 16px;
    font-size: 14px;
    
    &__content {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    
    &__title {
        color: #1C1B1F;
        font-size: 16px;
        font-weight: 500;
        line-height: 24px; 
        letter-spacing: 0.1px;
    }
    
    &__date {
        color: #CAC4D0;
        line-height: 20px; 
        letter-spacing: 0.25px;
    }
    
    &__desc {
        line-height: 20px; 
        letter-spacing: 0.25px;
        margin-top: 16px;
        margin-bottom: 17px;
    }
    
    &__controls {
        display: flex;
        align-items: center;
        justify-content: end;
    }
    
    &__btn {
        display: flex;
        align-items: center;
        gap: 8px;
        padding: 12px 12px 12px 15px;
        color: #6750A4;
        font-weight: 500;
        line-height: 20px; 
        letter-spacing: 0.1px;
        text-transform: uppercase;
        border-radius: 5px;
        
        &:hover {
            background: #E6DDFF;
        }
        
        &_red {
            color: #CF1B1B;
            
            &:hover {
                background: #FFE1E1;
            }
        }
    }
}
</style>