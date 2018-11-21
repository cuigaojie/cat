<template>
    <div class="content">
      <div class="flow"><img src="../assets/img/jinj_pic_qysh_e.png" alt="" class=""></div>
      <div class="image_list">
        <!--门面照、-->
        <div class="default_img p_r pic7">
          <!--<img :src="iptInfo5.storephotopath"  id="imgSrc7"/>-->
          <!--<input type="file" accept="image/*" capture="camera"  @keyup="getValue" @change='getImg($event,"7")'>-->

            <div  @click='getImg("7")' class="boximg">
              <img :src="iptInfo5.storephotopath"  id="imgSrc7"/>
            </div>
            <div class="box"  v-show="iptInfo5.storephotopath">
              <i class="delect" @click="delImg('7')"></i>
              <i class="look_big" @click="look('7')"></i>
            </div>

        </div>
        <!--收银台照-->
        <!--<div class="default_img p_r pic8">-->
          <!--<img :src="" />-->
          <!--<input type="file" accept="image/*" capture="camera"  @keyup="getValue">-->
        <!--</div>-->
        <!--&lt;!&ndash;店铺内部照、&ndash;&gt;-->
        <!--<div class="default_img p_r pic9">-->
          <!--<img :src="" />-->
          <!--<input type="file" accept="image/*" capture="camera"  @keyup="getValue">-->
        <!--</div>-->

      </div>
      <!--查看大图-->
      <div class="bigImg" v-show="isEnlargeImage==true">
        <!--<img :src="base64Img" alt="">-->
        <img :src="base64Img" alt="">
      </div>
      <div class="mask" v-show="isEnlargeImage==true" @click="isEnlargeImage=false"></div>
      <div :class="{'light': isB}" class="next_btn" @click="nextStep">下一步</div>
    </div>
</template>

<script>
  import imageUploadMixins from '@/mixins/image-compress'
    export default {
        name: "imgInfo",
      mixins: [imageUploadMixins],
      data(){
      return{
        isB:false,
        base64Img:'',
        isEnlargeImage:false,
        custid: sessionStorage.getItem('custid'),
        // iptInfo5:{"storephotopath":''},
        iptInfo5: this.$store.state.ipt_Info5,
        tid:this.$route.params.tid,
        nid:this.$route.params.nid,
      }
      },
      created(){
        window.getImg=this.getImg;
        window.getPic=this.getPic;
      },
      mounted() {
        localStorage.setItem("nid", this.$route.params.nid);
        setTimeout((params,type) => {
          this.getPic(params,type)
        }, 20)},
      methods:{
        getValue(){},
        // getImg(e,type) {
        //     let file = e.target.files[0];
        //     this.checkAndHandleCompression(file).then( fileOptions => {
        //       let {uploadSrc, uploadFile} = fileOptions;
        //       console.log(fileOptions)
        //           var imgsrc="imgSrc"+type;
        //           document.getElementById(imgsrc).src =uploadSrc;// 载入生成后的图片base64
        //       if(type==7){
        //         // 身份证正面
        //         var src7=document.getElementById("imgSrc7").src;
        //         this.iptInfo5.storephotopath=src7;
        //       }
        //     });
        // },
        getPic(params,type){
            if(type==7) {//开户许可证
              this.iptInfo5.storephotopath=decodeURIComponent(params);
          }
        },
        getImg(arg){
          var u = navigator.userAgent, app = navigator.appVersion;
          var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1;
          var isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/);
          if (isAndroid) {
            window.android.getPicture(arg); // Android
          }
          if (isIOS) {
            window.webkit.messageHandlers.getPicture.postMessage(arg);   // ios
          }
        },
        delImg(type){
          if(type==7){
            this.iptInfo5.storephotopath=null
          }
        },
        look(type){
          this.isEnlargeImage=true;
          if(type==7){
            this.base64Img=this.iptInfo5.storephotopath
          }
          },
        nextStep(){
          if(this.iptInfo5.storephotopath==''){
            this.$vux.toast.text('请上传图片', 'center');
          }else{
          let step5={step:5,storephotopath:this.iptInfo5.storephotopath,custid: this.custid}
          this.$http.post(this.GLOBAL.host+'/enterprise/addMerchantInfo', step5)
            .then((res) => {
              console.log(res)
              if (res.data.code == 0) {
                this.$store.commit("showInfo5");
                this.$router.push('/type/' + this.tid + '/' +this.nid + '/all');
              } else {
                this.$vux.toast.text('上传失败', 'center');
              }
            })
          }

        }
      }
    }
</script>

<style scoped>
  .pic7{
    background:url('../assets/img/jinj_pic_mmzp.png') center center;
    background-size: 4.9rem;
  }
  /*.pic8{*/
    /*background:url('../assets/img/jinj_pic_syt.png') center center;*/
    /*background-size: 4.9rem;*/
  /*}*/
  /*.pic9{*/
    /*background:url('../assets/img/jinj_pic_dpnb.png') center center;*/
    /*background-size: 4.9rem;*/
  /*}*/

</style>
