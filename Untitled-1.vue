<template>
    <div class="warp">
        <div v-for="(item,index) of attachMentList" :key="index" class="relative pointer">
                <p  @mouseenter="enter(index,item.level)" @mouseleave="leave(index,item.level)" >
                    <span  @click="hand(index,item.level)">
                        <img :src="`../../../assets/images/attachment/${item.boultSrc}.png`" class="jiantou" v-if="item.sign == 'folder' || item.sign ==  'doc'"/>
                        <img :src="`../../../assets/images/attachment/${item.sign}.png`" class="icon"/>
                        <span>{{item.name}}</span>                        
                    </span>
                    <span class="right" v-show="item.iconShow" >
                        <img src="../../../assets/images/attachment/update.png" v-if="item.sign == 'folder' || item.sign ==  'doc'"/>
                        <span  v-if="item.sign == 'ppt' || item.sign ==  'pdf' || item.sign ==  'word' || item.sign ==  'excel'"  @click="haveMenuHand(index,item.level,item.address)">
                            <span>预览</span>/<span>下载</span>
                            <span  v-clickoutside = "handleClickOutSide(index,item.level,item.address)">
                                <span @click="handShowMenu(index,item.level,item.address)" class="expand">
                                    <img src="../../../assets/images/attachment/nlist.png" class="meun"/>
                                </span>
                                <div v-if="!item.children" v-show="item.menuShow" class="downmenu">
                                    <div class="mb">
                                    <RadioGroup vertical class="ti">
                                        <Radio label="manager">
                                            <span>仅管理员可见</span>
                                        </Radio>
                                        <Radio label="member">
                                            <span>所有组员可见</span>
                                        </Radio>
                                    </RadioGroup>                 
                                    </div>
                                    <div class="line"></div> 
                                    <p class="mb mt">
                                        <img src="../../../assets/images/attachment/move.png"  class="ti rel"/>
                                        <span>移动</span>  
                                    </p>
                                    <div class="line"></div>  
                                    <p class="mb mt">
                                        <img src="../../../assets/images/attachment/delete.png"  class="ti rel"/>
                                        <span>删除</span>
                                    </p>
                                </div>                                 
                            </span>

                            
                        </span>
                    </span>                    
                </p>



                <div v-if="item.children" v-show="item.isShow" v-for="(c_item,index) of item.children" :key="index"  class="relative  pointer">
                        <p  @mouseenter="enter(index,c_item.level,c_item.address)" @mouseleave="leave(index,c_item.level,c_item.address)" style="padding-left: 20px;">
                            <span  @click="hand(index,c_item.level,c_item.address)">
                                <img :src="`../../../assets/images/attachment/${c_item.boultSrc}.png`" class="jiantou" v-if="c_item.sign == 'folder' || c_item.sign ==  'doc'"/>
                                <img :src="`../../../assets/images/attachment/${c_item.sign}.png`"  class="icon"/> 
                                <span>{{c_item.name}}</span>                                
                            </span>
                            <span class="right" v-show="c_item.iconShow">
                                <img src="../../../assets/images/attachment/update.png" v-if="c_item.sign == 'folder' || c_item.sign ==  'doc'"/>
                                <span  v-if="c_item.sign == 'ppt' || c_item.sign ==  'pdf' || c_item.sign ==  'word' || c_item.sign ==  'excel'" @click="haveMenuHand(index,c_item.level,c_item.address)">
                                    <span>预览</span>/<span>下载</span>
                                    <span @click="handShowMenu(index,c_item.level,c_item.address)" class="expand">
                                        <img src="../../../assets/images/attachment/nlist.png" class="meun" />
                                    </span>                                  
                                    <div v-if="!c_item.children" v-show="c_item.menuShow" class="downmenu">
                                        <div class="mb">
                                        <RadioGroup vertical class="ti">
                                            <Radio label="manager">
                                                <span>仅管理员可见</span>
                                            </Radio>
                                            <Radio label="member">
                                                <span>所有组员可见</span>
                                            </Radio>
                                        </RadioGroup>                  
                                        </div>
                                        <div class="line"></div> 
                                        <p class="mb mt">
                                            <img src="../../../assets/images/attachment/move.png"  class="ti rel"/>
                                            <span>移动</span>  
                                        </p>
                                        <div class="line"></div>  
                                        <p class="mb mt">
                                            <img src="../../../assets/images/attachment/delete.png"  class="ti rel"/>
                                            <span>删除</span>
                                        </p>
                                    </div>
                                    
                                </span>
                            </span>
                        </p>



                        <div v-if="c_item.children" v-show="c_item.isShow" v-for="(cc_item,index) of c_item.children" :key="index"  class="relative pointer">
                            <p  @mouseenter="enter(index,cc_item.level,cc_item.address)" @mouseleave="leave(index,cc_item.level,cc_item.address)"  style="padding-left: 40px;">
                                <span>
                                    <img :src="`../../../assets/images/attachment/${cc_item.boultSrc}.png`" class="jiantou" v-if="cc_item.sign == 'folder' || cc_item.sign ==  'doc'"/>
                                    <img :src="`../../../assets/images/attachment/${cc_item.sign}.png`"  class="icon"/> 
                                    <span>{{cc_item.name}}</span>                                    
                                </span>
                                <span class="right"  v-show="cc_item.iconShow">
                                    <img src="../../../assets/images/attachment/update.png" v-if="cc_item.sign == 'folder' || cc_item.sign ==  'doc'"/>
                                    <span  v-if="cc_item.sign == 'ppt' || cc_item.sign ==  'pdf' || cc_item.sign ==  'word' || cc_item.sign ==  'excel'"  @click="haveMenuHand(index,cc_item.level,cc_item.address)">
                                        <span>预览</span>/<span>下载</span>
                                        <span @click="handShowMenu(index,cc_item.level,cc_item.address)" class="expand">
                                            <img src="../../../assets/images/attachment/nlist.png" class="meun"/>
                                        </span>                                
                                        <div v-if="!cc_item.children" v-show="cc_item.menuShow" class="downmenu">
                                            <div class="mb">
                                            <RadioGroup vertical class="ti">
                                                <Radio label="manager">
                                                    <span>仅管理员可见</span>
                                                </Radio>
                                                <Radio label="member">
                                                    <span>所有组员可见</span>
                                                </Radio>
                                            </RadioGroup>                  
                                            </div>
                                            <div class="line"></div> 
                                            <p class="mb mt">
                                                <img src="../../../assets/images/attachment/move.png"  class="ti rel"/>
                                                <span>移动</span>  
                                            </p>
                                            <div class="line"></div>  
                                            <p class="mb mt">
                                                <img src="../../../assets/images/attachment/delete.png"  class="ti rel"/>
                                                <span>删除</span>
                                            </p>
                                        </div>
                                        
                                    </span>
                                </span>                                
                            </p>

                            
                        </div>
                </div>
        </div>
    </div>
