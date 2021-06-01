<template> 
    <div class="nkp_wrapper">
        <div class="show_nkp">
            <input type="checkbox" id="checkbox" v-model="checked" />
            <label for="checkbox" style="padding-left: 10px">Отобразить экранную клавиатуру</label>
        </div>
        <div class="numkeypad" v-show="checked">
            <div class="button_nkp">
                <button
                    v-for="item in buttons"
                    :key="item"
                    v-text="item"
                    @click="$emit('ekeypad', item)"
                ></button>
            </div>
            <div class="choose_op">
                <input type="radio" id="one" value="1" v-model="picked" />
                <label for="one" style="padding: 0 10px 0 5px">Верхний операнд</label>            
                <input type="radio" id="two" value="2" v-model="picked" />
                <label for="two" style="padding-left: 5px">Нижний операнд</label>
            </div>
        </div>        
    </div>
</template>

<script>
export default {
  name: 'Numkeypad',
  emits: ["ekeypad", "toggleHandle"],  
  data() {
    return {
        checked: false,
        picked: '1',
        buttons:['0','1','2','3','4','5','6','7','8','9','←']
    }
  },
  watch: {
    picked(value){
        this.$emit('toggleHandle', value)
    }
  }
}
</script>

<style>
</style>