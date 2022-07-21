<template>
    <div class="apple" :style="{top: this.pos[1] + 'px', left: this.pos[0] + 'px'}"></div>
</template>

<script>
    export default {
        props:['pos'],
        components: {},
        data() {
            return {
                
            }
        },
        computed: {
            
        }, 
        methods: {
            
        }
    }
</script>

<style scoped>
.apple {
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: red;
}
</style>