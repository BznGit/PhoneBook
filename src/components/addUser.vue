<template>
  <div class="back"></div>
  <div class="main">
      <div class="text">
        <span>Добавить пользователя</span>
      </div>
      <div class="image">
        <div class="imgcont" >
          <img  id="foto1" src="../assets/user.svg">
        </div>
        <img  class="im" @click="addFile" src="../assets/edit.svg">
      </div>
      <div class="inputs">
        <input type="text" placeholder="Имя" v-model="user.name">
        <input type="text" placeholder="Фамилия" v-model="user.secondName">
        <input type="text" placeholder="Номер" v-model="user.number">
        <input type="text" placeholder="Электронная почта" v-model="user.addres">
        <input type="text" placeholder="Адрес" v-model="user.mail">
      </div>
      <div class="butGrup">
        <div class="sv" @click="save">
            <span>СОХРАНИТЬ</span>
        </div>
        <div class="cl" @click="cansel">
          <span>ОТМЕНА</span>
        </div>
      </div>
  </div>
    
  
</template>

<script>
export default {
  name: 'AddUser',
  props: {
    msg: String
  },
  data(){
    return {
      user: {
        name:null,
        number: null,
        secondName: null,
        addres: null,
        mail:null,
        avatar:'./user.svg'
      }

      }
    },

  methods:{
    cansel(){
      console.log('ddddd')
      this.$emit("close-addmenu")
    },
    save(){
      this.$emit("save-newuser", this.user)
    },
     addFile(){

      let input = document.createElement('input' );
      input.type = 'file';
      input.setAttribute('multiple','')
      input.click();
      input.onchange = (e) => {
      document.getElementById('foto1').src =  URL.createObjectURL(e.target.files[0]);
      this.user.avatar = URL.createObjectURL(e.target.files[0]);
      console.log( e.target.files[0] )
      };		
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.back{
  position: absolute;
  top:0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: gray;
  opacity: 0.7;

}
.main{
  display: flex;
  flex-direction: column;
  position: absolute;
  top:25%;
  left: 30%;
  height: 500px;
  width: 500px;
  background-color: aliceblue;
  border-radius: 10px;
  justify-content: center;
 
}
.text{
  align-items: center;
  margin-top: 20px;
  color: #273B69;
  font-weight: bolder;
}
.imgcont{
  margin-top: 20px;
  align-self: center;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
}     

img{
   height: 80px;
}
.image{
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.im{
  height: 20px;
 align-self: end;
 cursor: pointer;
}
.im:hover{
  transform: scale(1.2);
}
.inputs{
  display: flex;
  align-self: center;
  align-items: center;
  flex-direction: column;
  
  
}
input{
  margin-top: 20px;
  height: 30px;
  background-color: aliceblue;
  border-radius: 10px;
  border-color: #273B69;
  width: 280px;
}
input:focus{
  border-color: red;
}
input::-webkit-input-placeholder { color: gray; text-align:center;}
.butGrup{
  display: flex;
  flex-direction: row;
  margin-top: 20px;
  justify-content: space-between;
  color: #273B69;
  font-weight: bolder;
}
.sv{
  display: flex;
  width: max-content;
   margin-left: 110px;
   cursor: pointer;
   width: 140px;
   height: 30px;
   border-radius: 10px;
   justify-content: center;
   align-items: center;
}
.cl{
  display: flex;
  width: max-content;
   margin-right: 110px;
   cursor: pointer;
   width: 140px;
   height: 30px;
   border-radius: 10px;
   justify-content: center;
   align-items: center;
}

.sv:hover{
  color: white;
  background-color: #273B69;
}
.cl:hover{
  color: white;
  background-color: #273B69;
}
</style>
