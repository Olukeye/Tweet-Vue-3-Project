<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ state.user.username }}</h1>
      <!-- <h2>{{ userId }}</h2> -->
      <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ state.followers }}
      </div>
      <TweetPanel @addTweet="addTweet"/>
    </div>
    <div class="user-profile__tweets-wrapper">
      <TweetItem
        v-for="tweet in state.user.tweets"
        :key="tweet.id"
        :username="state.user.username"
        :tweet="tweet"
      />
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";
import TweetItem from "./TweetItem";
import TweetPanel from "./TweetPanel";

export default {
  name: "Profile",
  components: { TweetPanel , TweetItem},
  setup() {
    const state = reactive({
      followers: 0,
      user: {
        id: 1,
        username: "tyjani3",
        firstName: "vevi",
        lastName: "tijani",
        email: "seun@gmail.com",
        isAdmin: true,
        tweets: [
          {
            id: 1,
            content: " Am enjoying the tutorials"
          },
          {
            id: 2,
            content: " you gonna love this show "
          }
        ]
      }
    })

    function addTweet(tweet) {
      state.user.tweets.unshift({
        id: state.user.tweets.length + 1,
        content: tweet
      }); 
    }
    return {
      state,
      addTweet
    }
  }
};
</script>

<style scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
h1 {
  margin: 0;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile__tweet-wrapper {
  display: grid;
  grid-gap: 10px;
}
</style>
