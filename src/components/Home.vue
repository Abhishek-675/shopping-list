<template>
  <h1>Shopping List</h1>
  <form action="">
    <input @keypress="add2($event)" ref="input" type="text" placeholder="Add items" v-model="input">
    <button @click="add" type="button" class="add-btn">Add</button>
  </form>
  <h2>Items</h2>
  <h3>{{ input }}</h3>
  <div class="ol-div">
    <ol>
      <li v-for="item in list" :key="item"><span>{{ item }}</span><button @click="del($event)" type="button"
          class="danger-btn">Delete</button></li>
    </ol>
  </div>
  <div id="shopping-items">
    <h3>Shopping Items</h3>
    <div>
      <span v-for="item in list" :key="item">{{ item }}, </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home-1',
  data() {
    return {
      input: '',
      list: []
    }
  },
  methods: {
    add() {
      if (this.input === '') {
        alert('Input filed cannot be empty')
        return
      }
      this.list.push(this.input);
      this.input = '';
    },
    add2(e) {
      if (e.key === 'Enter') {
        e.preventDefault()
        this.add()
      }
    },
    del(e) {
      const toBeRemoved = e.target.parentNode.firstElementChild.textContent;
      // console.log(this.list)
      const filtered = this.list.filter(item=>{
        return item !== toBeRemoved
      })
      // console.log(filtered);
      this.list = filtered;
    }
  },
  mounted(){
    this.$refs.input.focus();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

ol{
  padding: 0;
}

li {
  margin: 10px 0;
  font-size: 24px;
  display: flex;
  justify-content: space-between;
}

h1,
h2,
h3 {
  text-align: center;
}

h3{
  min-height: 30px;
}

a {
  color: #42b983;
}

form {
  display: flex;
  margin: auto;
  width: 500px;
  justify-content: space-between;
}

input {
  padding: 10px;
  width: 300px;
  border: 1px solid skyblue;
}

input:focus {
  outline: 1px solid rgb(9, 170, 234);
}

::placeholder {
  font-size: 18px;
}

.add-btn {
  padding: 10px 30px;
  cursor: pointer;
  background: rgb(8, 148, 203);
  border: 1px solid skyblue;
  color: white;
  font-size: 18px;
}

.ol-div {
  width: 500px;
  margin: auto;
  height: 400px;
  overflow: auto;
  padding: 0 40px;
}

.danger-btn {
  margin-left: 20px;
  background: red;
  border: none;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}

#shopping-items{
  width: 600px;
    margin: auto;
}
</style>
