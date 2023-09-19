<template>
    <div>
      <v-app-bar
        color="primary"
        dense
        flat
        dark
      >
        <v-toolbar-title>Register</v-toolbar-title>
      </v-app-bar>
      <v-container class="pt-0 pb-0">
        <v-row>
          <v-col cols="12">
            <div class="set-padding">
              <div class="text-center mt-10">
                <img src="~/assets/gift05.png" alt="" width="236px">
                <h1 class="text-title">ยินดีต้อนรับ, {{ name }}</h1>
                <p class="mt-7">
                  ยินดีต้อนรับ,<br/>เข้าสู่เว็บทำภารกิจแชร์ออนไลน์นะคะ<br/> มาเริ่มสร้างรายได้ให้ตัวเองกันค่ะ.
                </p>
              </div>
              <v-btn rounded color="primary" dark class="w-100 mt-10 my-btn" @click="mission">ทำภารกิจตอนนี้</v-btn>
              <div class="w-100 text-center my-btn outlined text-primary mt-5" @click="close">Close</div>                    
            </div>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </template>


<script>
export default {  
  data(){
    return {
      name: this.$store.getters.getRegister.firstname
    }
  },
  methods: {
    mission(){
      this.$router.push('mission')
    },
    close(){
      liff.closeWindow();
    }
  }
}
</script>