</template>
<script>
import clickoutside from '../../app/directives/clickoutside-2.js'
export default{
        directives:{
            clickoutside
        },
        methods: {
            handleClickOutSide(index,level,address){
                this.attachMentList.forEach((val) => {
                        val.iconShow = false;
                        val.menuShow = false;
                    if(val.children){
                        val.children.forEach((c_val) => {
                                c_val.iconShow = false;
                                c_val.menuShow = false;
                            if(c_val.children){
                                c_val.children.forEach((cc_val) => {
                                        cc_val.iconShow = false;
                                })                                    
                            }
                            })                        
                    }
                }) 
            },
            enter(index,level,address){
                if( level == 1 ){
                    this.leave();
                    this.attachMentList[index].iconShow = true;
                }else if( level == 2 ){
                    this.leave();
                    let fatherNum = Number(address.substr(0,1));
                    this.attachMentList[fatherNum].children[index].iconShow = true;
                }else if( level == 3 ){
                    this.leave();
                    let grandFatherNum = Number(address.substr(0,1));
                    let fatherNum = Number(address.substr(1,1));
                    this.attachMentList[grandFatherNum].children[fatherNum].children[index].iconShow = true;
                }
            },
            leave(index,level,address,ev){
                var ev = ev || window.event;
                if( level == 1 ){
                    if( this.attachMentList[index].haveMenu ){
                      ev.target.style.backgroundColor = '#eeeeee';
                    }else{
                        this.hideAll();
                    }
                }else if( level == 2 ){
                    let fatherNum = Number(address.substr(0,1)); 
                    if(  this.attachMentList[fatherNum].children[index].haveMenu ){
                      ev.target.style.backgroundColor = '#eeeeee';
                    }else{
                        this.hideAll();
                    }                                    
                }else if( level == 3 ){
                    let grandFatherNum = Number(address.substr(0,1));
                    let fatherNum = Number(address.substr(1,1));
                    if(  this.attachMentList[grandFatherNum].children[fatherNum].children[index].haveMenu ){
                      ev.target.style.backgroundColor = '#eeeeee';
                    }else{
                        this.hideAll();
                    } 
                }
           
            },
            hideAll(){                //关闭全部标签菜单
                this.attachMentList.forEach((val) => {
                    if( !val.haveMenu ){
                        val.iconShow = false;
                        val.menuShow = false;
                    }
                    if(val.children){
                        val.children.forEach((c_val) => {
                            if( !c_val.haveMenu ){
                                c_val.iconShow = false;
                                c_val.menuShow = false;
                            }
                            if(c_val.children){
                                c_val.children.forEach((cc_val) => {
                                    if( !cc_val.haveMenu ){
                                        cc_val.iconShow = false;
                                        cc_val.menuShow = false;
                                    }
                                })                                    
                            }
                            })                        
                    }
                })                     
            },
            // hideMenu(){            //整个父级点击时所有下拉菜单隐藏
            //         this.attachMentList.forEach((val) => {
            //             val.menuShow = false;
            //             if(val.children){
            //                 val.children.forEach((c_val) => {
            //                     c_val.menuShow = false;
            //                     if(c_val.children){
            //                         c_val.children.forEach((cc_val) => {
            //                             cc_val.menuShow = false;
            //                         })                                    
            //                     }
            //                  })                        
            //             }
            //         })                   
            // },
            hand(index,level,address){     //点击切换黑三角的开、关 状态
                if( level == 1 ){
                    this.attachMentList[index].isShow = !this.attachMentList[index].isShow;
                    this.attachMentList[index].boultSrc = this.attachMentList[index].isShow?'open':'close';
                    if(this.attachMentList[index].children){
                        this.attachMentList[index].children.forEach((val) => {
                            val.isShow = false;
                            val.boultSrc = 'close';
                        });
                    }
                }else if(level == 2){
                    let fatherNum = Number(address.substr(0,1));
                    this.attachMentList[fatherNum].children[index].isShow = !this.attachMentList[fatherNum].children[index].isShow;
                    this.attachMentList[fatherNum].children[index].boultSrc = this.attachMentList[fatherNum].children[index].isShow?'open':'close';
                }
            },
            handShowMenu(index,level,address){      //点击显示下拉菜单
                if( level == 1 ){
                    this.attachMentList[index].menuShow = true;
                }else if( level == 2 ){
                    let fatherNum = Number(address.substr(0,1));
                    this.attachMentList[fatherNum].children[index].menuShow = true;                
                }else if( level == 3 ){
                    let grandFatherNum = Number(address.substr(0,1));
                    let fatherNum = Number(address.substr(1,1));
                    this.attachMentList[grandFatherNum].children[fatherNum].children[index].menuShow = true;
                }
            },
            haveMenuHand(index,level,address){      //点击右边的功能键（预览、下载、菜单），改变父级状态
                if( level == 1 ){
                    this.attachMentList[index].haveMenu = true;
                }else if( level == 2 ){
                    let fatherNum = Number(address.substr(0,1));
                    this.attachMentList[fatherNum].children[index].haveMenu = true;              
                }else if( level == 3 ){
                    let grandFatherNum = Number(address.substr(0,1));
                    let fatherNum = Number(address.substr(1,1));
                    this.attachMentList[grandFatherNum].children[fatherNum].children[index].haveMenu = true;
                }
            }
        },
        data(){
            return{
                attachMentList: [
                    {
                        name: '车工坊',
                        sign: 'folder',
                        level: 1,                 //层级
                        haveMenu: false,          //判断菜单是否显示。若没显示，则移出全部关闭；若显示，则移出不做动作
                        iconShow: false,          //右边图标移入移出控制  
                        isShow: false,            //控制子类的显隐
                        boultSrc: 'close',           //三角箭头的src  
                        children: [
                            {
                                name: '交互演示.ppt',
                                sign: 'ppt',
                                level: 2,
                                address: '00',
                                haveMenu: false,
                                iconShow: false,
                                menuShow: false
                            },
                            {
                                name: '交互演示.ppt',
                                sign: 'ppt',
                                 level: 2,
                                address: '01',
                                haveMenu: false,
                                iconShow: false,
                                menuShow: false
                            }
                        ]
                    },
                    {
                        name: 'OKR',
                        sign: 'folder',
                        level: 1,
                        haveMenu: false,
                        iconShow: false,
                        isShow: false,
                        boultSrc: 'close',
                        children: [
                            {
                                name: '车工坊会议纪要',
                                sign: 'doc',
                                level: 2,
                                address: '10',
                                haveMenu: false,
                                iconShow: false,
                                isShow: false,
                                boultSrc: 'close',
                                children: [
                                    {
                                        name: '车工坊会议纪要.pdf',
                                        sign: 'pdf',
                                        level: 3,
                                        address: '100',
                                        haveMenu: false,
                                        iconShow: false ,
                                        menuShow: false
                                    }
                                ]
                            },
                            {
                                name: '车工坊理论.pdf',
                                sign: 'pdf',
                                level: 2,
                                address: '11',
                                haveMenu: false,
                                iconShow: false,
                                menuShow: false                               
                            }
                        ]
                    },
                    {
                        name: '交互文件.doc',
                        sign: 'word',
                        level: 1,
                        haveMenu: false,
                        iconShow: false,
                        menuShow: false
                    },
                    {
                        name: '交互文件.xle',
                        sign: 'excel',
                        level: 1,
                        haveMenu: false,
                        iconShow: false,
                        menuShow: false
                    }
                ]
            }
        }
}
</script>
<style lang="less" scoped>
*{
    padding: 0px;
    margin: 0px;
}
.warp{
    padding: 0px 0px 0px 24px;
    margin-top: -16px;
    font-family:PingFangSC-Medium;
    color: #444444;
    user-select: none;
}
.right{
    position: absolute;
    top: 3px;
    right: 30px;
    font-size:12px;
    color:#AAAAAA;
}
.pointer{
    cursor: pointer;
    margin-top: 16px;
}
.warp div p{
    padding: 1px;
}
.warp div p:hover{
    background-color: #eeeeee;
}
.jiantou{
    margin-right: 6px;
    margin-bottom: 1px;
}
.icon{
   position: relative;
   top: 3px;
   left: 0px;
}
.meun{
   position: relative;
   top: 3px;
   left: 4px;
   margin-right: 4px;
}
.downmenu{
    background:#fffffa;
    box-shadow:0 2px 6px 0 rgba(0,0,0,0.15);
    border-radius:2px;
    padding-top: 6px;
    padding-bottom: 2px;
    width:132px;
    position: absolute;
    top: 20px;
    right: 0px;
    z-index: 100;
    // height:142px;
}
.ti{
    padding-left: 10px;
}
.mb{
    margin-bottom: 8px;
}
.mt{
    margin-top: 8px;
}
.rel{
    position: relative;
    top: 3px; 
    left: 0px;
}
.bob{
    border-bottom: 1px solid #1B98C7;
    padding-bottom: 10px;
}
.line{
    width: 102px;
    height: 1px;
    background-color: #1B98C7;
    margin-left: 14px;
}
.expand{         //扩大下拉框点击范围
    display: inline-block; 
    width: 14px;
}



