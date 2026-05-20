<script setup lang="ts">
import Bgfloat from './bgfloat.vue';

  import SplitText from "../component/SplitText/SplitText.vue";
  import Issam from "../assets/image/issam.png"

  const handleAnimationComplete = () => {
    console.log('All letters have animated!');
  };


 import ProfileCard from "../component/ProfileCard/ProfileCard.vue";
import Dialog from './dialog.vue';

  const handleContactClick = () => {
    console.log('Contact button clicked!');
  };
</script>

<template>
  <div class=" ">
    <Bgfloat class="flex flex-col items-center justify-center ">

      <SplitText
    text=""
    class-name="text-[30px] font-bold   text-white "
    :delay="100"
    :duration="0.6"
    ease="power3.out"
    split-type="chars"
    :from="{ opacity: 0, y: 40 }"
    :to="{ opacity: 1, y: 0 }"
    :threshold="0.1"
  
    text-align="center"
    @animation-complete="handleAnimationComplete"
  />

      

      <div class="flex flex-col justify-center items-center ">
      


              <ProfileCard

   
  ></ProfileCard>

 <div class="p-">
  .

 </div>
     <Dialog class="p-2" />

      <div class="p-1">
  .

 </div>
 
  
 


                



       
      </div>
      
    </Bgfloat>
  </div>

</template>

