<template>
    <div class="notes">
        <div class="container">
            <div class="notes__top">
                <h2 class="notes__title">Все заметки</h2>
                <button class="notes__btn" @click="grid = !grid">
                    <img src="../assets/img/list.svg" alt="" v-if="grid">
                    <img src="../assets/img/grid.svg" alt="" v-else>
                    <span>{{ grid ? 'Список' : 'Сетка'}}</span>
                </button>
            </div>
            <div class="notes__list" :class="{ active: !grid}">
                <NotesCard :grid="grid"
                v-for="item in notes" :key="item.id"
                :note="item"
                />
            </div>
        </div>
    </div>
</template>

<script>
    import NotesCard from '@/components/NotesCard.vue';
    export default {
        props: {
            notes: {
                type: Array,
                default: []
            }
        },
        components: {
            NotesCard
        },
        data(){
            return {
                grid: true
            }
        }
    }
</script>

<style lang="scss">
    .notes {
        margin-top: 30px;
        
        &__top {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        &__title {
            font-weight: 400;
            font-size: 22px;
            line-height: 28px;
            color: #323232;
        }
        
        &__btn {
            display: flex;
            padding: 16px 20px 16px 16px;
            align-items: center;
            gap: 12px;
            border-radius: 16px;
            background: linear-gradient(0deg, rgba(103, 80, 164, 0.11) 0%, rgba(103, 80, 164, 0.11) 100%), #FFFBFE;
            box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.30), 0px 4px 8px 3px rgba(0, 0, 0, 0.15);
            font-size: 14px;
            font-weight: 500;
            line-height: 20px; 
            letter-spacing: 0.1px;
            color: #6750A4;
        }
        
        &__list {
            margin-top: 30px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 24px;
            
            &.active {
                grid-template-columns: repeat(1, 1fr);
            }
        }
    }
</style>