/**
* 利用深度选择器来修改引入单选框的样式      /deep/
*/
.downmenu{
    /deep/ .ivu-radio-checked .ivu-radio-inner {
         border-color: #1B98C7;  
    }
    /deep/ .ivu-radio-inner:after {
        position: absolute;
        width: 4px;
        height: 8px;
        left: 4px;
        top: 1px;
        border-radius: 0px;
        display: table;
        border-top: 1px solid #1B98C7; 
        border-left: 1px solid #1B98C7; 
        border-bottom: 0px solid #1B98C7; 
        border-right: 0px solid #1B98C7; 
        content: " ";
        background-color: transparent;
        opacity: 0;
        transition: all .2s ease-in-out;
        -webkit-transform: scale(0) rotate(-135deg);
        transform: scale(0) rotate(-135deg);
    }
    /deep/ .ivu-radio-checked .ivu-radio-inner:after {
        opacity: 1;
        transform: scale(1) rotate(-135deg);
        transition: all 0.2s ease-in-out;
    }
    /deep/ .ivu-radio-wrapper {
        font-size: 12px;
        vertical-align: middle;
        display: inline-block;
        position: relative;
        white-space: nowrap;
        margin-right: 8px;
        cursor: pointer;
    }
    /deep/ .ivu-radio-wrapper-checked{
        color: #1B98C7;
    }
}
</style>
