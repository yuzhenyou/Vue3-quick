<template>
  <div class='layout'>
    <menu class="menu">
      <div class="menu_header">目录</div>
      <ul>
        <li v-for="item in menuList" :key="item.path" :class="active == item.path ? 'activeMenu' : ''"
          @click="goPath(item)">
          {{ item.title }}
        </li>
      </ul>
    </menu>
    <main class="main">
      <router-view></router-view>
    </main>
  </div>
</template>

<script>
import { defineComponent, reactive, toRefs, onMounted } from 'vue'
import { useRouter, useRoute } from 'vue-router'
export default defineComponent({
  setup() {
    let state = reactive({
      menuList: [
        { title: '1.ref 函数', path: '/ref' },
        { title: '2.reactive 函数', path: '/reactive' },
        { title: '3.响应式原理', path: '/proxy' },
        { title: '4.计算属性computed', path: '/computed' },
        { title: '5.监听watch', path: '/watch' },
        { title: '6.生命周期', path: '/lifecycle' },
        { title: '7.hooks', path: '/hooks' },
        { title: '8.toRef与toRefs', path: '/toRef' },
        { title: '9.shallowReactive 与 shallowRef', path: '/shallowReactive' },
        { title: '10.readonly 与 shallowReadonly', path: '/readonly' },
        { title: '11.toRaw 与 markRaw', path: '/toRaw' },
        { title: '12.customRef', path: '/customRef' },
        { title: '13.provide 与 inject', path: '/provide' },
        // { title: '问题', path: '/question' },
        { title: 'Element Plus', path: '/elementPlus' },
      ],
      active: '/'
    })
    let router = useRouter();
    let route = useRoute();
    let stateAsRefs = toRefs(state);
    const goPath = (item) => {
      router.push({ path: item.path })
      state.active = item.path;
    }
    onMounted(() => {
      state.active = route.path
    })
    return {
      goPath,
      ...stateAsRefs,
    }
  }


})
</script>

<style lang='scss' scoped>
.layout {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: flex-start;
  flex-wrap: nowrap;

  .menu {
    width: 260px;
    height: 100%;
    border-right: 1px solid #eee;
    padding: 10px 10px;
    box-sizing: border-box;

    .activeMenu {
      color: #409EFF;
    }

    .menu_header {
      text-align: center;
      color: #67C23A;
      width: 90%;
      padding: 10px 0;
      border-bottom: 1px solid #eee;
      margin: 0 auto 20px;
    }

    ul li {
      margin-bottom: 10px;
      text-align: left;

    }

    ul li:hover {
      text-decoration: underline;
      cursor: pointer;
      color: #409EFF;
    }
  }

  .main {
    flex: 1;
    padding: 10px 10px;
    box-sizing: border-box;
  }
}
</style>
