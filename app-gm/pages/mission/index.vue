<template>
    <div>
      <v-app-bar color="primary" dense flat dark>
        <v-toolbar-title>ทำภารกิจ</v-toolbar-title>
      </v-app-bar>
      <v-container class="pt-0 pb-0">
        <v-row>
          <v-col cols="12">
            <div class="mt-3 text-primary text-title text-center">
              {{ list.date }}
            </div>
          </v-col>
          <v-col cols="12">
            <Card
              v-for="item in list.sessions"
              :session="item"
              :key="item.id"
              :active="selectedMission.includes(item.id)"
              v-on:moreDetail="moreDetail(item)"
              v-on:chooseMission="chooseMission(item)" />          
          </v-col>
          <v-col cols="12">
            <div class="set-padding">
              <v-btn
                rounded
                color="primary"
                dark
                class="w-100 mt-3 my-btn"
                @click="next"
                >ถัดไป</v-btn
              >
            </div>
            <div v-if="index > 0" class="w-100 mt-3 text-center my-btn text-primary" @click="back">Back</div>
          </v-col>
        </v-row>
        <v-dialog v-model="isShowDialog" max-width="290">
          <v-card class="dialog-card"> 
            <v-img
              class="white--text align-end"
              height="200px"
              :src="dialog.image"
            >
            </v-img>
            <v-card-title class="headline">{{ dialog.title }}</v-card-title>
            <v-card-text>
              <p>Time: {{ dialog.time }}</p>
              <p>Place: {{ dialog.place }}</p>
              <p class="detail">
                {{ dialog.detail }}
              </p>
              <p>
                Speaker: <br/>
                <span v-html="dialog.spakers"></span>              
              </p>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>            
              <v-btn class="text-primary" text @click="isShowDialog = false">
                OK
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-container>
    </div>
  </template>
  
  <script>
  import Card from '~/components/Card'
  export default {
    components: {
      Card
    },
    data(){
      return {
        isShowDialog: false,
        index: 0,
        dialog: {
          title: '',
          time: '',
          place: '',
          image: '',
          detail: '',
          spakers: ''
        },
        selectedMission: [],
        list: [],
        missions: this.$store.getters.getMission    
      }
    },
    mounted(){
      // api 
      this.list = this.missions[this.index]
    },
    methods: {
      back() {
        this.index = this.index-1
        this.list = this.missions[this.index]
      },
      next() {
        if(this.index == this.missions.length -1){
          // api save register mission 
          this.$axios.patch(`https://marketing-thai789-default-rtdb.asia-southeast1.firebasedatabase.app/line:0001.json`, { ...this.selectedMission }).then((res) => {
            this.$router.push('/mission/done')
          }).catch(e => console.log(e)) 
        }else{
          this.index = this.index+1
          this.list = this.missions[this.index]
        }      
      },
      moreDetail(item){
        this.isShowDialog = true
        this.dialog = item
      },
      chooseMission(item){
        const listId = this.list.sessions.map(session => session.id)
        this.selectedMission = this.selectedMission.filter(session => !listId.includes(session))
        this.selectedMission.push(item.id)
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
  .dialog-card{
    p{
      margin-bottom: 0;
    }
    .v-card__title.headline{
      font-size: 20px !important;
    }
    .v-card__text{
      padding-bottom: 0;
    }
    .detail{
      margin: 10px 0;
    }
  }
  </style>