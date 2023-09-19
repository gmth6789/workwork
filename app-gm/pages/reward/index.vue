<template>
    <div>
      <v-app-bar
        color="primary"
        dense
        flat
        dark
      >
      <v-toolbar-title>แชร์เว็บรับรางวัล</v-toolbar-title>
      </v-app-bar>
      <v-container class="pt-0 pb-0">
        <v-row>
          <v-col>
            <v-card class="mt-8">
              <v-card-text>
                <div class="d-flex">
                  <div>
                    <img :src="getLine.pictureUrl" alt="" width="40" style="border-radius: 50%;">
                  </div>
                  <div class="align-self-center">
                    <h2 class="name text-primary m-0">{{ getUser.firstname }}</h2>
                  </div>
                </div>
              </v-card-text>
              <div class="stamp-zone">
                <div class="stamp" v-for="(obj, index) in stamps" :key="index">
                  <div class="circle" :class="obj.value == true ? 'active' : ''" v-if="index != Object.keys(stamps).length - 1">
                    <span>{{ index+1 }}</span>
                    <v-icon>check</v-icon>
                  </div>
                  <div class="circle end" :class="obj.value == true ? 'active' : ''" v-else>
                    <span>GOAL</span>
                    <v-icon>check</v-icon>
                  </div>
                </div>              
              </div>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn v-if="isDone == false" rounded color="primary" dark class="w-100 mt-10 my-btn scan" @click="scan">
              <svg id="fi_7280222" enable-background="new 0 0 187.4 190.1" height="28" viewBox="0 0 187.4 190.1" width="28" xmlns="http://www.w3.org/2000/svg">
                <path d="m93.7 4.7c-51.7 0-93.7 41.6-93.7 92.7s42 92.7 93.7 92.7 93.7-41.6 93.7-92.7c0-51.2-42.1-92.7-93.7-92.7z" fill="#e5a100"></path><path d="m93.7 0c-50.4 0-91.5 41-91.5 91.5s41 91.5 91.5 91.5 91.5-41 91.5-91.5c-.1-50.5-41.1-91.5-91.5-91.5z" fill="#ffcf00"></path><path d="m93.7 15.5c-41.9 0-76 34.1-76 76s34.1 76 76 76 76-34.1 76-76-34.1-76-76-76zm0 144.4c-37.7 0-68.4-30.7-68.4-68.4s30.7-68.4 68.4-68.4 68.4 30.7 68.4 68.4-30.7 68.4-68.4 68.4z" fill="#e5a100"></path><g fill="#ffe500"><path d="m91.5 182.7c-.4 0-.8-.2-1-.4-.2-.3-.4-.6-.3-1l.6-11.7c.1-.7.5-1.1 1.2-1.1.3 0 .6.1.8.4.2.2.3.5.3.7l-.2 11.8c0 .7-.6 1.3-1.4 1.3zm19.8-1.8c-.5 0-1-.4-1.1-1l-2.1-11.8c0-.3 0-.5.1-.7s.4-.3.6-.4h.2c.5 0 .8.3.9.7l2.7 11.7c.1.4 0 .7-.2 1s-.5.5-.8.6h-.2c.1-.1 0-.1-.1-.1zm-39.7-.9c-.1 0-.2 0-.3 0-.4-.1-.7-.3-.9-.7-.2-.3-.2-.7-.1-.9l3.2-11.6c.1-.4.6-.7 1-.7h.2c.5.1.8.6.7 1.2l-2.5 11.6c-.1.6-.7 1.1-1.3 1.1zm58.9-5.2c-.4 0-.8-.3-1-.7l-4.7-11c-.2-.5 0-1 .5-1.3h.4c.4 0 .7.2.9.5l5.2 10.7c.2.4.2.7.1 1.1-.1.3-.3.5-.5.6l-.3.1c-.3-.1-.4 0-.6 0zm-77.8-2c-.2 0-.4 0-.6-.1-.3-.2-.5-.4-.7-.8-.1-.4-.1-.7.1-1l5.8-10.5c.2-.5.7-.5.8-.5.2 0 .4 0 .5.1.3.1.4.3.5.6.1.2 0 .4 0 .6l-5.2 10.8c-.2.5-.7.8-1.2.8zm95.4-8.2c-.5 0-.9-.2-1.2-.6l-6.9-9.7c-.3-.4-.2-1 .2-1.3.2-.2.4-.2.6-.2.3 0 .6.1.8.4l7.4 9.3c.2.3.3.6.3 1s-.2.7-.5.9l-.1.1c-.3.1-.5.1-.6.1zm-112.2-2.9c-.3 0-.6-.1-.8-.3-.6-.5-.7-1.4-.2-2l7.9-8.9c.2-.2.5-.3.8-.3.2 0 .5.1.6.2.4.3.6.9.2 1.4l-7.4 9.3c-.3.4-.7.6-1.1.6zm126.7-11.1c-.3 0-.6-.1-.9-.4l-8.9-7.9c-.4-.4-.4-1-.1-1.4.2-.2.5-.3.8-.3.2 0 .4.1.6.2l9.3 7.4c.3.2.5.6.5.9 0 .2 0 .6-.3.9l-.1.1v.1c-.3.3-.6.4-.9.4zm-140.4-3.5c-.4 0-.8-.2-1.1-.5-.2-.3-.3-.7-.2-1.1 0-.2.2-.5.5-.7l9.8-7c.1-.1.4-.2.6-.2.3 0 .7.1.9.4.4.5.2 1-.2 1.4l-9.3 7.4c-.4.2-.7.3-1 .3zm151.5-13.2c-.2 0-.4-.1-.6-.1l-10.5-5.8c-.6-.3-.6-.9-.4-1.4l.1-.2v-.1c.2-.2.5-.4.8-.4.1 0 .2 0 .4.1l10.8 5.2c.3.2.6.5.7.8s.1.6-.1.9l-.1.2v.1c-.3.5-.7.7-1.1.7zm-162-4.1c-.5 0-.9-.3-1.1-.8-.2-.3-.2-.6-.1-1 .1-.3.4-.6.7-.8l11-4.7c.1 0 .3-.1.4-.1.4 0 .7.2.9.6s0 1.1-.4 1.2l-10.7 5.2c-.3.3-.5.4-.7.4zm169.2-14.8c-.1 0-.2 0-.3 0l-11.5-3.3c-.5-.1-.8-.7-.7-1.2v-.1c.2-.4.5-.7 1-.7h.2l11.6 2.7c.4.1.7.3.9.6s.2.6.2.9c-.3.7-.8 1.1-1.4 1.1zm-175.3-4.3c-.6 0-1.1-.4-1.3-.9v-.2-.1c-.1-.4 0-.7.2-.9.2-.3.5-.5.9-.6l11.9-2.1h.2c.4 0 .7.3.8.6v.2.1c.1.5-.2 1-.7 1.1l-11.6 2.7c-.1.1-.3.1-.4.1zm166.2-16.2c-.7-.1-1.1-.5-1.1-1.2s.5-1.2 1.2-1.2h11.7c.4 0 .7.2 1 .4.2.3.3.6.3.9v.5c0 .4-.1.6-.2.7-.3.3-.7.5-1.1.5zm-168.1-3.9c-.6 0-1.1-.6-1.1-1.3-.1-.8.4-1.3 1.1-1.3l12.1.6c.4 0 .8.4.8 1 0 .4-.5.9-.9.9zm166.6-13.7c-.5 0-1-.3-1.1-.9-.1-.3 0-.6.1-.8s.3-.3.6-.4l11.7-2.7h.3c.6 0 1.1.4 1.2.9v.2c.2.8-.4 1.4-1.1 1.6zm-152.2-3.6c-.1 0-.2 0-.2 0l-11.7-2.7c-.7-.2-1.1-.9-.9-1.6v-.1-.2c.2-.5.7-.8 1.2-.8.1 0 .2 0 .3.1l11.7 3.3c.2.1.4.2.5.4.1.1.2.4.1.6v.1.2c-.2.5-.5.7-1 .7zm146.5-13.2c-.3 0-.6-.2-.8-.6-.1-.2-.1-.5-.1-.8.1-.3.3-.5.5-.6l10.7-5.3c.2-.1.4-.2.6-.2.5 0 .9.3 1.1.7.1.3.2.7 0 1.1-.1.3-.4.6-.7.7l-11 4.9-.1.1s-.1 0-.2 0zm-140.4-3.1c-.1 0-.3 0-.4-.1l-10.7-5.2c-.3-.2-.6-.5-.7-.8s-.1-.7.1-1l.1-.2v-.1c.3-.4.7-.5 1.1-.5.2 0 .4.1.6.2l10.5 5.9c.3.2.4.4.5.6.1.3 0 .5-.1.8-.2.2-.6.4-1 .4zm131.6-11.8c-.3 0-.6-.2-.8-.4-.4-.5-.3-1 .1-1.4l9.3-7.5c.2-.2.5-.3.9-.3.2 0 .7.1 1 .5.2.3.3.6.3 1s-.2.7-.6.9l-9.6 6.9c-.2.2-.4.3-.6.3zm-121.9-2.7c-.2 0-.4 0-.6-.2l-9.3-7.5c-.6-.5-.7-1.3-.2-1.9.2-.3.6-.4 1-.4.3 0 .6.1.8.3l9 8c.2.2.3.4.3.7s-.1.5-.2.7c-.2.2-.5.3-.8.3zm109.8-10c-.2 0-.4-.1-.6-.2-.5-.4-.5-.9-.2-1.4l7.4-9.3c.3-.3.7-.5 1.1-.5.2 0 .5 0 .8.3.3.2.4.5.4.9s-.1.7-.3.9l-7.9 9c-.1.2-.4.3-.7.3zm-97.2-2.1c-.3 0-.6-.1-.8-.3l-7.4-9.3c-.2-.3-.3-.7-.3-1 0-.2.1-.6.5-.8.3-.2.6-.3.7-.3.4 0 .9.2 1.2.6l6.9 9.6c.3.4.2 1-.2 1.4-.1 0-.3.1-.6.1zm82.7-7.4c-.1 0-.3 0-.4-.1-.2-.1-.4-.3-.5-.6s-.1-.5.1-.8l5.2-10.7c.2-.5.7-.8 1.2-.8.2 0 .4 0 .6.1.3.2.5.4.7.8.1.4.1.7-.1 1l-5.6 10.4c-.5.4-.9.7-1.2.7zm-67.8-1.6c-.4 0-.7-.2-.9-.6l-5.3-10.7c-.2-.3-.2-.7-.1-1s.4-.6.7-.8c.1 0 .3-.1.5-.1.5 0 1 .3 1.2.8l4.7 11c.2.5 0 1-.5 1.3 0 .1-.1.1-.3.1zm51.5-4.6c-.1 0-.2 0-.3 0-.3-.1-.5-.3-.7-.5-.1-.2-.2-.4-.1-.7l2.6-11.7c.1-.6.7-1.1 1.3-1.1h.3c.7.2 1.1.9 1 1.7l-3.3 11.5c-.1.6-.5.8-.8.8zm-34.7-.8c-.5 0-1-.3-1-.7l-2.7-11.6c-.1-.4 0-.8.2-1.1s.5-.4.8-.5h.3c.6 0 1.2.5 1.3 1.2l2.1 11.7c0 .3 0 .5-.1.7s-.4.3-.6.4c-.2-.1-.3-.1-.3-.1zm17.3-1.5c-.7 0-1-.5-1-1v-11.9c0-.8.7-1.3 1.3-1.3h.1c.7 0 1.3.6 1.3 1.4l-.6 11.9c0 .4-.5.9-1.1.9z"></path><path d="m120.1 162.7c-8.6 3.3-18 5-27.4 5-23.2 0-47.1-10.4-62.3-33.9-3.5-5.3-4.7-8.2-4.7-8.2l4.5-8.3c0-.1 0-.2.1-.2 10.1 25.1 34.8 42.8 63.4 42.8 37.7 0 68.4-30.7 68.4-68.4 0-7.2-1.1-14.2-3.2-20.8v-.1c1.9.4 5.5 1.5 8.5 2.4 11.3 42.9-13.5 77.2-47.3 89.7z"></path></g><path d="m93.7 23.1c-37.7 0-68.4 30.7-68.4 68.4 0 9 1.8 17.6 5 25.5 9.2-23.6 36-38.9 57.9-47.4 18.2-7 51.1-8.9 70.6.9-8.9-27.4-34.7-47.4-65.1-47.4z" fill="#ffc500"></path><path d="m122.6 92c-2-2-4.1-3.6-6.6-4.7 8.1-5.3 10-13.2 8.8-19.2-1.7-8.9-10.3-17.3-23.8-17.6v-9.6h-25.8v9.7h-9v80.4h9v11.2h25.9v-11.1c10.2-.2 20-5.8 24.6-14.5 4.3-8.2 3.1-17.4-3.1-24.6zm-33.7 7.1h.4c4-.1 10.8-.2 12.9 1.7l.3.2c1.2.9 2 2.5 2 4.5 0 2.1-.8 4.1-2.1 5.1l-.3.3c-2 2-8.8 1.9-12.8 1.8-.1 0-.2 0-.3 0zm12.5-24.9c.1 2.4-.7 3.4-1.3 4-2.3 2.2-7.2 2.5-11.2 2.5v-11.9c5.8-.1 10.2.9 11.9 2.6.4.4.8 1.1.7 2.4v.2z" fill="#ffe500"></path><g id="圖層_2_00000088817577234573337530000011922961527176976806_"><path d="m120.4 92.9c-3.2-3.3-7.4-5.2-12.7-5.9v-.2c24.7-7.8 15.4-36.2-9.6-34.3v-9.7h-7.6v9.7h-4.7v-9.7h-7.6v9.7h-9v74.5h9v11.2h7.6v-11.2h4.7v11.2h7.6v-11.2c19.4 2 35.7-18.3 22.3-34.1zm-34.5-28c7.4-.5 19.5.1 18.5 8.2.3 10-11.2 9.8-18.5 9.5zm18.2 47.1c-3.6 3.6-13.1 2.6-18.2 2.7v-19.6c5.1.1 14.6-.9 18.3 2.5 4.5 3.2 4.2 11.2-.1 14.4z" fill="#c78c00"></path></g></svg>
              กดแชร์เพื่อรับเงินรางวัล
            </v-btn>
            <v-btn v-if="isDone == true" rounded color="primary" dark class="w-100 mt-10 my-btn" @click="next">รับรางวัล</v-btn>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </template>
  
  <script>
  export default {
    mounted(){
      liff.init({
        liffId: '1660755023-ywWIxxDL'
      }).then(() => {
        if(liff.isLoggedIn()){
          liff.getProfile().then(profile => {
            this.$store.dispatch('setLine', profile);
            this.$axios.get(`https://marketing-thai789-default-rtdb.asia-southeast1.firebasedatabase.app/members/${this.$store.getters.getLine.userId}/profile.json`).then((res) => {            
              if(res.data != null){
                this.$store.dispatch('setUser', res.data);
              }
            });
            this.$axios.get(`https://marketing-thai789-default-rtdb.asia-southeast1.firebasedatabase.app/rewards/${this.$store.getters.getLine.userId}.json`).then((res) => {            
              if(res.data != null){
                this.stamps = res.data
              }
            });
          })
        }else{
          liff.login();
        }
      })
    },
    computed: {
      getLine(){
        return this.$store.getters.getLine;
      },
      getUser(){
        return this.$store.getters.getUser;
      },
      isDone(){
        let isDone = true;
        this.stamps.forEach(ele => {
          if(ele.value === false){
            isDone = false;
            return isDone;
          }
        })
        return isDone;
      }
    },
    methods: {
      scan(){
        liff.scanCode().then(result => {
          this.stamps = this.stamps.map((obj) => {
            if(obj.name == result.value){
              obj.value = true;
            }
            return obj;
          })
          this.$axios.patch(`https://marketing-thai789-default-rtdb.asia-southeast1.firebasedatabase.app/rewards/${this.$store.getters.getLine.userId}.json`, {...this.stamps}).then((res) => {            
  
          }).catch(e => alert(e))
        }).catch(e => alert(e))
      },
      next(){
        this.$router.push('reward/done');
      }
    },
    data(){
      return {
        stamps: [
          {
            name: 'stamp1',
            value: false
          },
          {
            name: 'stamp2',
            value: false
          },
          {
            name: 'stamp3',
            value: false
          },
          {
            name: 'stamp4',
            value: false
          },
          {
            name: 'stamp5',
            value: false
          },
          {
            name: 'stamp6',
            value: false
          },
          {
            name: 'stamp7',
            value: false
          },
          {
            name: 'stamp8',
            value: false
          }     
        ]
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
    .name{
      margin-left: 20px;
      font-size: 20px;
    }
    .v-card__text{
      padding: 10px 15px;
    }
    .stamp-zone{
      background: #f0e9e9;
      padding: 25px 25px 0;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
    }
    .stamp{
      flex-basis: 25%;
    }
    .circle{
      background: #FFF;
      border-radius: 50%;
      border: 2px #ff7ea9 solid;
      height: 55px;
      width: 55px;    
      justify-content: center;
      display: inline-flex;
      margin-bottom: 25px;    
      .v-icon{
        display: none;
      }
      &.active{
        background: #050505;
        span{
          display: none;
        }
        .v-icon{
          display: flex;
          color: #FFF;
        }
      }
      &.end{
        background: #ff2ba0;
        span{
          font-size: 16px;        
          color: #FFF;
        }
      }
      span{
        align-self: center;
        font-size: 20px;
        color: #161616;
        font-weight: bold;
      }
    }
    .scan{
      svg{
        margin-right: 5px;
      }
    }
  </style>