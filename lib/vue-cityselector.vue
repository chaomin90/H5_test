<template>
  <div class="city-selector" v-if="citys && citys.length > 0">
    <div class="selected-list">
      已选择城市：
      <div 
        class="item" 
        v-for="(item, index) in activeCitys" 
        :key="item.id">
        {{item.name}}
        <span @click="removeCity(index)">×</span>
      </div>
    </div>
    <!-- <div class="hot-citys">
      热门城市：
      <div class="hot-city-item">
        <span>城市名</span>
      </div>
    </div> -->    
    <div class="citys-container clearfix">
      <div class="container-left">
        <div class="city-options">
          <div 
            class="options-item"
            :class="{'active' : currentCitys.id == item.id}"
            v-for="(item, index) in citys"
            :key="item.id"
            @click="selectOption(index)">
            {{item.name}}
          </div>
        </div>
      </div>
      <div class="container-right">
        <div class="city-list clearfix">
          <div 
            class="city-item" 
            :class="{'active' : isSelected(item)}" 
            v-for="item in currentCitys.options" 
            :key="item.id">
            <span @click="selectCity(item)">{{item.name}}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'vue-city-selector',
  created () {
    if (!this.citys) throw new Error('请传入数据')
    this.currentCitys = this.citys[0]
    this.activeCitys = JSON.parse(JSON.stringify(this.value))
  },
  data () {
    return {
      activeCitys: [],
      currentCitys: [],
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
  model: {
    prop: 'value',
    event: 'changeCity'
  },
  watch: {
    // 监听选中城市的变化
    activeCitys: {
      handler (newValue, oldValue) {
        let value = JSON.parse(JSON.stringify(this.activeCitys))
        this.$emit('changeCity', value)
      },
      deep: true
    }
  },
  props: {
    value: {
      type: Array,
      default: () => {
        return []
      }
    },
    data: {
      type: Array
    },
    max: {
      type: Number,
      default: 2
    }
  },
  methods: {
    // 判断是否存在
    isSelected (city) {
      let res = this.activeCitys.filter(item => {
        return item.id == city.id
      })
      return res.length > 0 ? true : false
    },
    // 选择城市
    selectCity (city) {
      if (this.isSelected(city)) return
      let limitMax = this.activeCitys.length >= this.max
      if (limitMax) {
        this.activeCitys.splice(-1, 1)
      }
      this.activeCitys.push(city)
    },
    // 移除选中的城市
    removeCity (index) {
      this.activeCitys.splice(index, 1)
    },
    // 点击左侧选项
    selectOption (index) {
      this.currentCitys = this.citys[index]
    }
  }
}
</script>

<style lang="scss">
.clearfix:before, .clearfix:after {
  display: block;
  content: '';
  clear: both;
  height: 0;
  visibility: hidden;
}
.city-item-span {
  display: inline-block;
  padding: 4px 8px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 100%;
  border-radius: 3px;
  cursor: pointer;
  &:hover {
    background-color: #f0f8ff;
  }
}
.city-selector {
  max-width: 800px;
  border: 1px solid #ededed;
  font-size: 14px;
  .selected-list {
    border: 1px solid #ededed;
    border-left: none;
    border-right: none;
    padding: 14px;
    line-height: 26px;
    .item {
      display: inline-block;
      position: relative;
      vertical-align: middle;
      line-height: 26px;
      padding: 0 16px 0 6px;
      border: 1px solid #73C1B1;
      color: #73C1B1;
      border-radius: 3px;
      + .item {
        margin-left: 8px;
      }
      > span {
        cursor: pointer;
        position: absolute;
        right: 2px;
        top: 50%;
        margin-top: -6px;
        height: 12px;
        width: 12px;
        line-height: 12px;
        text-align: center;
      }
    }
  }
  .hot-citys {
    padding: 8px 14px;
    .hot-city-item {
      display: inline-block;
      vertical-align: middle;
      > span {
        @extend.city-item-span;
      }
    }
  }
  .citys-container {
    > * {
      float: left;
    }
    .container-left {
      min-height: 300px;
      width: 20%;
      background-color: #fafafa;
      .city-options {
        .options-item {
          padding: 10px 16px;
          cursor: pointer;
          &:hover {
            background-color: #f0f8ff;
          }
          &.active {
            background-color: #fff;
            color: #73C1B1;
            &:hover {
              background-color: #fff;
            }
          }
        }
      }
    }
    .container-right {
      width: 80%;
      .city-list {
        .city-item {
          padding: 6px 16px;
          text-align: center;
          float: left;
          width: 10%;
          > span {
            @extend.city-item-span; 
          }
          &.active {
            > span {
              background-color: #73C1B1;
              color: #fff;
            }
          }
        }
      }
    }
  }
}
</style>