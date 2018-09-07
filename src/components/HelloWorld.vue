<template>
  <div>

    <div class="container">
      <p>todos</p>
      <input @keyup.enter='add(listData,val)' v-model="val" type="text" class="inputStyle" placeholder="please write your todos">
      <button @click='add(listData,val)'>添加</button>
      <div class="item">
        <ul>
          <li v-for='(item,index) in listData' :key='index'>{{item}}
            <button class="remove" @click='remove(listData,index)'>删除</button>
          </li>
        </ul>
        <div class="footer" @click='clickBtn'>
          <button ref='btns' v-for='(item,index) in btns' :key='index'>{{item}}</button>
        </div>
      </div>
    </div>
  </div>

</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
import { Prop, Watch, Provide } from 'vue-property-decorator'

@Component({
  // 这里放vue实例的配置
  // props的第一种写法，需要在下声明一下才可以使用
  // props: {width: Number, ratio: Number}
})
export default class Swiper extends Vue {
  // data
  @Provide() val: String = ''
  @Provide() listData: Array<Object> = []
  @Provide() message: String = 'test'
  @Provide() btns: Array<Object> = ['all', 'active', 'completed']
  // props的第一种写法, props声明
  // width: Number
  // ratio: Number

  // vue实例中的data属性这样写
  scrollWidth: number = window.screen.availWidth
  // ref 子组件的引用
  $refs: {
    // button: Button
  }

  // 生命周期
  mounted() {}
  // props的第二种写法
  @Prop() width: Number
  @Prop() ratio: Number
  @Prop() swiperData: Array<Object>
  @Prop() value: String
  // 计算属性
  get swiperStyle(): any {
    return ''
  }
  // watch
  @Watch('$route')
  onRouteChanged(route: any, oldRoute: any): void {}
  // 函数方法可以直接写
  getData(data): void {
    return data
  }
  add(list: Array<Object>, val: String) {
    if (val) {
      list.push(val)
      this.val = ''
    }
  }
  remove(list: Array<Object>, i: any) {
    list.splice(i, 1)
  }
  clickBtn(event: any) {
    if (this.$refs['btns']) {
      this.$refs['btns'].forEach(element => {
        element.classList.remove('active')
      })
    }
    event.target.classList.add('active')
  }
}
</script>

<style lang="scss" scoped>
p {
  color: blueviolet;
}
.container {
  width: 500px;
  border: 1px solid gainsboro;
  border-radius: 5px;
  margin: 0 auto;
  box-shadow: 2px 2px 2px grey;
  padding: 10px;
}
.inputStyle {
  -web-kit-appearance: none;
  -moz-appearance: none;
  font-size: 1em;
  height: 1.7em;
  border-radius: 4px;
  border: 1px solid #c8cccf;
  color: #6a6f77;
  width: 80%;
}
button {
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 5px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  // font-size: 16px;
  border-radius: 4px;
  outline: none;
}
.remove {
  float: right;
  background-color: red;
}
ul {
  padding: 0px;
}
li {
  list-style: none;
  line-height: 30px;
  text-align: left;
  border-bottom: 1px solid #c8cccf;
  padding: 10px 0;
}
.item {
  margin: 5px;
}
.footer {
  line-height: 30px;
  display: flex;
}
.footer button {
  margin: 0px 5px;
  background: white;
  color: black;
}
.footer .active {
  background-color: #4caf50;
  color: white;
}
</style>
