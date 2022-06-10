
<template>

      

       <transition name="slide-Portfolio">    
             <div v-if="welcomVis" class="welcom">             
                  <button  @click="join()" class="welcom-button">Vstúpiť</button>               
             </div>       
        
        </transition>

         <me-contact :vis-contact="this.contactVis">

        </me-contact>


        

       

        
 <transition name="slide-Portfolio">    

   <div v-if="portfolioVis" id="portfolio" class="portfolio-xxl">
             

    <div class="top-flex-group">
              
         <div class="profil-img">
                  
                    <img-profil
                    :animated="this.imgAnimated"
                    >
                
                    </img-profil>
                
            </div>

              <div class="about-me">
                      
                    
                      <me-about
                      :about-vis="this.aboutVis">

                      </me-about>


              </div>
        


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
                    @next-pages="visNextPage($event)"
                    :name="item.name"
                      
                          >

                    </me-skills>
                  
          </div>

          
           <figure class="project-click project-on-class" v-if="projectIconVis">
                 <img @click="project()" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAABmJLR0QA/wD/AP+gvaeTAAACL0lEQVRoge2ZMWsUQRTHf7e5CEIIYhE9i5AmnyAQrBQEJYUpxCJF0iskpZiQSkFEIbG20MavoKTSHCIIEkLSprMLmCaQBAzCXYp5yQ3nzs7N7uzObtgfPLi9eXv7/9/Mm3vMQU15mQXawLHEJnA3qKIUvAa6hlgNqMuJWZTgU+A5cEtiWd7rAPeDqXOgjTKyHDO2ImOfC1WUkiOU2FbMWAvzkis6EmloSQ1DjvVDCsKkD4CoKBV5UxsJxA8MNVM1I0aqWOyxekPNyFsR0h+ZsO3Trvt
                 9R8KW98LxWXF6L2rG94x0gEVUq2NjDhj1+XBfM/IPWNDue5mQuwOMSd7EgM8y6b249mHkL/BI8keAprxej8n9CVyT8RnghN4yC2rkBHggudeBX8An1EbSAN5ruV/FKMBjVHet10wwI0fAPcm7AexqYx
                 /p7UYfgC/AVcmdRy1Fl00kNyMHwJTkjAN7MTlrMt4EhuX1EoPtaoUY6QC3ZXwS+J0gQN9mV1MYyH1GvgPTwP4AIp4BbzKYsBrJ2qJ0E+7zjalF6UL2FqUoE1YuTferG7kDbAB/JDbkvUqg10
                 iae32TpCXXGikNTXuKkbQzmQuXZkYi1IF15YmArdAifBAB70KL8MkrsvVBRcQ5tmseAt/oHWqXLRKNlKZXcsDpB/EpcIj6z+Rmvrry5Qnhl1LapfYfM6jDgkrUTBVrpJ/EGumnrpmiYmhAI9uog
                 7cW6qjzivNXUVNTU1OjcQYLETcCHV0NTQAAAABJRU5ErkJggg=="/>
           </figure>          

       
        
     </div>
 </transition>  
  
  <transition name="slide-Portfolio">    
      <div id="project" v-if="projectVis">
           <me-project
            :project-animated="this.projectAnimated"
            @back-page="isPages($event)">

           </me-project>
           

      </div>
   </transition>

</template>





<script>
import meAbout from './portfolio/meAbout.vue';
import meSkills from './portfolio/meSkills.vue'
import imgProfil from './portfolio/imgProfil.vue'
import meContact from './portfolio/meContact.vue'
import meProject from './projectMe.vue'

