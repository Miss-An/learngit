<template>
  <div class="treeTable">
    <table>
      <tr>
        <th>设备类型</th>
        <th>产品名称</th>
        <th>版本</th>
        <th>检查项</th>
        <th>检查子项</th>
        <th>检查大类</th>
        <th>设备小类</th>
        <th>备注</th>
      </tr>
      <tbody>
        <tr v-for="(item,index) in datas" :key="index" v-show="item.display">
          <td :style="{paddingLeft:item.left}"><span  @click="nodeClick(index)" v-if="item.branch" :class="item.expand? 'expand':'collapse'"></span>{{item.type}}</td>
          <td>{{item.name}}</td>
          <td>{{item.version}}</td>
          <td>{{item.checkItem}}</td>
          <td>{{item.checkSubItem}}</td>
          <td v-if="item.branch">{{item.BigItem}}</td>
          <td v-else><input type="text"  v-model="item.BigItem"></td>
          <td v-if="item.branch">{{item.smallItem}}</td>
          <td v-else><input type="text"  v-model="item.smallItem"></td>
          <td v-if="item.branch">{{item.remark}}</td>
          <td v-else><input type="text"  v-model="item.remark"></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
/* eslint-disable */ 
export default {
  name: 'treeTable',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      datas:[
          {left:'0',branch:true,expand:true,display:true,id:'1',pid:'0',type:'防火墙',name:'',version:'',checkItem:'',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'0.5rem',branch:true,expand:true,display:true,id:'1_1',pid:'1',type:'防火墙',name:'CE001',version:'',checkItem:'',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'1rem',branch:true,expand:true,display:true,id:'1_1_1',pid:'1_1',type:'防火墙',name:'CE001',version:'VR001',checkItem:'',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'1.5rem',branch:true,expand:true,display:true,id:'1_1_1_1',pid:'1_1_1',type:'防火墙',name:'CE001',version:'VR001',checkItem:'检查项A',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'3rem',branch:false,expand:true,display:true,id:'1_1_1_1_1',pid:'1_1_1_1',type:'防火墙',name:'CE001',version:'VR001',checkItem:'检查项A',checkSubItem:'检查子项A',BigItem:'软件版本',smallItem:'检查项A',remark:'备注信息'},
          {left:'0',branch:true,expand:true,display:true,id:'2',pid:'0',type:'数据交换中心',name:'',version:'',checkItem:'',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'0.5rem',branch:true,expand:true,display:true,id:'2_1',pid:'2',type:'数据交换中心',name:'CE001',version:'',checkItem:'',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'1rem',branch:true,expand:true,display:true,id:'2_1_1',pid:'2_1',type:'数据交换中心',name:'CE001',version:'VR001',checkItem:'',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'1.5rem',branch:true,expand:true,display:true,id:'2_1_1_1',pid:'2_1_1',type:'数据交换中心',name:'CE001',version:'VR001',checkItem:'检查项A',checkSubItem:'',BigItem:'',smallItem:'',remark:''},
          {left:'3rem',branch:false,expand:true,display:true,id:'2_1_1_1_1',pid:'2_1_1_1',type:'数据交换中心',name:'CE001',version:'VR001',checkItem:'检查项A',checkSubItem:'检查子项A',BigItem:'软件版本',smallItem:'检查项A',remark:'备注信息'},
        ],
    }
  },
  methods:{
    nodeClick(index){
      this.datas[index].expand = this.datas[index].expand ? false : true
      let pid =  this.datas[index].id 
      if(this.datas[index].expand){
        for(let i = index +1;i<this.datas.length;i++){
          let reg = new RegExp('^'+pid)
          if(this.datas[i].pid == pid){
            this.datas[i].display = true
            this.datas[i].expand = false 
          }else if(reg.test(this.datas[i].id)){
            this.datas[i].display = false
            this.datas[i].expand = false
          }else{
            break
          }
        }
      }else{
        for(let i = index +1;i<this.datas.length;i++){
          let reg = new RegExp('^'+pid)
          if(reg.test(this.datas[i].id)){
            this.datas[i].display = false
            this.datas[i].expand = false 
          }else{
            break
          }
        }
      }
      // for(let i = index +1;i<this.datas.length;i++){
      //   let reg = new RegExp('^'+pid)
      //   if(reg.test(this.datas[i].id)){
      //     if(this.datas[index].expand){
      //       this.datas[i].display = true
      //     }else{
      //       this.datas[i].display = false
      //       this.datas[i].expand = false 
      //     }
      //   }
      // }
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
th,td{
  width: 150px;
}
td:first-child{
  text-align: left;
}
td span{
  display: inline-block;
  width: 1.5rem;
  height: 1rem;
}
td span.expand{
  background-image: url('./folder_open.png');
}
td span.collapse{
  background-image: url('./folder.png');
}
</style>
