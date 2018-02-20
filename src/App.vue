<template>
  <div id="app">


   <div class="container-fluid">

     <alert v-model="show" placement="top" duration="3000" type="success" width="400px" dismissable>
  <span class="icon-ok-circled alert-icon-float-left"></span>
  <strong>Alert!</strong>
  <p>{{status}}</p>
</alert>

    <div class="jumbotron jumbotron-fluid">
     <div class="container-fluid">
      <h1 class="display-4">Welcome to Buffer-App</h1>
      <p class="lead">This app is experiment on producer-consumer business modal</p>
    </div>
  </div>
  

<div class="main">
  <div class="row">
    <div class="col-lg-6 col-md-8 offset-md-2 col-sm-10 offset-sm-1 ">
      <div class="container-fluid">

<div class="row">
  <div class="col-lg-12">
    <h1 class="display-4">Ready to Produce</h1>
<button type="button" @click="produce" class="btn btn-primary">Produce <i class="fa fa-plus-circle" aria-hidden="true"></i>
</button>

<div v-show="clicked" class="d-block mt-4 ">
  <p class="lead">{{loading?"Generating your magic Number":"Number Generated..."}} </p>

<div class="status">
  <template v-if="loading">
    <i class="fa fa-circle-o-notch fa-spin fa-3x fa-fw"></i>
  <span class="sr-only">Loading...</span>
  </template>
<template v-else>
  <p class="lead">{{randomNumber}}</p>
</template>
</div>


</div>


  </div>
    <div class="col-lg-12">
        <h1 class="display-4">You can consume</h1>
    <button @click="consume" type="button" class="btn btn-secondary">Consume <i class="fa fa-minus-circle" aria-hidden="true"></i>
</button>
  </div>
</div>

      </div>
     
    </div>
    <div  class="col-lg-6 mr-0 col-md-8 offset-md-2 col-sm-10 offset-sm-1">
         
            <p class="lead">History <span class="badge badge-secondary">{{total}}</span></p>
            <div class="row">
              <div class="col-lg-5 offset-lg-1">
                <p class="lead">Producer <span class="badge badge-secondary">{{producer}}</span></p>
              <div class="h-divider"></div>
              <div class="history-list bg-light">
                <ul>
  <li v-for="items in producer_history " ><p class="bg-primary ">produced <span class="badge badge-secondary">{{items.value}}</span></p></li>
                </ul>
              </div>
              </div>
              <div class="col-lg-5 offset-lg-1">
                 <p class="lead">Consumer<span class="badge badge-secondary">{{consumer}}</span></p>
                  <div class="h-divider"></div>
                   <div class="history-list bg-dark">
               <div class="history-list bg-light">
                           <ul>
  <li v-for="list in consumer_history " ><p class="bg-primary ">consumed <span class="badge badge-secondary">{{list.val}}</span></p></li>
                </ul>
              </div>
                 </div>
              </div>
            </div>
        
    </div>
  </div>
</div>
 </div>


<div class="footer">
  <div class="container">
    <h3 class="display-1">
     Visual Buffer 
      </h3>
 <div class="progress align-self-end ">
 <div v-for="items in buffer" class="progress-bar bg-success progress-bar-striped" role="progressbar" style=" width:10%" :aria-valuenow="percent" aria-valuemin="0" aria-valuemax="100">{{items}}</div>
</div>
</div>
  </div>

</div>
  </div>
</template>

<script>
import {progressbar,alert} from 'vue-strap';


export default {
  name: 'app',
  data () {
    return {
     producer:0,
     consumer:0,
     buffer:[],
     clicked:false,
     randomNumber:null,
     loading:false,
     producer_history:[],
     consumer_history:[],
     show:false
    }
  },
  components:{
    progressbar,alert
  },watch:{
    randomNumber:function(newValue,oldValue){

console.log(newValue+" "+oldValue);

    }
  },
  methods:{
     random:function(){
     return Math.floor(Math.random() * Math.floor(10));
    },
    add(val){
      if(this.buffer.includes(val))
      return false;
      this.buffer.unshift(val);
      return true;
    },
    remove(){
     return this.buffer.shift();
    },
    consume(){
      if(this.isEmpty)
      {
this.status("Buffer Empty cannot Perform Operation : remove");
      }
      else{
      let removed=  this.remove();
        this.consumer++;
        this.consumer_history.unshift({val:removed});
      }
    },
    status:function(val){
      this.show=true;
      this.status=val;
    },
    produce(){
      this.clicked=true;
     this.loading=true;
      setTimeout( ()=>{
          this.loading=false;
  
        let random=this.random();
         if(this.isFull)
        {
         this.status(" Buffer already full , you can't perform operation : produce !");
        }
       else if(!this.add(random))
       {
      console.log("duplicate found ");
      this.status("Duplicate found produce again");
      
       }else{
         this.producer++;
       this.producer_history.unshift({value:random});
     this.randomNumber=random;
       }
      },1000);

    }
  },
  computed:{
   time:function(){
   return new Date().getSeconds();
   },
   percent:function(){
return (this.buffer.length/10)*100;
   },
    total:function(){
      return this.producer+this.consumer;
    },
    isFull:function(){
     return this.buffer.length===10;
    },
     isEmpty:function(){
     return this.buffer.length===0;
    }
  }
}
</script>

<style lang="scss">
.history-list{
  width:100%;
  height:29vh;
  border:1px 2px;
  margin:auto;
  padding:1px;

  ul{
     list-style-type: none;
  list-style-image: none;
height:inherit;
overflow: scroll;
li{
  margin-top:2px;
}
li:first-child{
margin-top:10px;
}
  }
 
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.v-divider{
  margin-left:1px;
  height:100%;
  border-left:1px solid grey;
}
.h-divider{
  margin-top:5px;
  margin-left:5px;
  width:100%;
  border-top:1px solid grey;
}
</style>
