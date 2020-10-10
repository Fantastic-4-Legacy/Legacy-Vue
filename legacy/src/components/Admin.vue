<template>
  <div id="Admin">
    <div v-if="displayBann">
      <h1 id="ban">Admin Interface</h1>
      <div id="userBann">
        <h1 class="h1a">Banned Accounts</h1>
        <input
          type="username"
          placeholder="Username"
          v-model="username"
          required
        />
        <input type="text" placeholder="reason" v-model="reason" required />

        <input type="date" v-model="date" required /> <br />
        <button id="buttValid" @click="AxiosBann">Validate</button>
        <button id="getfeeds" @click="getFeedBack">See Feedbacks</button>
      </div>
      <div id="repo">
        <h1 id="repN">Reports</h1>

        <div class="reposes" v-for="({ to, report }, key) in dataR" :key="key">
          {{ to }} Said : {{ report }}
        </div>
      </div>
    </div>

    <div v-if="displayFeedback">
      <h1 id="feed" class="h1a">Users Feedbacks</h1>
      <button id="back" @click="handleBack">Back</button>
      <div id="feeds">
        <div>
          <div id="feedhold" v-for="ele in dataF" :key="ele.id">
            {{ ele.feedbacks }}
          </div>
          <br />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Admin",
  data() {
    return {
      username: "",
      reason: "",
      date: "",
      dataF: [],
      displayBann: true,
      displayFeedback: false,
      dataR: [],
    };
  },
  mounted() {
    axios({
      url: "/freports",
      method: "post",
    }).then((result) => {
      setTimeout(() => {
        this.dataR = result.data;
        console.log("this dataR   ====== ", this.dataR);
      }, 500);
    });
  },
  methods: {
    getFeedBack() {
      this.displayBann = false;
      this.displayFeedback = true;
      axios({
        url: "/Feeds",
        method: "GET",
      })
        .then((result) => {
          this.dataF = result.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    AxiosBann() {
      axios({
        url: "/banaccount",
        method: "post",
        data: {
          username: this.username,
          reason: this.reason,
          date: this.date,
        },
      });
    },
    handleBack() {
      this.displayBann = !this.displayBann;
      this.displayFeedback = !this.displayFeedback;
    },
  },
  // updated() {
  //   console.log("updated :", this.displayBann, this.displayFeedback);
  // },
};
</script>

<style>
#Admin {
  border: 3px solid black;
  width: 821px;
  position: relative;
  padding: 0px;
  padding-left: 55px;
  left: 208px;
  padding-top: 17px;
  top: 69px;
  height: 500px;
}
.h1a {
  color: white;
}
#ban {
  color: white;
  margin: -5px;
  position: relative;
  left: 273px;
}

#userBann {
  position: relative;
  width: 394px;
  margin-left: -45px;
  margin-top: 33px;
  top: 68px;
}

#repo {
  border: 1px solid black;
  width: 416px;
  height: 350px;
  position: relative;
  top: -224px;
  left: 376px;
  overflow-y: auto;
  overflow-x: hidden;
}

#repN {
  position: relative;
  left: 146px;
  top: -20px;
  color: white;
}
.reposes {
  border: 1px solid black;
  width: 361px;
  height: 43px;
  position: relative;
  left: 20px;
  border-radius: 4px;
  background-color: #eeeeee;
  margin-top: 11px;
}
.Xbutt {
  padding: 11px;

  color: red;
  background-color: white;
  position: absolute;
  left: 311px;
  top: 2px;
  background-color: red;
  color: white;
  padding: 14px 20px;
  margin: -2px 0px;
  border: inherit;
  cursor: pointer;
  width: 14%;
  opacity: 0.9;
  border-radius: 0px;
}

#feed {
  position: relative;
  left: 287px;
  top: -19px;
}

#back {
  position: relative;
  top: -74px;
  left: -47px;
  padding: 8px;
}

#feeds {
  border: 2px solid black;
  position: relative;
  left: -46px;
  top: -54px;
  width: 855px;
  height: 422px;
  overflow-y: scroll;
  overflow-x: visible;
}

#feedhold {
  border: 2px solid rgb(255, 255, 255);
  width: 807px;
  /* height: 59px; */
  position: relative;
  left: 25px;
  top: 15px;
  border-radius: 5px;
  background-color: white;
  color: black;
  text-align: center;
}
</style>>