var id = 0;
export default {
  components: { meSkills, imgProfil, meContact, meAbout, meProject },
   data () {     

      return {
         skillsIconVis:false,
         isSkillAnime:false,
         projectIconVis:false,
         imgAnimated:false,
         contactVis:false,
         aboutVis:false,
         welcomVis:true,
         portfolioVis:false,
         projectVis:false,
         projectAnimated:false,
         
         X:0,
         Y:0,
         
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
   },
   mounted(){     


    },
   methods: {
     mouseleave(){



     },
      visProfilAll(){  
        this.imgAnimated = !this.imgAnimated
         setTimeout(()=>{
           this.aboutVis = !this.aboutVis            
              setTimeout(()=>{
                this.isSkillAnime = !this.isSkillAnime
                this.skillsIconVis = !this.skillsIconVis
                   setTimeout(()=>{
                       this.contactVis = !this.contactVis        
                   },5000)
              },2000)
         },2000)   
    
      },     
      visNextPage(data){
        if(data == true){
          this.projectIconVis = true
        }
      },
      join(){
        this.welcomVis = false
        this.portfolioVis = true
          setTimeout(()=>{
              this.visProfilAll()
          },1500)
      },
      project(){  
        this.imgAnimated = false     
        setTimeout(()=>{
           this.projectAnimated = true          
           this.projectVis = true
           this.portfolioVis = false
           this.closeAll()
        },10)
        
        
      },
      isPages(data){
         if(data == true){      
           this.projectVis = false     
           this.portfolioVis = true
          setTimeout(()=>{
             this.visProfilAll()     
          },2000)    
         }
      },
      closeAll(){          
          this.aboutVis = false
          this.isSkillAnime = false
          this.skillsIconVis = false
          this.contactVis = false            
          this.projectIconVis = false          
       
      },
     

   
   },
  

}

</script>



<style lang="scss" scoped>





 .portfolio-xxl{
   width:1000px;
   height:800px;   
   border-top-right-radius: 5pc;
   border-bottom-left-radius: 5pc;
   border-bottom-right-radius: 5pc;
   background: rgb(101,198,255);
   background: -o-radial-gradient(circle, rgba(101,198,255,1) 0%, rgb(152 255 188) 100%);
   background: radial-gradient(circle, rgba(101,198,255,1) 0%, rgb(152 255 188) 100%);  
   position: absolute;
   z-index: 2;


 }


  #project{
       
    border-top-right-radius: 5pc;
    border-bottom-left-radius: 5pc;
    border-bottom-right-radius: 5pc;
    background: rgb(101,198,255);
    background: -o-radial-gradient(circle, rgba(101,198,255,1) 0%, rgb(152 255 188) 100%,rgba(101,198,255,1) 0%);
    background: radial-gradient(circle, rgba(101,198,255,1) 0%, rgb(152 255 188) 100%,rgba(101,198,255,1) 0%); 
    position: absolute;
    z-index: 1;
  
       
  }


  


  .project-click{
    bottom: 4rem;
    left: 24rem;
    cursor: pointer;
  }





 #icons-skills{
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
    -ms-flex-wrap: wrap;
        flex-wrap: wrap;
    -ms-flex-pack: distribute;
        justify-content: space-around;
  
 }

 .profil-img{
   width:400px;
   height:400px;
 
   display: -webkit-box;
 
   display: -ms-flexbox;
 
   display: flex;
   -webkit-box-orient: vertical;
   -webkit-box-direction: normal;
       -ms-flex-direction: column;
           flex-direction: column;
   -webkit-box-align: center;
       -ms-flex-align: center;
           align-items: center;
   -ms-flex-pack: distribute;
       justify-content: space-around;
   overflow: hidden;
 }

 .about-me{
   width:600px;
   height:400px;
  

    display: -ms-grid;
  

    display: grid;
   justify-items: start;
    -ms-flex-line-pack: center;
        align-content: center;
    overflow: hidden;
 }

 .top-flex-group{
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
 }

