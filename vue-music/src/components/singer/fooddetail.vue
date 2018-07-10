<template>
 	<transition name="slide">
		<div class="my-singer-detail">
			{{msg+','+get+','+post1+","+childValue}}
      <yd-button @click.native="sdsd" size="large" type="danger">danger</yd-button>
      
		</div>
	</transition>
</template>

<script>
import { lookOption } from '@/common/js/axous.js'
import {mapActions,mapMutations,mapGetters,mapState} from 'vuex';


export default {
  components: {
    
  },
  data(){
        return {
          msg:'',
          get:0,
          post1:0,
          childValue: '我是子组件的数据',
         
        }
  },
  ...mapActions(['switch_dialog','switch_dialog1']),
	created(){
    this.get=this.$route.query.getid
    this.post1=this.$route.params.postid
    lookOption().then(res=>{
      this.switch_dialog1()
      console.log(res.data)
      this.msg=res.data.result.mobile
      setTimeout(()=>{
        this.switch_dialog()
      },2000)
    }).catch(err=>{
      console.log(err)
    })
  },
  methods:{
    sdsd(){
      // console.log(this.childValue)
      this.$router.go(-1)
      this.$emit('childByValue',this.childValue)
      
    }
  }
}

</script>

<style lang="scss" scoped>
@import '~@/common/scss/const.scss';
@import '~@/common/scss/mymixin.scss';
.my-singer-detail {
	width:100%;
	height:100%;
  position: fixed;
  z-index: 100;
  top: $headerheight;
  left: 0;
  right: 0;
  bottom: $headerheight;
  background:$color-background ;
}

.slide-enter-active, .slide-leave-active {
  transition: all .3s ease;
}
.slide-enter, .slide-leave-to {
  opacity: 0;
  transform: translate3d(100%, 0, 0);
}
.loading{
  width:100%;
  height:100%;
  position:fixed;
  top:0;
  left:0;
  background:rgba(255,255,255,.5);
  z-index:1000;
  .sds{
    position:absolute;
    left:50%;
    top:50%;
    margin-left:-50px;
  }
}
</style>