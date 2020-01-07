<template>
  <div class="container">
    <hr>
    <div class="row">
      <div class="col-sm-12">
        <!--<textarea class="form-control" rows="10" readonly="" v-model="messages.join('\n')"></textarea>-->
        <li v-for=" message in messages" v-bind:key="message">
          {{message}}
        </li>
        <hr>
        <input type="text" class="form-control" v-model="textMessage" @keyup.enter="sendMessage">
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import Echo from 'laravel-echo'

window.io = require('socket.io-client')

// window.Echo = new Echo({
//   broadcaster: 'socket.io',
//   host: 'http://46.180.63.44:6001'
// })

// async function jsDlyaPidorov () {
//   await axios.post('http://46.180.63.44:8080/api/login', { email: '11quarasique@gmail.com', password: 'qwertyui' }.then(r => { localStorage.setItem('token', r.data.success.token) }))
//   window.Echo = new Echo({
//     broadcaster: 'socket.io',
//     host: window.location.hostname + ':6001',
//     auth: {
//       headers: {
//         Authorization: 'Bearer ' + localStorage.getItem('token')
//       }
//     }
//   })
// }
//
// jsDlyaPidorov()

window.Echo = new Echo({
  broadcaster: 'socket.io',
  host: window.location.hostname + ':6001',
  auth: {
    headers: {
      Authorization: 'Bearer ' + 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIxIiwianRpIjoiZmRjMDk3OWZiODg2MjRkNTRlYzEyMDhjYzE2NTJlYWJiNzkyZTBkM2VmMTkxNDJkMTU4OWYwOTZlNjg2ZDY3YzdlYjhhMGUwYzdlZjM0ZTAiLCJpYXQiOjE1Nzg0MTYyNDAsIm5iZiI6MTU3ODQxNjI0MCwiZXhwIjoxNjEwMDM4NjQwLCJzdWIiOiI5Iiwic2NvcGVzIjpbXX0.cgKQYvTId3kaxAizd7lTPN8Moqiy2I-S9n8JtJYwQqxodECVQaz-WC7-Hj_qgAqlRzQK47dVR8kjQqq_jwAVOl8Er-CGYLgxNLpgfuaJ3H7QQLyhty7YRkcr996qNABhOBDx-OWaOFWeQ9w6NbpLSplkfCOFurxF7yJuBrtgVMadJ_y3o-1mGz7jQZApuuXTrUcXW7LLadLBc5w1GfznnGRMp51dyQ16-eAIiDEE5XsaHjZT40rqKeY9epfQEDT_uAa42RjAhrGayi4KLriLQfz50qH2JWmvAh0JLvUK4y3vrIgW7-xq3Rmt_qk0E3Klknbf16S_c9EhZCrXrutW_5eSKsAyeCRRZ6W3CQTv1cW7-dw_DzQfvaWmREhC5da1HoirRecrv5abeRqHYywBh1-0L9vNpz4bbW_FOaudDGEAfhdW_7MePeHsUvyjp8yUJq34f8JSxFazLRSyWIUYaYPYoqUJ4zI51hwFZpXoPYCbl50USCUhNy3q5uUH47amQLI_uy3F4-BNkiv8eJywnWnk65PGdpgWCb17zRHzwG2y_wlW1mF2KaSgyZ8ICW6hXfclB7C_pFhiB613TKpNqP1RcbnqP0a83TSfMAdtB_Jp_mZkribOvHdTX4bxF6I00dY-Vi6dhRg9dO7xHQjzbkXV5ptaeKz4zfKaXqufEbo'
    }
  }
})

// window.Echo = new Echo({
//   authEndpoint: 'http://46.180.63.44:6001/broadcasting/auth',
//   broadcaster: 'socket.io',
//   key: 'anyKey',
//   wsHost: window.location.hostname,
//   wsPort: 6001,
//   disableStats: true
// })

export default {
  data () {
    return {
      messages: ['123', '124'],
      textMessage: '',
      userName: 'Rabotaet'
    }
  },
  mounted () {
    window.Echo.private('chat')
      .listen('Message', ({ message }) => {
        this.messages.push(message)
      })
  },
  methods: {
    sendMessage () {
      axios.post('http://46.180.63.44:8080/api/messages', { body: this.userName + ': ' + this.textMessage })
      this.textMessage = ''
    }
  }
}
</script>
