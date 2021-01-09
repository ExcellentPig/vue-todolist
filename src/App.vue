<template>
  <div>
     <input 
       type="text" 
       placeholder="请输入需要添加的项目"
       v-model="value"
      >
     <button @click="add(value)">添加</button>
     <h3>未完成的项目</h3>
     <div 
         v-for="(item, index) in inputValue" 
        :key="index"
      >
       <p v-if="!item.isOk">{{ item.value }} --- <span @click="complate(item)">点击完成该项目</span> --- <span @click="del(item)">点击删除该项目</span></p>
     </div>
     <h3>已完成的项目</h3>
     <div
         v-for="(item, index) in isok" 
        :key="index"
      >
       <p>{{ item.value }}</p>
     </div>
     <hr>
     <div class="tip">说明：输入内容后点击添加，内容会进入未完成的项目，点击完成该项目内容会进入已完成的项目中，点击删除可以删除该项目</div>
  </div>
</template>
<script>
import { mapState, mapActions, mapGetters } from 'vuex'
export default {
  data () {
    return {
       value: ''
	}
  },
  computed: { 
    ...mapState({
       inputValue: 'inputValue'
	}),
    ...mapGetters(['isok'])
  },
  methods: {
    add (value) {
       if (this.value == '') {
         return
       } else {
         this.addItem(value)
         this.value = ''
       }
       //console.log(value)
    },
	...mapActions(['addItem']),
    del (item) {
       this.$store.dispatch('toDel', item)
    },
    complate (item) {
        item.isOk = true
        console.log(item.isOk)
    }
  }
}
</script>
<style lang="stylus">
span {
  cursor pointer
}
.tip {
  color: red
  font-weight: bold
}
</style>
