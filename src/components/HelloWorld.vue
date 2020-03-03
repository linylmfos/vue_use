<template>
  <div class="hello">
    <p>
      <input v-model.number="price" />
      <button @click="batchUpdate">批量更新价格</button>
    </p>
    <div class="course-list">
      <div v-for="c in courses" :key="c.name">{{c.name}} -- ${{c.price}}</div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      price: 0,
      course: '',
      courses: [],
      totalCount:0,
      show: false
    }
  },
  computed: {
    total() {
      return this.courses.length + "门";
    }
  },
  async created() {
    const courses = await this.getCourses();
    this.courses = courses;
  },
  methods: {
    getCourses() {
      return new Promise(resolve => {
        setTimeout(() => {
          resolve([{
            name: "web全站"
          }, {
            name: "web高级"
          }])
        }, 2000)
      });
    },
    batchUpdate() {
      this.courses.forEach(c => {
        // Vue.set(target, propertyName, value)
        Vue.set(c, 'price', this.price)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
