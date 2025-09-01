<template>
  <!-- ToDo List -->
  <div id="todoListPage" class="bg-half">
    <nav>
      <h1><a href="#">ONLINE TODO LIST</a></h1>
      <ul>
        <li class="todo_sm">
          <a href="#"><span>王小明的代辦</span></a>
        </li>
        <li><a href="#loginPage">登出</a></li>
      </ul>
    </nav>
    <div class="conatiner todoListPage vhContainer">
      <div class="todoList_Content">
        <div class="inputBox">
          <input type="text" v-model="newTodo" placeholder="請輸入待辦事項" />
          <a href="#" v-on:click="addTodo">
            <i class="fa fa-plus">+</i>
          </a>
        </div>
        <p>current input: {{ newTodo }}</p>
        <div class="todoList_list" v-if="todolist.length > 0">
          <ul class="todoList_tab">
            <li>
              <a href="#" @click.prevent="setActiveTab('all')" :class="{ active: activeTab === 'all' }">全部</a>
            </li>
            <li>
              <a href="#" @click.prevent="setActiveTab('pending')" :class="{ active: activeTab === 'pending' }">待完成</a>
            </li>
            <li>
              <a href="#" @click.prevent="setActiveTab('completed')"
                :class="{ active: activeTab === 'completed' }">已完成</a>
            </li>
          </ul>
          <div class="todoList_items">
            <ul class="todoList_item" v-for="todoitem in filteredTodos" :key="todoitem.id">
              <TodoItem :id="todoitem.id" :name="todoitem.name" :completed="todoitem.completed"
                @emitFinishFromList="finishFromList" @emitRemoveItem="removeItem" />
            </ul>
            <div class="todoList_statistics">
              <p>{{ todolist.length - completedCount }} 個待完成項目</p>
            </div>
          </div>
        </div>
        <div v-else>
          <p>目前尚無待辦事項</p>
          <img src="@/assets/nolist.svg" alt="">
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, computed, onMounted } from 'vue'
import TodoItem from '@/components/TodoItem.vue'

// Add reactive state for active tab
const activeTab = ref('all') // 'all', 'pending', or 'completed'
const newTodo = ref('')
// Set active tab function
function setActiveTab(tab) {
  activeTab.value = tab
}

const addTodo = () => {
  alert(`Add todo: ${newTodo.value}`)
  // console.log("Add todo: ", newTodo.value)
  todolist.value.push({
    id: todolist.value.length + 1,
    name: newTodo.value,
    completed: false,
  })
  newTodo.value = ''
}

const finishFromList = (todoItem) => {
  const removeItem = todolist.value.find((todo) => todo.id === todoItem.id)
  if (removeItem) removeItem.completed = !todoItem.completed
}
const removeItem = (id) => {
  todolist.value = todolist.value.filter(todo => todo.id !== id);
}

const todolist = ref([
  {
    id: 1,
    name: '把冰箱發霉的檸檬拿去丟',
    completed: true,
  },
  {
    id: 2,
    name: '打電話叫媽媽匯款給我',
    completed: false,
  },
  {
    id: 3,
    name: '整理電腦資料夾',
    completed: false,
  },
  {
    id: 4,
    name: '繳電費水費瓦斯費',
    completed: false,
  },
  {
    id: 5,
    name: '約vicky禮拜三泡溫泉',
    completed: false,
  },
  {
    id: 6,
    name: '約ada禮拜四吃晚餐',
    completed: false,
  },
])

// Filter todos based on active tab
const filteredTodos = computed(() => {
  if (activeTab.value === 'all') return todolist.value
  if (activeTab.value === 'pending')
    return todolist.value.filter((todo) => todo.completed === false)
  if (activeTab.value === 'completed')
    return todolist.value.filter((todo) => todo.completed === true)
  return todolist.value
})

// Count completed items
const completedCount = computed(() => {
  return todolist.value.filter((todo) => todo.completed === true).length
})

onMounted(() => {
  console.log('Component mounted!')
})
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC&display=swap');

html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}

/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}

body {
  line-height: 1;
}

ol,
ul {
  list-style: none;
}

blockquote,
q {
  quotes: none;
}

blockquote:before,
blockquote:after,
q:before,
q:after {
  content: '';
  content: none;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
}

* {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}

