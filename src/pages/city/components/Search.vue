<template>
   <div class="search">
     <input class="search-input" type="text" placeholder="输入城市名或拼音" v-model="keyword">
     <div class="search-content">
       <ul>
         <li v-for="item in list">{{item.name}}</li>
       </ul>
     </div>
   </div>
</template>

<script>
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
      }, 100)
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .search
    height : .72rem
    padding: 0 .1rem
    background: $bgColor
    .search-input
      box-sizing :border-box
      padding : 0 .1rem
      width : 100%
      height: .62rem
      line-height: .62rem
      text-align : center
      border-radius : .06rem
      color: #666
  .search-content
    position absolute
    overflow :hidden
    z-index :1
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
</style>
