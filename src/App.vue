<template>
  <div class="page">
    <vue-city-selector v-model="value" :data="citys" :max="3"/>
  </div>
</template>

<script>
import VueCitySelector from '../lib/vue-cityselector.vue'

export default {
  data () {
    return {
      value: [
        {
          id: '1',
          name: '深圳'
        }
      ],
      citys: [
        {
          id: 'hot',
          name: '热门城市',
          options: [
            {
              id: '0',
              name: '北京'
            },
            {
              id: '1',
              name: '深圳'
            },
            {
              id: '2',
              name: '广州'
            }
          ]
        },
        {
          id: 'abc',
          name: 'A B C',
          options: [
            {
              id: '3',
              name: '阿坝'
            },
            {
              id: '4',
              name: '阿克苏'
            },
            {
              id: '5',
              name: '阿拉尔'
            },
            {
              id: '6',
              name: '阿拉善盟'
            },
            {
              id: '7',
              name: '阿拉善盟'
            },
            {
              id: '8',
              name: '阿勒泰'
            },
          ]
        },
        {
          id: 'defg',
          name: 'D E F G',
          options: [
            {
              id: '9',
              name: '达州'
            },
            {
              id: '10',
              name: '大理'
            },
            {
              id: '11',
              name: '大连'
            },
            {
              id: '12',
              name: '大庆'
            },
            {
              id: '13',
              name: '大同'
            },
            {
              id: '14',
              name: '大兴安岭'
            },
          ]
        },
      ]
    }
  },
  components: {
    VueCitySelector
  }
}
</script>

<style lang="scss">
</style>