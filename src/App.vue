<template>
  <Header @open-menu="openMenu" @search="search"/>
  <div class="list" @scroll="onScroll(e)">
    <Table  :users="users" @open-edit="editMenu"/>
  </div>
  <AddUser v-if="addUserMenuVis" @close-addmenu="addUserMenuVis=false" @save-newuser="saveUser"/>
  <Menu v-if="menuVis"   @close-menu="menuVis=false" @add-user="addMenu"/>
  <EditUser :curuser="curuser" v-if="editVis" @close-edit="editVis=false" @save-user="saveEditUser" />
  
  
</template>

<script>
import Header from './components/header.vue'
import AddUser from './components/addUser.vue'
import Menu from './components/menu.vue'
import Table from './components/table.vue'
import EditUser from './components/editUser.vue'
import users from '../src/data/users.js'
export default {
  name: 'App',
  components: {
    Header,
    Table,
    AddUser,
    EditUser,
    Menu,
    
  },
  data(){
    return{
      users: null,
      oldCount: 0,
      menuVis: false,
      addUserMenuVis: false,
      editVis: false,
      curuser:null,
      oldUsers: null,
    }
  },
  mounted(){
    this.download(4);
  },
  methods:{
    onScroll(){
      let el = document.getElementsByClassName('list')[0]

     if(el.scrollTop + el.clientHeight==el.scrollHeight){
      this.downloadChunk(3)
     }
    },
    download(count){
      setTimeout(()=>{
        let arr = [];
        for (let i = this.oldCount; i<count; i++){
          console.log(i)
          arr.push(users[i])
          this.oldCount = i
        }
        this.users = arr;
        this.oldUsers = this.users;
        this.users.sort((a, b)=>a.mainName - b.mainName);  
        this.users = this.validate(this.users)
     
      }, 3000)
    },
    downloadChunk(count){
      let limit = null;
      if(this.oldCount>=users.length-1)limit = users.length; else limit = this.oldCount + count
      console.log('limit>', limit)
      setTimeout(()=>{
        for (let i = this.oldCount+1; i<limit; i++){
          this.users.push(users[i])
        }
        this.oldCount = this.oldCount + count-1;
        this.oldUsers = this.users;
        this.users.sort((a, b)=>a.mainName - b.mainName);  
        this.users = this.validate(this.users)
      }, 3000);
      
    },
 
    openMenu(){
      this.menuVis = true;
      let all = document.querySelectorAll('.disvis');
      all.forEach(item=>{
        let tr = item.parentElement;
          tr.parentElement.classList.remove('bkgrnd');
          item.classList.remove('disvis');
      })
     
    },
    addMenu(){
      this.addUserMenuVis = true;
      this.menuVis = false;
    },
    editMenu(id){
      this.editVis = true;
      this.menuVis = false;
      this.curuser   = this.users.find(item=>item.number == id)
      
    },
    saveUser(user){
      console.log(user)
      this.users.push(user)
      this.addUserMenuVis = false;
      this.users = this.validate(this.users)
    },
    saveEditUser(){
    
    // let index   = this.users.findIndex(item=>item.number == user.number);
    //  this.users.slice(index, 1);
     // this.users.push(user);
      this.editVis = false;
     // this.sortUsers();
     this.users = this.validate(this.users)
    },
    search(src){
      
      if (src=='') return this.users = this.oldUsers
			let arr = this.users.filter(item=>{
       let curr = null;
        if (!item.name) curr = item.secondName.toLowerCase();else curr = item.name.toLowerCase();
				
				//let bool = curr.includes(src.toLowerCase())
				if (curr.includes(src.toLowerCase())) return true;
			});
			this.users = arr;
		},
    validate(users){
      console.log(users) 
        users.map(item=>item.name? item.mainName = item.name : item.mainName = item.secondName)
        users.sort((a, b)=>a.mainName - b.mainName);  
        console.log(users)  
        return users
    }
  }
}
</script>

<style>
 * {
    margin: 0;
    padding: 0;
   }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.list{
  display: flex;
  margin-top:-1px;
  height: 30vh;
  background-color: whitesmoke;
  justify-content: center;
  overflow-y: scroll;
  overflow-x: hidden;
}
</style>
