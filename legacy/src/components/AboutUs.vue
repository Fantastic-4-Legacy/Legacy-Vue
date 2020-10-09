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
    <h4 id="devName">
      <a id="namedevlop" href="https://github.com/Slim-Kasraoui"
        >*Mohamed Slim kasraoui*</a
      ><br />
      <a id="namedevlop" href="https://github.com/achref-bououn"
        >*Achref bouaoun*</a
      >
      
      <br />
       <a id="namedevlop" href="https://github.com/WalaNour">*Wala nour*</a>
      <br />
      <a id="namedevlop" href="https://github.com/malek-chebil"
        >*Malek Chebil*</a
      >
      <br />
     
    </h4>
    <h3 id="contact">FeedBack</h3>
    <input
      id="Fid"
      type="text"
      placeholder="send us a feedback or find support"
      required
      v-model="feedback"
    />
    <button @click="sendFB" id="feedback">send</button>
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

<style >
.aboutus {
  color:white;
  position: relative;
  top: 16px;
  left: 250px;
  background: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: "Montserrat", sans-serif;
  /* height: 65vh; */
  width: 790px;
  border: #f6f5f7;
  border-radius: 5%;
  border-style: solid;
  height: 544px;
  text-align:center;
}
#feedback {
  background-color: #ff2626;
  position: relative;
  top: -41px;
  left: -7px;
}
#Fid{
  position:relative;
  top:-35px;
  border-radius:5px;
}
#abs{
  position: relative;
    top: 18px;
}
#devName{
  color:gray;
}
#contact{
 position: relative;
  position: relative;
  top: -30px;
  left: 3px;
  list-style-type: circle;
    
}
</style>