<template>
  <div id="app">
    <div id="nav">
      <h1>{{appName}}</h1>
      <router-link to="/">Home</router-link> |
      <router-link v-if="authenticated" to="/myprofile">My profile</router-link>
      <router-link v-else to="/Login" class="s">My profile</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link v-if="authenticated" to="/Login" v-on:click.native="logout()" replace> Logout </router-link>
      <router-link v-else to="/Login" v-on:click.native="logout()" replace> Login </router-link>

    </div>
    <router-view @authenticated="setAuthenticated" />
      <p v-if="authenticated">logged in as: {{loggedInUser}}</p>
  </div>

</template>



<script>
import { mapState, mapActions } from 'vuex';


class Product {
  constructor(pid, name, owner, imgUrl, highestBid, highestBidder, timeout) {
    this.pid = pid;
    this.name = name;
    this.owner = owner;
    this.imgUrl = imgUrl;
    this.highestBid = highestBid;
    this.highestBidder = highestBidder;
    this.timeout = timeout;
  }
}

class User {
  constructor(uid, name, email, imgUrl, password) {
    this.uid = uid; //this.username = username;
    this.name = name;
    this.email = email;
    this.imgUrl = imgUrl;
    this.password = password;
  }
}



  export default {
    name: 'root',
    data () {
      return {
        appName: 'The Auction Application',
        authenticated: false,
        search:"",
        loggedInUser:"..",
        hiBidder: "",
        products: [
          new Product(
            '0',
            'Brukt Jakke',
            'frida',
            'https://images.finncdn.no/dynamic/960w/2018/9/vertical-5/20/5/129/691/465_136669269.jpg',
            '150',
            'emilia',
            "November 27, 2018"
          ),
          new Product(
            '1',
            'Smykke',
            'emilia',
            'https://www.gullfunn.no/content/images/thumbs/0003350_smykke-i-solv.jpeg',
            '250',
            'frida',
            "December 24, 2018"
          ),
          new Product(
            '2',
            'Stolen Child by AFK',
            'mikal',
            'https://www.kunstveggen.no/uploads/default/original/2X/4/4db8c760e3ae7161807809bb6cf51609d2b43628.jpg',
            '500',
            'frida',
            "November 30, 2018"
          )
        ],
        users: [
           new User(
            'emilia',
            'Emilia Botnen Van den Bergh',
            'ebvdb@hvl.no',
            'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/38043185_10155473704291373_4817665254009864192_n.jpg?_nc_cat=102&_nc_ht=scontent-arn2-1.xx&oh=87db07d966b1f4b4f06f78068ad25f2a&oe=5C6C41DF',
            'emilie'
          ),
          new User(
            'frida',
            'Frida Tryggestad Klockmann',
            'ftk@hvl.no',
            'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/29314875_10210157233919408_2013080888513921024_n.jpg?_nc_cat=110&_nc_ht=scontent-arn2-1.xx&oh=21e376d68b74dc5a36b663e01d9c9195&oe=5C80A7A1',
            'fride'
          ),
          new User(
            'mikal',
            'Mikal Fuglestein',
            'mikalErEnFugl@hvl.no',
            'https://scontent-arn2-1.xx.fbcdn.net/v/t1.0-9/60835_1451363597879_8100797_n.jpg?_nc_cat=106&_nc_ht=scontent-arn2-1.xx&oh=b7753d2d6a3bc83edb4dfa5e5d95e52d&oe=5C679D70',
            'mikkel'
          )
        ]
      }

    },
//    mounted() {}, første som skjer på siden
    computed: {
    ...mapState({
        alert: state => state.alert
      }),
      filteredList() {
        return this.products.filter(product => {
          return product.name.toLowerCase().includes(this.search.toLowerCase())
        })
      },
      theUser() {
        return this.users.filter(user => {
          return user.uid.toLowerCase().match(this.loggedInUser.toLowerCase())
        })
      }
    },
    methods: {
      setAuthenticated(status) {
          this.authenticated = status;
      },
      logout() {
        this.authenticated = false;
      }
    }
  };

</script>


<style>

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
#nav a.router-link-exact-active.s {
  color: #2c3e50;
}
</style>
