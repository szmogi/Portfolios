<template>


      <me-contact :vis-contact="this.contactVis">

      </me-contact>


      <div class="profil-medium">

          <img-profil
             :animated="this.profilAnimated"
             :visible="this.profilVisible"
             >
          
          </img-profil>

      </div>


      <div class="about-medium">

          <me-about
          :about-vis="this.aboutVis">


          </me-about>

      </div>

        <div  id="icons-skills" >     
                        
                    <me-skills v-for="item in iconArray" :key="item.id"                
                     v-show="skillsIconVis"  
                    :icon-Name="item.icon"
                    :ide="item.id"
                    :progress-color="item.color"
                    :number-percente="item.numberPercete"
                    :progress-width="item.progressWidth"
                    :skills-anime="this.isSkillAnime" 
                    :name="item.name"
                              >

                    </me-skills>
                  
          </div>


         
         
         <div id="medium-project" >
             
              <me-project
               v-if="projectVis"
              :project-animated="this.profilAnimated"
              :back-icon-vis="this.projectBackIcon"
              >

              </me-project>
                

         </div>





   
</template>

<script>
import ImgProfil from "./portfolio/imgProfil.vue"
import MeAbout from './portfolio/meAbout.vue';
import MeSkills from './portfolio/meSkills.vue';
import MeContact from './portfolio/meContact.vue';
import MeProject from './projectMe.vue';

var id = 0;
export default { 
    components: { ImgProfil, MeAbout, MeSkills,MeContact,MeProject },
    props: {
    
    },
    data() {
        return {
          profilAnimated:true,
          profilVisible:true,
          aboutVis:false,
          skillsIconVis:false,
          isSkillAnime:false,
          contactVis:false,
          projectVis:false,
          profilAnimated:false,         
          projectBackIcon:false,
          window:{
            height:null,
            width:null,            
          },
          scroll:null,

          
         

         iconArray:
          [
            {id:id++, name:'Css', icon:'icons8-css3-120.png',
            color:'linear-gradient(90deg, rgba(0,96,253,1) 1%, rgba(33,129,199,1) 34%, rgba(76,145,198,1) 59%, rgba(65,107,236,1) 96%)',
            numberPercete:70,progressWidth:'70%'},           
            {id:id++, name:'Git',  icon:'icons8-git-96.png',
            color:'linear-gradient(90deg, rgba(255,112,83,1) 1%, rgba(200,154,48,1) 31%, rgba(255,122,96,1) 59%, rgba(232,169,25,1) 96%)',
            numberPercete:30,progressWidth:'30%'},
            {id:id++, name:'Google',  icon:'icons8-google-96.png',
            color:'linear-gradient(90deg, rgba(233,66,53,1) 1%, rgba(250,187,5,1) 43%, rgba(52,168,83,1) 75%, rgba(66,133,244,1) 96%)',
            numberPercete:70,progressWidth:'70%'},
            {id:id++, name:'Html',  icon:'icons8-html-5-96.png',
            color:' linear-gradient(110deg, rgba(228,50,0,1) 1%, rgba(255,160,133,1) 29%, rgba(224,49,0,1) 64%, rgba(255,132,98,1) 83%)',
            numberPercete:70,progressWidth:'70%'},
            {id:id++, name:'JavaScript',  icon:'icons8-javascript-logo-96.png',
            color:'linear-gradient(75deg, rgba(207,180,51,1) 1%, rgba(255,207,0,1) 25%, rgba(226,187,1,1) 66%, rgba(255,225,96,1) 83%)',
            numberPercete:60,progressWidth:'60%'},
            {id:id++, name:'jQuery', icon:'icons8-jquery-96.png',
            color:'linear-gradient(287deg, rgb(5, 115, 189) 13%, rgb(204 234 253) 34%, rgb(24 145 226) 56%, rgb(154 191 255) 103%)',
            numberPercete:60,progressWidth:'60%'},
            {id:id++, name:'Laravel', icon:'icons8-laravel-100.png',
            color:'linear-gradient(90deg, rgba(255,34,26,1) 1%, rgba(235,113,109,1) 36%, rgba(255,102,96,1) 71%, rgba(255,68,63,1) 94%)',
            numberPercete:60,progressWidth:'60%'},
            {id:id++, name:'Mysql',  icon:'icons8-mysql-logo-96.png',
            color:'linear-gradient(250deg, rgb(0 129 184) 26%, rgb(251 169 33) 47%, rgb(0, 94, 134) 67%, rgb(221, 138, 0) 89%)',
            numberPercete:50,progressWidth:'50%'},
            {id:id++, name:'Php',  icon:'icons8-php-logo-96.png',
            color:'linear-gradient(90deg, rgba(9,9,9,0.7217261904761905) 1%, rgba(115,119,173,1) 36%, rgba(80,87,177,1) 63%, rgba(138,144,218,1) 94%)',
            numberPercete:50,progressWidth:'50%'},
            {id:id++, name:'Sass',  icon:'icons8-sass-avatar-96.png',
            color:'linear-gradient(90deg, rgba(198,99,148,1) 1%, rgba(148,155,249,1) 36%, rgba(198,99,148,1) 63%, rgba(180,185,245,1) 94%)',
            numberPercete:60,progressWidth:'60%'},
            {id:id++, name:'Vue.js',  icon:'icons8-vuejs-96.png',
            color:'linear-gradient(241deg, rgba(63,178,127,1) 5%, rgba(59,143,115,1) 15%, rgba(51,71,91,1) 36%, rgba(63,178,127,1) 76%, rgba(51,71,91,1) 91%)',
            numberPercete:60,progressWidth:'60%'}
          ]


        }

    },watch:{
       scroll:function(newVal){
         var profil = document.querySelector('.profil-medium').offsetHeight     
         
         
        
         if(newVal > (profil)){      
             this.isSkillAnime = true
             this.skillsIconVis = true 
           
         }
         
         if (newVal > 1100){
             this.projectVis = true
         }
       }
   
    },
    mounted(){   
       this.showStart();     
        
        
    },methods:{
      showStart(){
        this.profilAnimated = true
        setTimeout(()=>{ this.contactVis = true,this.aboutVis = true},2000)
      },
      handleResize(e){
          this.window.width = window.innerWidth;         
          this.window.height = window.innerHeight;   
         
      },
      onScroll(e) {
      this.scroll = e.target.documentElement.scrollTop.toFixed(0);  

     }
    
      

    },created(){
      window.addEventListener('resize', this.handleResize);
      window.addEventListener("scroll", this.onScroll);
      this.handleResize();    

        
    },
     destroyed() {
         window.removeEventListener('resize', this.handleResize);
         window.removeEventListener("scroll", this.onScroll);
    }

   
}
</script>

<style lang="scss" scoped>
   


   .about-medium{
             padding: 6rem 0rem 4rem;
               overflow: hidden;
         }


   .icon-skill{
     padding: 4rem 0rem;
   }      





    @media (max-width:1020px){
       #icons-skills{
         display: -webkit-box;
         display: -ms-flexbox;
         display: flex;
         -webkit-box-orient: horizontal;
         -webkit-box-direction: normal;
             -ms-flex-direction: row;
                 flex-direction: row;
         -webkit-box-pack: space-evenly;
             -ms-flex-pack: space-evenly;
                 justify-content: space-evenly;
         -ms-flex-wrap: wrap;
             flex-wrap: wrap;
       }
    }

  

</style>