.welcom{
  width: 1000px;
  height:800px;
  background: rgb(101,198,255);
  background: -o-radial-gradient(circle, rgba(101,198,255,1) 0%, rgb(152 255 188) 100%);
  background: radial-gradient(circle, rgba(101,198,255,1) 0%, rgb(152 255 188) 100%);
  position: absolute;
  z-index: 3;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  -ms-flex-pack: distribute;
      justify-content: space-around;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
  border-top-right-radius: 5pc;
  border-bottom-left-radius: 5pc;
  border-bottom-right-radius: 5pc;
  

   button{
     padding:.5rem 1rem;
     font-size:4rem;
     font-weight:600;
     border: none;    
     cursor: pointer;     
     color: #2a6776;
     background: rgb(101,198,255);
     background: -o-radial-gradient(circle, rgb(143 214 255) 0%, rgb(164 255 196 / 75%) 100%);
     background: radial-gradient(circle, rgb(143 214 255) 0%, rgb(164 255 196 / 75%) 100%);
     border-top-right-radius: 1pc;
     border-bottom-left-radius: 1pc;
     border-bottom-right-radius: 1pc;
     -webkit-box-shadow: 0 0 8px 5px rgb(34 170 249 / 72%);
             box-shadow: 0 0 8px 5px rgb(34 170 249 / 72%);





     &:hover,
     &:active{       
       -webkit-box-shadow: 0 0 10px 10px rgb(34 170 249);       
               box-shadow: 0 0 10px 10px rgb(34 170 249);
     }
     

   }
}



       .welcom-button {
            -webkit-animation: welcomvis-on 2s ease-out, entry-animated 1.5s ease-in infinite ;
                    animation: welcomvis-on 2s ease-out, entry-animated 1.5s ease-in infinite ;           
            
           }
     
 
         @-webkit-keyframes welcomvis-on {
             0% {
                -webkit-transform: translateX(-50rem) translateY(-38rem) scale(.1);
                        transform: translateX(-50rem) translateY(-38rem) scale(.1);              
                 
             }                          
            100% {
                  -webkit-transform: translateX(0rem) translateY(0rem) scale(1) ;
                          transform: translateX(0rem) translateY(0rem) scale(1) ;                                  
                           
             }     
                
             
        }
     
 
         @keyframes welcomvis-on {
             0% {
                -webkit-transform: translateX(-50rem) translateY(-38rem) scale(.1);
                        transform: translateX(-50rem) translateY(-38rem) scale(.1);              
                 
             }                          
            100% {
                  -webkit-transform: translateX(0rem) translateY(0rem) scale(1) ;
                          transform: translateX(0rem) translateY(0rem) scale(1) ;                                  
                           
             }     
                
             
        }


          @-webkit-keyframes entry-animated {
            0%{-webkit-box-shadow: 0 0 3px 3px rgb(34 170 249 / 72);box-shadow: 0 0 3px 3px rgb(34 170 249 / 72)}
            50%{-webkit-box-shadow: 0px 0px 15px 5px rgb(34 170 249 / 72);box-shadow: 0px 0px 15px 5px rgb(34 170 249 / 72)}
            100%{-webkit-box-shadow: 0 0 3px 3px rgb(34 170 249 / 72);box-shadow: 0 0 3px 3px rgb(34 170 249 / 72)}
          }


          @keyframes entry-animated {
            0%{-webkit-box-shadow: 0 0 3px 3px rgb(34 170 249 / 72);box-shadow: 0 0 3px 3px rgb(34 170 249 / 72)}
            50%{-webkit-box-shadow: 0px 0px 15px 5px rgb(34 170 249 / 72);box-shadow: 0px 0px 15px 5px rgb(34 170 249 / 72)}
            100%{-webkit-box-shadow: 0 0 3px 3px rgb(34 170 249 / 72);box-shadow: 0 0 3px 3px rgb(34 170 249 / 72)}
          }


        .slide-Portfolio-enter-active {
            -webkit-animation: Portfolio-on 2.8s;
                    animation: Portfolio-on 2.8s;      
            
           }

        .slide-Portfolio-leave-active {
            -webkit-animation: Portfolio-off .8s ease-out ;
                    animation: Portfolio-off .8s ease-out ;      
            
         }
     
 
         @-webkit-keyframes Portfolio-off {
             to {
                -webkit-transform: translateX(-50rem) translateY(-38rem) scale(.1);
                        transform: translateX(-50rem) translateY(-38rem) scale(.1);              
                 
             }                          
           from {
                  -webkit-transform: translateX(0rem) translateY(0rem) scale(1) ;
                          transform: translateX(0rem) translateY(0rem) scale(1) ;                                  
                           
             }                     
             
        }
     
 
         @keyframes Portfolio-off {
             to {
                -webkit-transform: translateX(-50rem) translateY(-38rem) scale(.1);
                        transform: translateX(-50rem) translateY(-38rem) scale(.1);              
                 
             }                          
           from {
                  -webkit-transform: translateX(0rem) translateY(0rem) scale(1) ;
                          transform: translateX(0rem) translateY(0rem) scale(1) ;                                  
                           
             }                     
             
        }

    
     @-webkit-keyframes Portfolio-on {
               0% {
                    -webkit-transform: translateX(-50rem) translateY(-38rem) scale(.1);
                            transform: translateX(-50rem) translateY(-38rem) scale(.1);              
                    
                }                          
              100% {
                      -webkit-transform: translateX(0rem) translateY(0rem) scale(1) ;
                              transform: translateX(0rem) translateY(0rem) scale(1) ;                                                   
                              
                }                       
                
            }

    
     @keyframes Portfolio-on {
               0% {
                    -webkit-transform: translateX(-50rem) translateY(-38rem) scale(.1);
                            transform: translateX(-50rem) translateY(-38rem) scale(.1);              
                    
                }                          
              100% {
                      -webkit-transform: translateX(0rem) translateY(0rem) scale(1) ;
                              transform: translateX(0rem) translateY(0rem) scale(1) ;                                                   
                              
                }                       
                
            }

         



        .project-on-class{
           -webkit-animation: project-on 1s  infinite;
                   animation: project-on 1s  infinite;      
            
        }          
 
         @-webkit-keyframes project-on {
             to {-webkit-transform: scale(1);transform: scale(1);                              
              }                          
            from {-webkit-transform: scale(1.10) ;transform: scale(1.10) ;                          
                           
             }     
                
             
        }          
 
         @keyframes project-on {
             to {-webkit-transform: scale(1);transform: scale(1);                              
              }                          
            from {-webkit-transform: scale(1.10) ;transform: scale(1.10) ;                          
                           
             }     
                
             
        }



     


 




</style>