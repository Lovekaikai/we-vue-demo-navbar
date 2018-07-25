<template>
  <div>
    <!-- <div class="page-infinite-wrapper" ref="wrapper" :style="{ height: wrapperHeight + 'px' }">
    <wv-group
      title="无限滚动加载"
      v-infinite-scroll="loadMore"
      infinite-scroll-disabled="loading"
      infinite-scroll-distance="50"
    >
      <wv-cell title="条目" v-for="item in list" :key="item" :value="item"/>
    </wv-group>
    <p v-show="loading" class="loading-tips">
      <wv-spinner type="snake" color="#444" :size="24"/>
    </p>
  </div> -->
    <wv-navbar v-model="selected" @change="changed" fixed>
      <wv-navbar-item id="1">选项1</wv-navbar-item>
      <wv-navbar-item id="2">选项2</wv-navbar-item>
      <wv-navbar-item id="3">选项3</wv-navbar-item>
    </wv-navbar>
    <component :is="hasShop"></component>
  </div>
</template>
<script>
import Item1 from './1'
import Item2 from './2'
import Item3 from './3'
export default {
  data () {
    return {
      list: [],
      loading: false,
      allLoaded: false,
      wrapperHeight: 0,
      selected: '',
      hasShop: Item1
    }
  },
  comments: {
    Item1,
    Item2,
    Item3
  },
  methods: {
    changed (val) {
      if (val === '1') {
        this.hasShop = Item1
      } else if (val === '2') {
        this.hasShop = Item2
      } else {
        this.hasShop = Item3
      }
    },
    loadMore () {
      console.log('loading more')
      this.loading = true
      setTimeout(() => {
        let last = this.list[this.list.length - 1]
        for (let i = 1; i <= 5; i++) {
          this.list.push(last + i)
        }
        this.$nextTick(() => {
          this.loading = false
        })
      }, 2000)
    }
  },

  mounted () {
    // this.wrapperHeight =
    //   document.documentElement.clientHeight -
    //   this.$refs.wrapper.getBoundingClientRect().top
    // for (let i = 1; i <= 15; i++) {
    //   this.list.push(i)
    // }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
