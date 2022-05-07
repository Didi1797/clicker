<template>
    <span :class="getBoardItemClasses" @click="select(field.id)"></span>
</template>

<script>
import { FIELD, GAME_STATUS } from '@/constants'
import { computed } from 'vue'

export default {
    name: 'BoardItem',
    props: {
        field: {
            type: Object,
            required: true,
        },

        gameStatus: {
            type:Number,
            required: false,
            default: GAME_STATUS.NONE,
        }
    },
    setup(props) {
        const getBoardItemClasses = computed(() => {
            let classes = 'item ';

            if (props.field.value === FIELD.FILLED && props.gameStatus === GAME_STATUS.PREVIEW 
            || props.field.clicked && props.field.value === FIELD.FILLED) {
                classes += 'active';
            }

            if (props.field.clicked && props.field.value === FIELD.EMPTY) {
                classes += 'eror'
            }
                
            return  classes
            
        })

        return { 
            
            getBoardItemClasses 
        }

    },

    methods: {
        select(id) {
            if (this.gameStatus === GAME_STATUS.STARTED) {
                
                this.$emit('selectField', id);
            }
        }
    }
}

</script>


<style scoped>
    .item {
        position: relative;
        width: 50px;
        height: 50px;
        background: rgb(0, 0, 0);
        display: inline-block;
        margin: 5px;
        cursor: pointer;
        transition: .6s;
    }

    .item.active {
        background: #42b983cc;
        transform: rotateY(180deg);
    }
        
    .item.eror {
        background-color: rgba(255, 0, 0, 0.603);
        transform: rotateY(180deg);

    }
</style>