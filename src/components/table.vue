<template>
  <table>
    <thead >
      <tr class="headerTable sdvig">
          <th class="logo">
            <img class="logosvg" src="../assets/points.svg">
          </th>
          <th class="name">
            <span>Имя</span>
          </th>
          <th class="number">
            <span>Телефон</span>
          </th>
          <th class="addres">
            <span>Адрес</span>
          </th>
          <th class="mail">
            <span>Электронная почта</span>
          </th>
          <th class="button">
            <span></span>
          </th>
      </tr>
    </thead>
    <tbody >
      <tr v-for="item in users" :key="item" class="headerTable body"  :id="item.number" @click="chooseItem(item.number)">
        <th class="logo">
          <div class="imgWriper">
            <img class="img" :src="item.avatar">
          </div>
          
        </th>
        <th class="name">
          <span>{{item.mainName}}</span>
        </th>
        <th class="number">
          <span>{{item.number}}</span>
        </th>
        <th class="addres left">
          <span>{{item.addres}}</span>
        </th>
        <th class="mail">
          <span>{{item.mail}}</span>
        </th>
        <th class="button">
          <div class="vis" @click="openEditMenu(item.number)">
            <span>Редактировать</span>
          </div>
        </th>
      </tr>
    </tbody>
  </table>

</template>

<script>

export default {
  name: 'TableList',
  props: {
    users:{
      type: Array,
      required: true,
     
  }
 },
  data(){
    return{

    }  
  },
  methods:{
    chooseItem(e){ 
     
      let all = document.querySelectorAll('.disvis');
      all.forEach(item=>{
        let tr = item.parentElement;
          tr.parentElement.classList.remove('bkgrnd');
          item.classList.remove('disvis');
      })
      let el  = document.getElementById(e)
      let but = el.querySelector('.vis'); 
      el.classList.add('bkgrnd');
      but.classList.add('disvis');
      
    },
    openEditMenu(id){

      this.$emit('open-edit', id );
    }
  },
  mounted(){
    //this.download(6)
        
  },
  computed:{
    

  }

 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.headerTable {
  display: flex;
  align-items: center;
  box-shadow: 0px 5px 5px -5px rgba(0, 1, 2, 0.6);
  margin: 0 ;
  background-color: rgb(253, 255, 253);
  height: 60px;
  width: 100vw;
  z-index: 0;

}
.sdvig{
  margin-top: -2px;

}
.body{
  margin-top: 2px;
  box-shadow: 0px 0px 0px -0px rgba(0, 1, 2, 0.6);
  margin-left: auto;
  margin-right: auto;
}
.body:hover{
  background-color:rgb(202, 223, 242);
}
.left{
  width: 52%;
}
.imgWriper{
  display: flex;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
}
.img{
 width: 100vw;
}
.logosvg{
  width: 70%;
}
thead {
  position: sticky;
  top: 2px;
  background: white;
}
.logo{
  display: flex;
  justify-content: center;
  width: 10%;
}

.name{
  display: flex;
  justify-content: left;
  width: 20%;
}
.number{
  display: flex;
  justify-content: left;
  width: 20%;
  font-weight: bolder;
}
.addres{
  display: flex;
  justify-content: left;
  width: 30%;
}
.mail{
  display: flex;
  justify-content: left;
  width: 20%;
}
span{
  margin-left: 10px;
 
}
.button{
  display: flex;
  justify-content: center;
  width: 30%;
  color: #273B69;
  cursor: pointer;
}
.vis{
  display: none;
  align-items: center;
  height: 35px;
  width: 150px;
  border-radius: 5px;
  background-color: white;
  color: #273B69;
 
  border-width: 2px;
  cursor: pointer;
}
.disvis{
  display: flex;
  
}
.bkgrnd{
 background-color:rgb(202, 223, 242);;
}

</style>
