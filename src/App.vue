<script setup>
import PortfolioContainer from './components/PortfolioContainer.vue'
import MediumPortfolio from '/src/components/mediumPortfolio.vue'
</script>

<template>
  <main :id="classMain">

    <portfolio-container v-if="xxlSize">

    </portfolio-container>


    <medium-portfolio v-else >

    </medium-portfolio>
  
    </main>


       <footer>
      <section class="link-footer">       
          <ul>
              <li><a style="font-size:.6rem" target="_blank" href="https://icons8.com/icon/"></a>Icon by <a target="_blank" href="https://icons8.com">Icons8</a></li>
              <li style="font-size:.8rem">&#169;szmo 2022. All rights reserved.</li>
              <li style="font-size:.8rem"><a href="mailto:juraj.smatana@szmogi.site"><small>Web design and features created &nbsp;</small><strong>Powered&nbsp;by&nbsp;Szmo</strong></a></li>            
          </ul>         
      </section>
    </footer>
</template>
<style>
@import './assets/base.css';

</style>


<script>
export default {
  components: { MediumPortfolio,PortfolioContainer },
  data () {
    

    return {
      window:{
                height:null,
                width:null,
            },
       classMain:'normal-size',       
       xxlSize:true,
       allClose:false,
      
       
    }
  }, 
  methods: {
        handleResize(){
             this.window.width = window.innerWidth;
             this.window.height = window.innerHeight;          
         


                   if(this.window.width < 1010){
                      this.xxlSize = false          
                      this.classMain = 'medium-size'
                      this.allClose = true
                   
                   }else{
                      this.xxlSize = true    
                      this.classMain = 'normal-size'

                    
                   }


         },
         

  },
  
  created() {
       window.addEventListener('resize', this.handleResize);
       this.handleResize();    

    },
    unmounted() {
         window.removeEventListener('resize', this.handleResize);

   }
}
</script>

<style lang="scss" scoped>

</style>

<style lang="scss" scoped>


 #normal-size{
        display: -webkit-inline-box;
        overflow: hidden;
        width:1000px;
        height:800px; 
        
  }


  #medium-size{
        min-height: 100rem;
  }
















</style>



