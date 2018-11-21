<template>
  <div class="content">
    <div class="flow" v-if="nid==22"><img src="../assets/img/jinj_pic_qysh_a.png" alt="" class=""></div>
    <div class="flow_micro" v-if="nid==11"><img src="../assets/img/jinj_pic_xwsh_a.png" alt="" class=""></div>
    <div class="image_list">
      <!--企业商户nid==22    小微商户nid==11       收款宝智能pos传统pos tid=1/2/3    收钱宝盒，超级收款宝 tid==4/5-->
        <!--营业执照、-->
        <div class="default_img p_r pic0"  v-if="nid==22">
          <!--<div  @click='getImg("0")' class="boximg">-->
            <!--<img :src="iptInfo.imgsrc0" alt="" id="imgSrc0">-->
          <!--</div>-->
         <!--<div class="box"  v-show="iptInfo.imgsrc0"> &lt;!&ndash;&ndash;&gt;-->
            <!--<i class="delect" @click="delImg('0')"></i>-->
            <!--<i class="look_big" @click="look('0')"></i>-->
          <!--</div>-->
          <img :src="iptInfo.imgsrc0" alt="" id="imgSrc0">
          <input type="file" name="image"  capture="camera"  accept="image/*" @change='getImg($event,"0")'   v-show="!iptInfo.imgsrc0">
        </div>
      <!--身份证人像面-->
      <div class="default_img p_r pic1">
        <!--<div  @click='getImg("1")' class="boximg">-->
          <!--<img :src="iptInfo.imgsrc1" alt="" id="imgSrc1">-->
        <!--</div>-->
        <!--<div class="box"  v-show="iptInfo.imgsrc1">-->
          <!--<i class="delect" @click="delImg('1')"></i>-->
          <!--<i class="look_big" @click="look('1')"></i>-->
        <!--</div>-->
        <img :src="iptInfo.imgsrc1" alt="" id="imgSrc1">
        <input type="file" name="image"  capture="camera"  accept="image/*" @change='getImg($event,"1")'   >
      </div>
      <!--身份证国徽面、-->
      <div class="default_img p_r pic2" >
        <!--<div  @click='getImg("2")' class="boximg">-->
          <!--<img :src="iptInfo.imgsrc2" alt="" id="imgSrc2">-->
        <!--</div>-->
        <!--<div class="box"   v-show="iptInfo.imgsrc2">-->
          <!--<i class="delect" @click="delImg('2')"></i>-->
          <!--<i class="look_big" @click="look('2')"></i>-->
        <!--</div>-->
        <img :src="iptInfo.imgsrc2" alt="" id="imgSrc2">
        <input type="file" name="image"  capture="camera"  accept="image/*" @change='getImg($event,"2")'   >
      </div>
      <div v-if="nid==11">
        <!--借记卡、-->
        <div class="default_img p_r pic3" >
          <!--<div  @click='getImg("3")' class="boximg">-->
            <!--<img :src="iptInfo.imgsrc3"  id="imgSrc3"/>-->
          <!--</div>-->
          <!--<div class="box"  v-show="iptInfo.imgsrc3">-->
            <!--<i class="delect" @click="delImg('3')"></i>-->
            <!--<i class="look_big" @click="look('3')"></i>-->
          <!--</div>-->
          <img :src="iptInfo.imgsrc3"  id="imgSrc3"/>
          <input type="file" name="image"  capture="camera"  accept="image/*" @change='getImg($event,"3")'   >
        </div>
      </div>
      <!--只有超级收款宝，收钱宝盒才需要门面照片-->
      <div v-if="nid==11&&(tid==4||tid==11)">
        <!--门面照片、-->
        <div class="default_img p_r pic4" >
          <!--<div  @click='getImg("4")' class="boximg">-->
            <!--<img :src="iptInfo.imgsrc4"  id="imgSrc4"/>-->
          <!--</div>-->
          <!--<div class="box"  v-show="iptInfo.imgsrc4">-->
            <!--<i class="delect" @click="delImg('4')"></i>-->
            <!--<i class="look_big" @click="look('4')"></i>-->
          <!--</div>-->
          <img :src="iptInfo.imgsrc4"  id="imgSrc4"/>
          <input type="file" name="image"  capture="camera"  accept="image/*" @change='getImg($event,"4")'   >
        </div>
      </div>

    </div>
    <ul class="mbt160 f_list padding" v-if="nid==22">
      <li class="item bor_bt">
        <label> 法人姓名</label><input type="text" placeholder="请输入法人姓名" v-model="iptInfo.name" @keyup="getValue"></li>
      <li class="item bor_bt">
        <label>法人身份证号</label>
        <input type="text" placeholder="请输入身份证号" v-model="iptInfo.cardId" @keyup="getValue"/></li>
      <li class="item bor_bt">
        <span class="longtime"  @click="(iptInfo.endTime=iptInfo.endDate)">长期</span>
        <label>身份证有效期</label> <datetime confirm-text="确认"
             cancel-text="取消" v-model="iptInfo.endTime"  @on-change="change" :start-date="iptInfo.startDate" :end-date="iptInfo.endDate"  @keyup="getValue"></datetime>
      </li>
      <li class="item bor_bt">
        <label>营业执照号</label><input type="text" placeholder="请输入营业执照号" v-model="iptInfo.licenceId" @keyup="getValue"/></li>
      <li class="item bor_bt">
        <label>营业执照名称</label><input type="text" placeholder="请输入营业执照名称" v-model="iptInfo.licenceName" @keyup="getValue"/></li>
      <li class="item">
        <label>营业执照地址</label> <input type="text" placeholder="请输入营业执照地址" v-model="iptInfo.licenceAddress" @keyup="getValue"/></li>
    </ul>
    <ul class="mbt160 f_list padding" v-if="nid==11">
      <li class="item bor_bt">
        <label> 入账户名</label>
        <input type="text" placeholder="请输入入账户名" v-model="iptInfo.mName" @keyup="getValue"></li>
      <li class="item bor_bt">
        <label> 入款账号</label>
        <input type="text" placeholder="请输入入款账号" v-model="iptInfo.mcardNum" @keyup="getValue"></li>
      <li class="item bor_bt">
        <label>法人身份证号</label>
        <input type="text" placeholder="请输入身份证号" v-model="iptInfo.cardId" @keyup="getValue"/></li>
      <li class="item bor_bt">
        <span class="longtime" @click="(iptInfo.endTime=iptInfo.endDate)">长期</span>
        <label>身份证有效期</label>
        <datetime confirm-text="确认" cancel-text="取消" v-model="iptInfo.endTime"
                  @on-change="change" :start-date="iptInfo.startDate" :end-date="iptInfo.endDate" @keyup="getValue"></datetime>
      </li>
      <li class="item bor_bt" @click="show">
        <i class="more_slt"></i> <label>开户银行</label>
        <input type="text" placeholder="招商银行（总行）" v-model="iptInfo.mbank" @keyup="getValue" readonly/></li>

    </ul>
    <awesome-picker
      ref="picker"
      :data="picker.data"
      :anchor="picker.anchor"
      @cancel="handlePickerCancel"
      @confirm="handlePickerConfirm">
    </awesome-picker>
    <div :class="{'light': isB}" class="next_btn" @click="nextStep1">下一步</div>
    <!--查看大图-->
    <div class="bigImg" v-show="isEnlargeImage==true">
      <!--<img :src="base64Img" alt="">-->
      <img :src="base64Img" alt="">
    </div>
    <div class="mask" v-show="isEnlargeImage==true" @click="isEnlargeImage=false"></div>
  </div>
