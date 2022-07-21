<template>
    <template v-for="piece in state" :key="piece.key">
        <div class="snake" :style="{left: piece.pos[0] + 'px', top: piece.pos[1] + 'px'}"></div>
    </template>
</template>

<script>
    export default {
        props:['state'],
        components: {},
        data() {
            return {
                
            }
        },
        computed: {
            snakeTail() {
                let snakePieces = [];
                for (let i=0; i<=this.state; i++) {
                    snakePieces.push(i);
                }
                return '';
            }
        }, 
        methods: {
            
        }
    }
</script>

<style scoped>
.snake {
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: green;
}
</style>