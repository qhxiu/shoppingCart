<template>
  <div>
    <h1>购物车</h1>
    <hr>
    <h3>添加课程</h3>
    <label for="">课程名称：</label><input v-model="courseInfo.name" type="text" />
    <label for="">课程价格：</label><input v-model="courseInfo.price" type="text" />
    <button @click="addClass">添加课程到列表</button>
    <hr>
    <h3><span>课程名称</span><span>课程价格</span></h3>
    <div v-for="(item, index) in list" :key="item.id">
      <span>{{item.name}}</span>&nbsp;&nbsp;
      <span>{{item.price}}</span>&nbsp;&nbsp;
      <button @click="addCart(index)">添加到购物车</button>
    </div>
    <hr>
    <cart :courseItem="courseItem" @removeItem="remove"></cart>
  </div>
</template>

<script>
  import Cart from './Cart'
    export default {
        name: "ShoppingCart",
        components: {
            Cart
        },
        data() {
            return {
                courseInfo: {
                    name: '',
                    price: ''
                },
                list: [],
                cartList: [],
                courseItem: [],
                count: 0
            }
        },
        methods: {
            addClass() {
                this.courseInfo.id = (this.count++) + 1;
                this.list.push(JSON.parse(JSON.stringify(this.courseInfo)));
            },
            addCart(index) {
                let item = this.list[index];
                let isHasCourse = this.courseItem.find(x => x.id == item.id);
                if (isHasCourse) {
                    isHasCourse.num += 1;
                } else {
                    this.courseItem.push({
                        ...item,
                        num: 1,
                        checked: true
                    });
                }
            },
            remove(index) {
                this.courseItem.splice(index, 1);
            }
        }
    }
</script>

<style scoped>

</style>