</template>
<script>
  import Vue from 'vue'
  // import lrz from 'lrz'
  import imageUploadMixins from '@/mixins/image-compress'
  import {ToastPlugin,DatetimePlugin,Datetime,Toast,Group } from 'vux'
  Vue.use(ToastPlugin,DatetimePlugin)
  export default {
    name: "inComing",
    mixins: [imageUploadMixins],
    components:{Group,Toast,Datetime,ToastPlugin,DatetimePlugin },
    data(){
      return{
        custid:'0',
        imgUrl:'',
        isEnlargeImage:false,
        iptInfo: this.$store.state.ipt_Info,
        // iptInfo:{name:'',endTime:'有效期',licenceId:'',licenceName:'',licenceAddress:'',  endDate:'2999-12-30', startDate:'',
        //   mbank:'',mcardNum:'',mName:'',imgsrc0:"" ,cardId:'',imgsrc1:'',imgsrc2:'',imgsrc3:'',imgsrc4:''},
        isB:false,
        tid:this.$route.params.tid,
        nid:this.$route.params.nid,
        picker:{
          anchor: [],
          data: [],
          swipeTime:1000,
        },
        base64Img:'',
        agentid:sessionStorage.getItem('agentid')
      }
    },
    created(){
      window.getImg=this.getImg;
      window.getPic=this.getPic;
      this.getInitData();//初始化数据
      this.getBank() // 小微商户选择银行
      // console.log( this.GetQueryString('agentid'))
      // 设置最小日期
      this.setDate()
    },
    // mounted() {
    //   localStorage.setItem("nid", this.$route.params.nid);
    //   setTimeout((params,type) => {
    //     this.getPic(params,type)
    //   }, 20)},
    methods: {
      getBank(){
        if(this.nid==11){
          this.$http.post(this.GLOBAL.host+'/enterprise/getBanklist')
            .then( (res)=> {
              var arr=new Array()
              var restxt=res.data.data;
              for(var i=0;i<restxt.length;i++){
                arr.push(restxt[i].bankName)
              }
              this.picker.data.push(arr)
            })
        }

      },
      setDate(){
        var d=new Date();
        var  month = '' + (d.getMonth() + 1);
        var day = '' + d.getDate();
        var  year = d.getFullYear();
        if (month.length < 2) month = '0' + month;
        if (day.length < 2) day = '0' + day;
        this.iptInfo.startDate=year+'-'+month+'-'+day;
      },
      getInitData(){
        // 企业进件初始化
        var step0={step:0, custid:this.custid,macType:this.tid, agentid:this.agentid};
        // console.log(this.agentid)
        if(this.nid==22){
          // console.log(this.GLOBAL.host)
          this.$http.post(this.GLOBAL.host+'/enterprise/addMerchantInfo', step0,{
            headers: {
              'Content-Type':'application/json;charset=utf-8'
            }
          })
            .then((res)=>{
              // console.log(res)
              if(res.data.code==0){
                this.custid=res.data.data.custid;
                sessionStorage.setItem('custid',res.data.data.custid)
              }else{
                this.$vux.toast.text('初始化失败', 'center');
              }
            })
        }else if(this.nid==11){
          // 小微商户进件初始化
          this.$http.post(this.GLOBAL.host+'/smallMicro/addMerchantInfo', step0)
            .then((res)=>{
              console.log(res)
              if(res.data.code==0){
                this.custid=res.data.data.custid;
                sessionStorage.setItem('custid',res.data.data.custid)
              }else{
                this.$vux.toast.text('初始化失败', 'center');
              }
            })
        }
      },
      delImg(type){
        if (type==0) {
          this.iptInfo.imgsrc0=null
        }else if (type==1) {
          this.iptInfo.imgsrc1=null
        }else  if (type==2) {
          this.iptInfo.imgsrc2=null
        }else if (type==3) {
          this.iptInfo.imgsrc3=null
        }else if (type==4) {
          this.iptInfo.imgsrc4=null
        }
      },
      look(type){
        this.isEnlargeImage=true;
        if (type==0) {
        this.base64Img = this.iptInfo.imgsrc0
        }else if (type==1) {
          this.base64Img =  this.iptInfo.imgsrc1
        }else  if (type==2) {
          this.base64Img = this.iptInfo.imgsrc2
        }else if (type==3) {
          this.base64Img = this.iptInfo.imgsrc3
        }else if (type==4) {
          this.base64Img = this.iptInfo.imgsrc4
        }
      },
      // getPic(params,type){
      //   if(type=='0'){
      //     this.iptInfo.imgsrc0=decodeURIComponent(params);
      //   }else if(type=='1') {
      //     this.iptInfo.imgsrc1=decodeURIComponent(params);
      //     // 身份证正面
      //     var data={"imagebase64":this.iptInfo.imgsrc1,"custId":this.custid,"fileName":"cardfrontpath"}
      //     this.$http.post(this.GLOBAL.host+'/tpisAuth/scanPhotoInfo',data,{
      //       headers: {
      //         'Content-Type':'application/json;charset=utf-8'
      //       }
      //     }).then(res=>{
      //       console.log(res.data.data);
      //       this.iptInfo.cardId=res.data.data.idCard.number;
      //       // this.iptInfo.imgsrc1=res.data.data.idCard.cardfrontpath;
      //       this.iptInfo.name=res.data.data.idCard.name;
      //       this.iptInfo.mName=res.data.data.idCard.name;
      //     },err =>{
      //       console.log(err)
      //     })
      //   }else if(type=='2'){
      //     // 身份证反面
      //     this.iptInfo.imgsrc2=decodeURIComponent(params);
      //     var data={"imagebase64":this.iptInfo.imgsrc2,"custId":this.custid,"fileName":"cardbackpath"}
      //     this.$http.post(this.GLOBAL.host+'/tpisAuth/scanPhotoInfo',data,{
      //       headers: {
      //         'Content-Type':'application/json;charset=utf-8'
      //       }
      //     }).then(res=>{
      //       // console.log(res.data.data);
      //       // this.iptInfo.imgsrc2=res.data.data.idCardExpire.cardbackpath;
      //       this.iptInfo.endTime=res.data.data.idCardExpire.date;
      //     },err =>{
      //       console.log(err)
      //     })
      //   }else if(type=='3'){
      //     this.iptInfo.imgsrc3=decodeURIComponent(params);
      //     var data={"imagebase64":this.iptInfo.imgsrc3,"custId":this.custid,"fileName":"settlefrontpath"}
      //     this.$http.post(this.GLOBAL.host+'/tpisAuth/scanPhotoInfo',data,{
      //       headers: {
      //         'Content-Type':'application/json;charset=utf-8'
      //       }
      //     }).then(res=>{
      //       console.log(res)
      //       this.iptInfo.mcardNum=res.data.data.accountNo.number;
      //     },err =>{
      //       console.log(err)
      //     })
      //   }else if(type=='4'){
      //     this.iptInfo.imgsrc4=decodeURIComponent(params)
      //   }
      // },
      // getImg(arg){
      //   var u = navigator.userAgent, app = navigator.appVersion;
      //   var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1;
      //   var isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/);
      //   // console.log(arg)
      //   if (isAndroid) {
      //     window.android.getPicture(arg); // Android
      //   }
      //   if (isIOS) {
      //     window.webkit.messageHandlers.getPicture.postMessage(arg);   // ios
      //   }
      // },
      getImg(e,type) {
          let file = e.target.files[0];
          this.checkAndHandleCompression(file).then( fileOptions => {
            let {uploadSrc, uploadFile} = fileOptions;
            console.log(fileOptions)
                var imgsrc="imgSrc"+type;
                document.getElementById(imgsrc).src =uploadSrc;// 载入生成后的图片base64
            if(type==0){
              var src0=document.getElementById("imgSrc0").src;
              this.iptInfo.imgsrc0=src0;
            }
            if(type==1){
              // 身份证正面
              var src1=document.getElementById("imgSrc1").src;
              this.iptInfo.imgsrc1=src1;
              var data={"imagebase64":src1,"custId":this.custid,"fileName":"cardfrontpath"}
              this.$http.post(this.GLOBAL.host+'/tpisAuth/scanPhotoInfo',data,{
                headers: {
                  'Content-Type':'application/json;charset=utf-8'
                }
              }).then(res=>{
                console.log(res.data.data);
                this.iptInfo.cardId=res.data.data.idCard.number;
                // this.iptInfo.imgsrc1=res.data.data.idCard.cardfrontpath;
                this.iptInfo.name=res.data.data.idCard.name;
                this.iptInfo.mName=res.data.data.idCard.name;
              },err =>{
                console.log(err)
              })
            }
            if(type==2){
              // 身份证反面
              var src2=document.getElementById("imgSrc2").src;
              this.iptInfo.imgsrc2=src2;
              var data={"imagebase64":src2,"custId":this.custid,"fileName":"cardbackpath"}
              this.$http.post(this.GLOBAL.host+'/tpisAuth/scanPhotoInfo',data,{
                headers: {
                  'Content-Type':'application/json;charset=utf-8'
                }
              }).then(res=>{
                // console.log(res.data.data);
                // this.iptInfo.imgsrc2=res.data.data.idCardExpire.cardbackpath;
                this.iptInfo.endTime=res.data.data.idCardExpire.date;
              },err =>{
                console.log(err)
              })
            }
            if(type==3){
              // 银行卡
              var src3=document.getElementById("imgSrc3").src
              this.iptInfo.imgsrc3=src3;
              var data={"imagebase64":src3,"custId":this.custid,"fileName":"settlefrontpath"}
              this.$http.post(this.GLOBAL.host+'/tpisAuth/scanPhotoInfo',data,{
                headers: {
                  'Content-Type':'application/json;charset=utf-8'
                }
              }).then(res=>{
                console.log(res)
                this.iptInfo.mcardNum=res.data.data.accountNo.number;

              },err =>{
                console.log(err)
              })

            }
            if(type==4){
              var src4=document.getElementById("imgSrc4").src;
              this.iptInfo.imgsrc4=src4;

            }
          });
      },
      getValue() {
        if (this.nid==22){
          if (this.iptInfo.name!=''&&this.iptInfo.cardId!=''&&this.iptInfo.endTime!=''&&
            this.iptInfo.licenceId!=''&&this.iptInfo.licenceName!=''&&this.iptInfo.licenceAddress!='') {
            this.isB = true;
          } else { this.isB =false ;}
        }else if (this.nid==11) {
          if (this.iptInfo.mName!=''&&this.iptInfo.mcardNum!=''&&this.iptInfo.endTime!=''&&
            this.iptInfo.mbank!=''&&this.iptInfo.cardId!='') {
            this.isB = true;
          } else { this.isB =false ;}
        }
      },
      validCardId(cardId){
        let reg = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/;
        return reg.test(cardId);
      },
      nextStep1() {
        if(this.nid==22){
          if(this.iptInfo.imgsrc0==''||this.iptInfo.imgsrc1==''||this.iptInfo.imgsrc2==''){
            this.$vux.toast.text('请上传图片', 'center');
            return false;
          }else  if (this.iptInfo.name==''||this.iptInfo.cardId==''||this.iptInfo.endTime==''||
            this.iptInfo.licenceId==''||this.iptInfo.licenceName==''||this.iptInfo.licenceAddress==''){
            this.$vux.toast.text('请填写所有信息', 'center');
            return false;
          }else if(!this.validCardId(this.iptInfo.cardId)){
            this.$vux.toast.text('请输入正确的身份证号', 'center');
            return false;
          }else{
            var step1={agentid:  this.agentid,step:1,custid: this.custid,macType:this.tid,  businesslicenseImg:this.iptInfo.imgsrc0,
              cardfrontpath:this.iptInfo.imgsrc1,  cardbackpath:this.iptInfo.imgsrc2,  corporation:this.iptInfo.name,
              idCardNo:this.iptInfo.cardId, expiryTime:this.iptInfo.endTime ,businesslicenseNo: this.iptInfo.licenceId,
              businesslicenseName: this.iptInfo.licenceName,businesslicenseAddress: this.iptInfo.licenceAddress }
            console.log(step1);
            this.$http.post(this.GLOBAL.host+'/enterprise/addMerchantInfo',step1 ,{headers: {
                'Content-Type':'application/json;charset=utf-8'
              }})
              .then((res)=>{
                console.log(step1)
                if(res.data.code==0){
                  this.$store.commit("showInfo1");
                  this.$router.push('/type/' + this.tid + '/' +this.nid + '/account');
                }else{
                  this.$vux.toast.text(res.data.data+'1', 'center');
                }
              })
          }
        }
        else if(this.nid==11){
          if(this.tid==4||this.tid==11){
            if(this.iptInfo.imgsrc1==''||this.iptInfo.imgsrc2==''||this.iptInfo.imgsrc3==''||this.iptInfo.imgsrc4==''){
              this.$vux.toast.text('请上传图片', 'center');
              return false;
            }
          }else{
            if(this.iptInfo.imgsrc1==''||this.iptInfo.imgsrc2==''||this.iptInfo.imgsrc3==''){
              this.$vux.toast.text('请上传图片', 'center');
              return false;
            }
          }
          if (this.iptInfo.mName==''||this.iptInfo.mcardNum==''||this.iptInfo.endTime==''||
            this.iptInfo.mbank==''||this.iptInfo.cardId==''){
            this.$vux.toast.text('请填写所有信息', 'center');
            return false
          }else if(!this.validCardId(this.iptInfo.cardId)){
            this.$vux.toast.text('请输入正确的身份证号', 'center');
            return false;
          }else{
            var step1={agentid:  this.agentid,step:1,custid: this.custid,macType:this.tid,
              cardbackpath:this.iptInfo.imgsrc2, cardfrontpath:this.iptInfo.imgsrc1,   storephotopath:this.iptInfo.imgsrc4,settlefrontpath:this.iptInfo.imgsrc3,
              accountName:this.iptInfo.mName, bank:this.iptInfo.mbank,
              idCardNo:this.iptInfo.cardId, expiryTime:this.iptInfo.endTime,
              accountNo:this.iptInfo.mcardNum}
            this.$http.post(this.GLOBAL.host+'/smallMicro/addMerchantInfo',step1 )
              .then((res)=>{
                console.log(res)
                if(res.data.code==0){
                  this.$store.commit("showInfo1");
                  this.$router.push('/type/' + this.tid + '/' +this.nid + '/business');
                  sessionStorage.setItem('mName',this.iptInfo.mName)
                  sessionStorage.setItem('cardId',this.iptInfo.cardId)
                }else{
                  this.$vux.toast.text('提交失败', 'center');
                }
              })
          }

        }

      },
      show() {
        this.$refs.picker.show();
      },
      handlePickerConfirm(v) {
        this.picker.anchor = v
        this.iptInfo.mbank = v[0].value ? v[0].value : null;
        console.log( v[0].value)
      },
      handlePickerCancel(data) {
      },
      change(value){
        // console.log(value)
      },

      // GetQueryString(name) {
      //   var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
      //   var r = window.location.search.substr(1).match(reg);
      //   if(r!=null)return  unescape(r[2]); return null;
      // },
    }

  }
</script>
<style>

</style>
