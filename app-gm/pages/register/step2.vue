<template>
    <div>
        <v-app-bar color="primary" dense flat dark>
            <v-toolbar-title>สมัครสมาชิก</v-toolbar-title>
        </v-app-bar>

        <v-container class="pt-0 pb-0">
            <v-row>

                <v-col cols="12">
                    <div class="mt-8 text-primary text-title text-center">
                        Step 2 of 2
                    </div>
                </v-col>

                <v-col cols="12">
                    <v-form>
                        <p class="text-center text-main mb-0 mt-4">กรอกข้อมูลที่ถูกต้อง ให้ครบทุกช่อง</p>
                    
                        <v-text-field
                        v-model="form.email"
                        type="email"
                        dense      
                        :rules="emailRules"
                        label="Email"
                        ></v-text-field>
                        <v-text-field
                        v-model="form.phone"
                        dense
                        :rules="phoneRules"
                        @keypress="onlyNumber($event, 10)"
                        label="Phone"
                        ></v-text-field>
                        <v-dialog
                        ref="dialog"
                        v-model="modal"
                        persistent
                        width="290px"
                        ></v-dialog>
                        <p class="text-center text-main mb-0 mt-4">ใช้สำหรับทำภารกิจแชร์</p>
                        <v-text-field
                        v-model="form.facebook"
                        dense
                        label="ชื่อเฟสบุ๊ค"
                        ></v-text-field>
                        <v-text-field
                        v-model="form.linkfb"
                        dense
                        label="ลิงค์เฟสบุ๊ค"
                        ></v-text-field>
                        <v-btn rounded color="primary" dark class="w-100 mt-10 my-btn" @click="register">สมัครสมาชิก</v-btn>
                        <div class="w-100 text-center my-btn text-primary" @click="back">กลับ</div>
                      </v-form>
                    </v-col>
                  </v-row>
                </v-container>
              </div>
</template>


<script>
const REGEX_EMAIL = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
const REGEX_PHONE = /^[0]([0-9]{9})*$/
const REGEX_NUMBER = /^[0-9]*$/
export default {
  data(){
    return {
      form: {
        email: this.$store.getters.getRegister.email,
        phone: this.$store.getters.getRegister.phone,
        facebook: this.$store.getters.getRegister.facebook,
        linkfb: this.$store.getters.getRegister.linkfb
      },
      modal: false,
      emailValidated: false,
      phoneValidated: false,
      emailRules: [ value => this.emailValidator(value)],
      phoneRules: [ value => this.phoneValidator(value)]
    }
  },
  methods: {
    phoneValidator(value){    
      this.phoneValidated = false  
      if(value == ''){
        return 'required'
      }
      if(REGEX_PHONE.test(value) && value.length == 10){ 
        this.phoneValidated = true
        return true
      }
      return "กรุณากรอกเบอร์มือถือของท่าน"
    },
    emailValidator(value){
      this.emailValidated = false
      if(value == ''){
        return 'required'
      }
      if(REGEX_EMAIL.test(value)){
        this.emailValidated = true
        return true
      }
      return "กรุณากรอกอีเมล์ของท่าน"
    },
    onlyNumber(event, max){  
      if(event.target.value.length == 0){
        if(event.key != 0){
          return event.preventDefault()
        }
      }else{
        if(!REGEX_NUMBER.test(event.key) || event.target.value.length == max){
          return event.preventDefault()
        }
      }      
    }, 
    validate(){
      let validated = true
      const errors = []
      const validatorField = [
        'email',
        'phone',
        'facebook',
        'linkfb'
      ]
      validatorField.forEach((field) => {
        if(this.form[field] == ''){
          validated = false
          errors.push(`${field} can not be null`)
        }
      })    
      if(!this.emailValidated){
        validated = false
        errors.push(`email is Invalid`)
      }
      if(!this.phoneValidated){
        validated = false
        errors.push(`please input phone number`)
      }
      if(!validated){
        this.$store.dispatch('setDialog', {
          isShow: true,
          title: 'Form is error',
          message: errors.map((error) => error+'<br/>').join('')
        })        
      }      
      return validated
    },  
    back() {      
      this.$router.push('/register')
    },
    register() {
      if(this.validate()){
        this.$store.dispatch('setRegister', this.form)
        this.$axios.patch(`https://marketing-thai789-default-rtdb.asia-southeast1.firebasedatabase.app/members/${this.$store.getters.getLine.userId}/profile.json`, this.$store.getters.getRegister).then((res) => {
          this.$router.push('/register/done')
        }).catch(e => console.log(e))         
      }      
    }
  }
}
</script>

<style lang="scss" scoped>
  .v-form{
    padding: 0 10px;
  }
  .set-birthday{
    position: relative;
    ::v-deep .v-input__prepend-outer{
      position: absolute;
      right: 0
    }
  }
</style>