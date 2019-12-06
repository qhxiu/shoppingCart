<template>
  <div>
    <h2>购物车</h2>
    <table>
      <tr>
        <td>勾选</td>
        <td>课程名称</td>
        <td>课程价格</td>
        <td>数量</td>
        <td>价格</td>
      </tr>
      <tr v-for="(item, index) in courseItem" :key="item.id" :class="item.checked ? 'red' : ''">
        <td>
          <input type="checkbox" v-model="item.checked">
        </td>
        <td>{{item.name}}</td>
        <td>{{item.price}}</td>
        <td>
          <button @click="minus(index)">-</button>
          {{item.num}}
          <button @click="add(index)">+</button>
        </td>
        <td>{{item.price*item.num}}</td>
      </tr>
      <tr>
        <td></td>
        <td colspan="2">{{isAcitveCourse}}/{{allCourseList}}</td>
        <td colspan="2">{{allPrice}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
    export default {
        name: "Cart",
        data() {
            return {

            }
        },
        props: {
            //遵守单向数据流
            courseItem: Array
        },
        methods: {
            minus(index) {
                let num = this.courseItem[index].num;
                if (num > 1) {
                    this.courseItem[index].num -= 1;
                } else {
                    if (window.confirm('确定要删除吗？')) {
                        this.$emit('removeItem', index)
                    }
                }
            },
            add(index) {
                this.courseItem[index].num += 1;
            }
        },
        computed: {
            isAcitveCourse() {
                return this.courseItem.filter(item => {
                    return item.checked
                }).length;
            },
            allCourseList() {
                return this.courseItem.length;
            },
            allPrice() {
                let total = 0;
                this.courseItem.forEach(item => {
                    if (item.checked) {
                        total += item.price * item.num
                    }
                });
                return total;
            }
        }
    }
</script>

<style scoped>
  .red td {
    color: red;
  }
</style>