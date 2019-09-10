<template>
  <div class="box"> 
    <div>
      <el-button @click='add'>
        保存
      </el-button>
      <el-button @click="huifu">
        回复
      </el-button>
    </div>
     <canvas id="mycanvas"></canvas>
     <div class="tabbox">
              <el-tabs v-model="activeName"  >
              <el-tab-pane label="用户管理" name="first">
               <div @click="changecanvas">
                 换主题1
               </div>
                <div @click="changecanvas">
                    换主题2
                </div>
                <div @click="changecanvas">
                 换主题3
                </div>
                </el-tab-pane>
              <el-tab-pane label="配置管理" name="second">
                 <div @click="changecanvas">
                    换背景
                </div>
                <div @click="changecanvas">
                 换背景
                </div>
              </el-tab-pane>
              <el-tab-pane label="角色管理" name="third"><div @click="changecanvas">
                 换人物
                </div>
                </el-tab-pane>
              <el-tab-pane label="定时任务补偿" name="fourth">定时任务补偿</el-tab-pane>
            </el-tabs>
      </div>
  </div>
  
</template>

<script>
import {fabric} from "fabric"
const img1=require('./assets/timg.jpg')
const img2=require('./assets/timg2.jpg')
const head=require("./assets/head2.jpg")
const body=require("./assets/body1.jpg")
export default {
  name: 'App',
  data(){
         return {
           activeName:"first",
           canvas:null,
           bgimgurl:[img1
           ],
           json:""
         }
  },
  mounted(){
    console.log(fabric)
   this.canvas=new fabric.Canvas("mycanvas",{
     backgroundImage:img1,
     width:645,
     height:400
   })
  },
  methods:{
    changecanvas(){
         if(this.activeName=="second"){
           console.log("gg")
           this.canvas.setBackgroundImage(img2)
           this.canvas.renderAll()
         }else if(this.activeName=="third"){
             console.log("jj")
           this.initbody()
         }else if(this.activeName=="first"){
           this.changezhuti()
         }
    },
    initbody(){
      let _this=this
      fabric.Image.fromURL(head,function(img1){
             fabric.Image.fromURL(body,function(img){
            _this.canvas.add(new fabric.Group([img1,img],{width:100,height:100}))
            //  _this.canvas.renderAll()
      })
      })
    },
    add(){
       this.json=this.canvas.toJSON()
    },
    huifu(){
        this.canvas.loadFromJSON(this.json)
    },
    changezhuti(){
      let _this=this
        fabric.Image.fromURL(head,function(img1){
           img1.set('width',50).set('height',50)
            _this.canvas.add(img1)
            //  _this.canvas.renderAll()
      })
    }
  }
}
</script>

<style>
.box{
  width: 635px;
  height:828px;
  background: #fff;

}
#mycanvas{
  height:400px;
  width: 100%;

}
.tabbox{
  height: 400px;
  width: 100%;

}
</style>
