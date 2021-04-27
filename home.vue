<template>
 <div  >
    <b-navbar toggleable="sm" type="light" variant="light"  class="navbar">
      

        <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item >
            <b-icon icon="list" variant="dark"></b-icon>Saved List</b-nav-item>
          <b-nav-item>
            <b-icon icon="funnel" variant="dark"></b-icon>Saved Filters
            </b-nav-item>
          <b-nav-item >
            <b-icon icon="clock-history" variant="dark" v-model="query" ></b-icon>Serach History</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <!-- <b-form-input size="sm" class="mr-sm-2" placeholder="Search" v-model="search"></b-form-input> -->
            
            <b-form-input
             type="text"
             name=""
             
              placeholder="Search...."
              
               v-model="filter"
            ></b-form-input>
            <!-- id="myinput" -->
       <!-- v-on:keyup="searchfun()" -->
          </b-nav-form>
          
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
<div class="content">
    <div class="col">
      <div>
        <div>
      <table class="table ">
        <thead>
        <tr >
          <th scope="col" >Date</th>
          <th scope="col">List Name</th >
         <th scope="col">  No Of Entities</th >
          <th scope="col" >Actions</th >
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in items" :key="item.id" allign="center">
        <!-- <tr v-for="(row, index) in filteredRows" :key="`ListName-${index}`">  -->
            <td md10>{{ item.Date }}</td>
            <td >{{ item.ListName }}</td>
            <td >{{ item.NoOfEntities }}</td>
            <td>
            <b-icon icon="envelope-open" variant="dark" style='margin-right:16px'></b-icon>
            <b-icon icon="share" variant="dark" style='margin-right:16px'></b-icon>
            <b-icon icon="pen" variant="dark" style='margin-right:16px'></b-icon>
            <b-icon icon="trash" variant="dark" style='margin-right:16px'></b-icon>
            
           </td>
           <td>
           <b-button class="my-2 my-sm-0" @click="showdetails(item.id)" >Details</b-button> 
            </td> 
            
          </tr>
         </tbody>
      </table>
      </div>
      </div>
    </div>
    <div class="col">
      <h4 class="heading"> Details</h4>
      <table class="table">
        <tr v-for="detail in dtl" :key="detail.id">
          <td>{{ detail}}</td>
        </tr>
      </table>

    </div>
  </div>
</div>

</template>

<script>
// import data from './plugins/data';
import RawData from "D:/vue practice/tableassign/src/RawData.json"
export default{
  

  name : "home",
  dtl:RawData,
  data() {
    return {
      //   // Note `isActive` is left out and will not appear in the rendered table
      
      query:'',
      originalrows:[], 
       fields: ['Date', 'ListName', 'NoOfEntities','Actions'],
        items: [
           {  Date: '02/02/2020', ListName: 'Book', NoOfEntities: '2' },
           {  Date: '01/02/2020', ListName: 'Pen', NoOfEntities: '2' },
            {  Date:'03/02/2020', ListName: 'Eraser', NoOfEntities: '2' },
            { Date: '01/04/2020', ListName: 'Ink', NoOfEntities: '2' }
         ]
        // data:data
    }

   
  },
  beforeMount(){
    this.originalrows=this.items;
  },
  methods:{
    search(){
      var result=[];
      var searchData=this.originalrows;
      if(this.query==""){
        this.items=this.originalrows;
      }
      else{
        for(var i=0;i< searchdata.length;i++){
          var sparam =this.query.toLowerCase();
          for(var key in searchData[i]){
            if(searchData[i].hasOwnProperty(key)){
              var value=searchData[i][key];
              if(typeof value =="string" && value.toLowerCase().indexOf(sparam) >= 0){
                result.push(searchData[i]);
              }
            }
          }
        }
        this.items=result;
      }
    },
   showdetails(){
      var id=item.id;
      return dtl.detail[id];
    


   }
  }
 

  }
   

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .content{
            display: flex;
            flex-wrap: wrap;
        }

  .content > *:nth-child(1)
        {
            flex: 1 1 70%;
            
            border-style : outset;
            
        }
        .content > *:nth-child(2)
        {
            flex: 1 1 30%;
        } 

        .heading{
          background:hsl(180, 30%, 92%);
          text-align: center;
        }

</style>