*,
*::before,
*::after {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.selector-for-some-widget {
  -webkit-box-sizing: content-box;
  box-sizing: content-box;
}

html {
  height: 100%;
}

body {
  font-family: 'Noto Sans TC';
  margin: 0 auto;
  overflow: hidden;
}

img {
  width: 100%;
  vertical-align: middle;
}

.logoImg {
  margin-bottom: 16px;
}

.vhContainer {
  height: 100vh;
}

.bg-yellow {
  background-color: #ffd370;
}

.bg-half {
  background-image: linear-gradient(175deg, #ffd370 60%, #fff 40%);
}

.conatiner {
  margin: 0 auto;
  padding: 87px 32px;
}

@media (max-width: 576px) {
  .conatiner {
    padding: 18px 32px;
  }
}

.side {
  width: 386px;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}

@media (max-width: 576px) {
  .side {
    width: 100%;
  }
}

nav {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  padding: 24px 32px 0 32px;
}

@media (max-width: 576px) {
  nav {
    margin-bottom: 16px;
  }
}

nav h1 a {
  width: 243px;
  height: 39px;
  background: url(https://upload.cc/i1/2022/03/23/8vTzYG.png) no-repeat;
  display: block;
  text-indent: 101%;
  overflow: hidden;
  white-space: nowrap;
}

nav ul {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  font-size: 1rem;
}

@media (max-width: 576px) {
  nav ul li {
    margin-top: 11px;
  }
}

nav ul a {
  text-decoration: none;
  color: #333333;
  margin-left: 24px;
}

@media (max-width: 576px) {
  nav ul a {
    margin-left: 0;
  }
}

nav ul a:hover {
  color: #d87355;
}

nav ul a span {
  font-weight: bold;
}

@media (max-width: 576px) {
  nav ul .todo_sm {
    display: none;
  }
}

.todoListPage {
  padding: 16px 32px;
}

@media (max-width: 576px) {
  .todoListPage {
    background-image: linear-gradient(175deg, #ffd370 100%, #fff 0%);
  }
}

.todoList_Content {
  width: 500px;
  margin: 0 auto;
}

@media (max-width: 576px) {
  .todoList_Content {
    width: 100%;
  }
}

.inputBox {
  width: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  position: relative;
  margin-bottom: 16px;
  -webkit-box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.15);
  box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.15);
}

.inputBox input {
  background: #fff;
  border: none;
  border-radius: 10px;
  position: relative;
  width: 100%;
  height: 47px;
  font-size: 1rem;
  padding-left: 16px;
}

.inputBox a {
  display: block;
  width: 40px;
  height: 39px;
  position: absolute;
  background: #333333;
  color: white;
  font-size: 20px;
  text-decoration: none;
  text-align: center;
  border-radius: 10px;
  top: 4px;
  right: 4px;
  padding: 10px;
}

.todoList_list {
  background: #fff;
  border-radius: 10px;
  -webkit-box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.15);
  box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.15);
}

.todoList_list .todoList_tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: space-evenly;
  -ms-flex-pack: space-evenly;
  justify-content: space-evenly;
}

.todoList_list .todoList_tab li {
  width: 100%;
}

.todoList_list .todoList_tab a {
  display: block;
  color: #9f9a91;
  text-decoration: none;
  line-height: 20px;
  font-weight: bold;
  text-align: center;
  padding: 16px;
  border-bottom: 2px solid #efefef;
}

.todoList_list .todoList_tab .active {
  color: #333333;
  border-bottom: 2px solid #333333;
}

.todoList_list .todoList_items {
  padding-top: 23px;
  padding-left: 24px;
  padding-right: 17px;
  padding-bottom: 32px;
}

.todoList_list .todoList_items .todoList_item {
  margin-bottom: 8px;
}

.todoList_list .todoList_items .todoList_label {
  width: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  border-bottom: 1px solid #e5e5e5;
  padding-bottom: 15px;
  color: #333333;
  line-height: 20.27px;
}

.todoList_list .todoList_items .todoList_input {
  width: 20px;
  height: 20px;
  border: 1px solid #9f9a91;
  border-radius: 5px;
  margin-right: 16px;
}

.todoList_list .todoList_items .todoList_input:checked~span {
  color: #9f9a91;
  text-decoration: line-through;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
}

.todoList_list .todoList_items li {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  margin-bottom: 17px;
}

.todoList_list .todoList_items li a {
  margin-left: 17px;
  display: block;
  font-size: 14px;
  color: #333333;
  opacity: 0;
}

.todoList_list .todoList_items li:hover a {
  opacity: 1;
}

.todoList_list .todoList_statistics {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
}

.todoList_list .todoList_statistics p {
  color: #333333;
  font-size: 0.875rem;
}

.todoList_list .todoList_statistics a {
  color: #9f9a91;
  font-size: 0.875rem;
  text-decoration: none;
}
</style>
