<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
        <h1 class="user-profile__username"> @{{user.username}} - {{fullName}} </h1>
    <div class="user-profile__admin-badge" v-if="user.isAdmin"> Admin </div>
    <div class="user-profile__admin-badge" v-else> Not Admin </div>
    <div class="user-profile__follower-count">
    <strong>Followers: </strong> {{followers}}
    <button @click="followUser()"> Follow </button>
  </div>
  <form class="user-profile__create-wittie">
      <label for="newWittie"><strong>New Wittie</strong></label>
      <textarea id="newWittie" row="4/">

      <div class="user-profile__create-wittie-type"<
          <label for="newWittieType"><strong>Type: </strong></label>
          <select id="newTwootType">
              <option :value="option.value" v-for="(option, index) in wittieTypes" :key="index">
                  {{ option.name }}
              </option>
          </select>
        </div>
      </form>
  </div>
  <div class="user-profile_wittlers-wrapper">
     <WittiesItem 
        v-for="wittie in user.witties" :key="wittie.id" 
        :username="user.username" 
        :wittie="wittie" @favourite="toggleFavourite"
        />
      </div>
  </div>
</template>

<script>
export default {
  name: "UserProfile", 
  data() {
    return {
        wittieTypes: [
            { value: "draft", name: "Draft"},
            { value: "instant", name: "Instant Witie"}
        ],
      followers: 0,
      user: {
        id: 1,
        username: "MarilynMonroe",
        firstName: "Marilyn",
        lastName: "Monroe",
        email: "marilyn.monroe@stars.com",
        isAdmin: true,
        witties: [
            {id: 1, content: "Wittler is amazing"},
            {id: 2, content: "Love thy rabbits"}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newfollowerCount){
        console.log(this.user.username + "has gained a follower!");
      }
    }
  },
  computed: {
    fullName(){ 
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id){
        console.log(`Favourited Wittie #${id}}`);
    }
  },
  mounted(){
    this.followUser();
  }
};
</script>

<style>
.user-profile{
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
    border: 2px solid #DFE3E8;
}
.user-profile__admin-badge{
    background: rgb(31, 116, 228);
    color: whitesmoke;
    border-radius: 10px;
    margin-right: auto;
    margin-left: auto;
    margin-top: 1em;
    margin-bottom: 1em;
    padding: 0 20px;
    font-weight: bold;
    text-align: center;
}

h1{
    margin: 0;
}

.user-profile__create-wittie {
    display: flex;
    flex-direction: column;
    border-top: 1px solid black;
    padding-top: 20px; 
}
</style>
