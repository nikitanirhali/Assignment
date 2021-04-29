<template>
 <div  >
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" ><b-icon icon="list" variant="dark"></b-icon>Saved List<span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" ><b-icon icon="funnel" variant="dark"></b-icon>Saved Filters</a>
      </li>
      <li class="nav-item ">
        <a class="nav-link ">
          <b-icon icon="clock-history" variant="dark" v-model="query" ></b-icon>Serach History
        </a>
        
      </li>
     
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="text" placeholder="Search"  id="myInput" v-on:keyup="myFunction()"  title="Type in a name">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
<div class="content">
    <div class="col">
      
    <div>
      <table class="table " id="myTable">
        <thead>
        <tr  class="header">
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
           <b-button class="my-2 my-sm-0" @click="showdetails(item.details)" >Details</b-button> 
           
            </td> 
            
          </tr>
         </tbody>
      </table>
      </div>
      
    </div>
    <div class="col">
      <h4 class="heading"> Details</h4>
      <table class="table">
        <tr v-for="a in arr" :key="a.id">
          <td>{{a}}</td>
        </tr>
      </table>

    </div>
  </div>
</div>

</template>

<script>
// import data from './plugins/data';
// import RawData from "D:/vue practice/tableassign/src/RawData.json"
export default{
  

  name : "home",
  
  data() {
    return {
      //   // Note `isActive` is left out and will not appear in the rendered table
      // dtl:RawData,
      search:'',
      filter:"", table:"", tr:"", td:"", i:"", txtValue:"",
      arr:[],
       fields: ['Date', 'ListName', 'NoOfEntities','Actions'],
        items: [
           {  Date: '02/02/2020', ListName: 'Book', NoOfEntities: '2',details:["Name:Nikita ","Age:23"] },
           {  Date: '01/02/2020', ListName: 'Pen', NoOfEntities: '2',details:["Name:Nikhil ","Age:23"] },
            {  Date:'03/02/2020', ListName: 'Eraser', NoOfEntities: '2',details:["Name:Mousam ","Age:23"] },
            { Date: '01/04/2020', ListName: 'Ink', NoOfEntities: '2',details:["Name:Prathamesh ","Age:23"] }
         ]
        // data:data
    }

   
  },
methods:{
 myFunction() {
  // Declare variables
 
  this.input = document.getElementById("myInput").value;
  this.filter = document.getElementById("myInput").value.toUpperCase();
  this.table = document.getElementById("myTable");
  this.tr = table.getElementsByTagName("tr");

  // Loop through all table rows, and hide those who don't match the search query
  for (i = 0; i < this.tr.length; i++) {
    this.td = this.tr[i].getElementsByTagName("td")[1];
    if (this.td) {
      this.txtValue = this.td.textContent || this.td.innerText;
      if (this.txtValue.toUpperCase().indexOf(this.filter) == -1) {
        this.tr[i].style.display = "none";
        
      } else {
        this.tr[i].style.display = "";
       
      }
    }
  }

},
        
showdetails(arr){
  this.arr=arr;

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
