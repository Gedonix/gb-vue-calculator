<template>   
    <div class="operation">
        <div class="show_sign">
            <span :class="activeClass" id='sign'></span>
        </div>
        <button class="clean_btn" @click="$emit('clean'), changeClass('fas fa-calculator')">
            <span class="fas fa-broom"></span>
        </button>
        <div class="btn_wrapper">
            <button
                v-for="(action, idx) in actions"
                :key="idx"
                @click="$emit('calculate', action.sign), changeClass(action.font)"
            >
                <span :class="action.font"></span>
            </button>
        </div>
    </div>

</template>

<script>
export default {
    name: 'Button',
    emits: ["calculate", "clean"],
    data() {
        return {
            activeClass: 'fas fa-calculator',
            actions: [
                {sign: '+', font: 'fas fa-plus'},
                {sign: '-', font: 'fas fa-minus'},
                {sign: '*', font: 'fas fa-times'},
                {sign: '/', font: 'fas fa-divide'},
                {sign: 'e', font: 'fas fa-superscript'},
                {sign: 'i', font: 'fas fa-percentage'},
            ]
        }
    },
    methods: {
        changeClass(font){
            this.activeClass = font;
        }        
    }
}
</script>

<style>

</style>
