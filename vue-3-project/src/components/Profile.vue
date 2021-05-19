<template>
<div class="user-profile">
    <div class="user-profile__user-panel">
        <hi class="user-profile__username"> @{{user.username}} - {{fullName}}</hi>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">
            Admin
        </div>
        <div class="user-profile__follower-count">
            <strong>followers: </strong>{{followers}}
        </div>
    </div>
    <div class="user-profile__tweets-wrapper">
        <TweetItem
         v-for="tweet in user.tweets" 
         :key="tweet.id"
         :username="user.username"
         :tweet="tweet" />    
     </div>
</div>
</template>
<script>
import TweetItem from "./TweetItem";

export default {
  name: 'Profile',
  components : {TweetItem},
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'tyjani3',
        firstName: "vevi",
        lastName: "tijani",
        email: "seun@gmail.com",
        isAdmin: true,
        tweets: [
            {
             id: 1, 
             content: ' Am enjoying the tutorials'
            },
            {
             id: 2,
             content:  ' you gonna love this show ' 
            }
        ]
      }
    }
  },
  // track followers or changes
  watch: {
  followers(oldFollowerCount, newFollowerCount) {
    if(newFollowerCount < oldFollowerCount) {
      console.log(`${this.user.username} is folloewed!`)
    }
  }
  },

  // gettin full name of user
  computed : {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  // function
  methods: {
    followUser() {
      this.followers++;
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style>
.user-profile{
 display: grid;
 grid-template-columns: 1fr 3fr;
 width: 100%;
 padding:50px 5%;
}

.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color:white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
}
.user-profile__admin-badge {
    background: rebeccapurple;
    color:white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

h1 {
    margin: 0;
}
</style>
