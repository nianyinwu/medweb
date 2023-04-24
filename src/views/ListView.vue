<template>
  <v-container fluid class="search-list-page">
    <v-row>
      <v-col align="center" justify="center">
        <v-card class="mx-1 mb-1" color="rgb(224, 224, 224, 0.2)">
          <v-card-title class="pa-6 pb-0">
            <h3>
              急救車點班情況
            </h3>
          </v-card-title>
          <v-card-text class="pa-6 pt-0">
              <br>
              <v-date-picker
                v-model="record_Date"
                locale="zh-tw"
                color="#444444"
                header-color="#888888"
              ></v-date-picker>
              <br>
              <br>
              <v-btn 
                type="primary"
                color="secondary"
                @click="day">
                  白班
              </v-btn>
              &nbsp;
              <v-btn 
                type="primary"
                color="secondary"
                @click="mid">
                 小夜班
              </v-btn>
              &nbsp;
              <v-btn 
                type="primary"
                color="secondary"
                @click="night">
                  大夜班
              </v-btn>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
      user: {
        uid: '',
        uname: '',
        pNo: '',
      },
      record_Date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
      record_Time:'',
    };
    },
    created(){
      this.user.uid=this.$route.query.uid;
      this.user.uname=this.$route.query.uname;
      this.user.pNo=this.$route.query.pNo;
    },
    methods: {
      day() {
        var that = this;
          that.record_Time='白班'
          that.axios.get('/shift', {
            params:{
              record_Date: that.record_Date,
              record_Time: that.record_Time,
            }
          }).then(function(res){
            if(res.data.status==200){
                that.$router.push({
                  path: '/search',
                  query:{
                    uid: that.user.uid,
                    uname: that.user.uname,
                    pNo: that.user.pNo,
                    record_Date: that.record_Date,
                    record_Time: that.record_Time,
                  }
                })
            }
            else{
              alert('查無資料',{
              confirmButtonText: '確定',
              // callback: action => {
              //   that.user.uid='',
              //   that.user.uname='',
              //   that.user.pNo='',
              //   that.record_Date='',
              //   that.record_Time=''
              // }
            });
            }
          }).catch(err=>{
            alert(err);
          })
      },
      mid() {
        var that = this;
          that.record_Time='小夜班'
          that.axios.get('/shift', {
            params:{
              record_Date: that.record_Date,
              record_Time: that.record_Time,
            }
          }).then(function(res){
            if(res.data.status==200){
                that.$router.push({
                  path: '/search',
                  query:{
                    uid: that.user.uid,
                    uname: that.user.uname,
                    pNo: that.user.pNo,
                    record_Date: that.record_Date,
                    record_Time: that.record_Time,
                  }
                })
            }
            else{
              alert('查無資料',{
              confirmButtonText: '確定',
            });
            }
          }).catch(err=>{
            alert(err);
          })
      },
      night() {
        var that = this;
          that.record_Time='大夜班'
          that.axios.get('/shift', {
            params:{
              record_Date: that.record_Date,
              record_Time: that.record_Time,
            }
          }).then(function(res){
            if(res.data.status==200){
                that.$router.push({
                  path: '/search',
                  query:{
                    uid: that.user.uid,
                    uname: that.user.uname,
                    pNo: that.user.pNo,
                    record_Date: that.record_Date,
                    record_Time: that.record_Time,
                  }
                })
            }
            else{
              alert('查無資料',{
              confirmButtonText: '確定',
            });
            }
          }).catch(err=>{
            alert(err);
          })
      },
    },
  }
</script>