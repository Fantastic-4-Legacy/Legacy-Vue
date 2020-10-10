<template>
  <div class="aboutus">
    <h2 id="abs">About Us</h2>
    <h3>
      Our product is basically a social media application but it looks a better
      way different than other social media applications
    </h3>
    <h4>what are Mary-j Tokens ?</h4>
    <p>
      Mary-J tokens are usefull to allow users to buy real e-cards like PayPal
      card we appreciate your time spent on connecting to our application, for
      this reason we allow users to gain 5 tokens per 10 minutes
    </p>
    <h2>development team:</h2>
    <div id="devName">
      <a id="namedevlop" href="https://github.com/achref-bououn"
        >*Achref bouaoun*</a
      >
      <br />
      <a id="namedevlop" href="https://github.com/Slim-Kasraoui"
        >*Slim kasraoui*</a
      >
      <br />
      <a id="namedevlop" href="https://github.com/malek-chebil"
        >*Malek Chebil*</a
      >
      <br />
      <a id="namedevlop" href="https://github.com/WalaNour">*Wala nour*</a>
      <br />
    </div>
    <div id="contactDiv">
      <h2 id="contact">FeedBack</h2>
      <input
        id="Fid"
        type="text"
        placeholder="send us a feedback or find support"
        required
        v-model="feedback"
      />
      <button @click="sendFB" id="feedback">send</button>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import Toast from "light-toast";
export default {
  name: "AboutUs",
  data() {
    return {
      feedback: "",
    };
  },
  methods: {
    sendFB() {
      let data = {
        feedback: this.feedback,
      };
      axios.post("/feedbacks", data).catch((err) => console.log(err));
      Toast.success("Thank for the Feedback", 1500, () => {
        location.reload();
      });
    },
  },
};
</script>
<style>
.aboutus {
  color: white;
  position: relative;
  left: 250px;
  margin: 5%;
  background: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: "Montserrat", sans-serif;
  width: 755px;
  border: #f6f5f7;
  border-radius: 5%;
  border-style: solid;
  text-align: center;
}
#contactDiv {
  height: 10rem;
  width: 80%;
  padding: 5%;
  margin: 5% 0;
}
#feedback {
  background-color: #ff2626;
  padding: 1.5% 5%;
  margin: 3%;
}
#feedback:hover {
  cursor: pointer;
}
#Fid {
  border-radius: 5px;
  height: 33px;
  width: 100%;
}
#abs {
  position: relative;
  top: 10px;
  left: -7px;
}
#devName {
  color: gray;
}
#text {
  text-align: center;
}
#team {
  position: relative;
  left: -2px;
  top: 0px;
}
#namedevlop{
  color: #f6f5f7;
}

</style>
