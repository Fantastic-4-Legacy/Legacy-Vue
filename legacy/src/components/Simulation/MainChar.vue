<template>
  <img
    class="avatar-img"
    :src="currentP"
    v-on:keyup="moveView"
    :tabIndex="0"
    :style="{ position: 'absolute', top: Xx + 'px', left: Yy + 'px' }"
  />
</template>
<script>
import axios from "axios";
export default {
  name: "Maincharacter",
  data() {
    return {
      character: 0,
      Id: 0,
      name: "",
      Fd: 0,
      Fu: 0,
      Fl: 0,
      Fr: 0,
      positionX: 0,
      positionY: 0,
    };
  },
  props: ["skin", "id", "MainP"],
  computed: {
    currentP: function () {
      return "/images/chars/" + this.skin + "/FD/fd0.png";
    },
    Xx: function () {
      return this.positionX;
    },
    Yy: function () {
      return this.positionY;
    },
    face: function () {
      return [
        {
          D0: `../../../public/images/chars/${this.skin}/FD/fd0.png`,
          D1: `../../../public/images/chars/${this.skin}/FD/fd1.png`,
          D2: `../../../public/images/chars/${this.skin}/FD/fd2.png`,
          R0: `../../../public/images/chars/${this.skin}/FR/fr0.png`,
          R1: `../../../public/images/chars/${this.skin}/FR/fr1.png`,
          R2: `../../../public/images/chars/${this.skin}/FR/fr2.png`,
          L0: `../../../public/images/chars/${this.skin}/FL/fl0.png`,
          L1: `../../../public/images/chars/${this.skin}/FL/fl1.png`,
          L2: `../../../public/images/chars/${this.skin}/FL/fl2.png`,
          u0: `../../../public/images/chars/${this.skin}/FU/fu0.png`,
          u1: `../../../public/images/chars/${this.skin}/FU/fu1.png`,
          u2: `../../../public/images/chars/${this.skin}/FU/fu2.png`,
        },
      ];
    },
  },
  mounted() {
    // this.currentP();
    // console.log('this skin =====', this.skin)
    // this.positionX();
    // this.positionY();
    setTimeout(() => {
      this.positionX = this.MainP.x * 10 + 130;
      this.positionY = this.MainP.y * 10 + 100;
      this.Id = this.id;
      this.character = this.skin;
    }, 1500);
    // console.log("this.positionX ===", this.positionX);
    // console.log("this.positionY ===", this.positionY);
  },
  methods: {
    moveView: function (event) {
      var x = event.keyCode;
      // console.log('keycode ===>', x)
      var face = "";
      if (x === 87) {
        if (this.positionX <= 390 && this.positionX > 130) {
          this.Fu++;
          if (this.Fu % 3 === 0) {
            face = this.face[0]["u2"];
            this.currentP = this.face[0]["u2"];
          } else if (this.Fu % 2 === 0) {
            face = this.face[0]["u1"];
            this.currentP = this.face[0]["u1"];
          } else {
            face = this.face[0]["u0"];
            this.currentP = this.face[0]["u0"];
          }
          this.positionX = this.positionX - 10;
          axios({
            method: "post",
            url: "/position",
            data: {
              positionX: this.positionX - 10,
              positionY: this.positionY,
              name: this.name,
              id: this.Id,
              Face: "top",
              skin: this.skin,
              face: face,
            },
          }).then((data) => {
            if (data.data.move) {
              console.log(data.data.move);
            }
          });
        }
      }
      if (x === 65) {
        if (this.positionY <= 390 && this.positionY > 100) {
          this.Fl++;
          if (this.Fl % 3 === 0) {
            face = this.face[0]["L2"];
            this.currentP = this.face[0]["L2"];
          }
        } else if (this.Fl % 2 === 0) {
          face = this.face[0]["L1"];
          this.currentP = this.face[0]["L1"];
        } else {
          face = this.face[0]["L0"];
          this.currentP = this.face[0]["L0"];
        }
        this.positionY = this.positionY - 10;
        axios({
          method: "post",
          url: "/position",
          data: {
            positionX: this.positionX,
            positionY: this.positionY - 10,
            name: this.name,
            id: this.Id,
            Face: "left",
            skin: this.skin,
            face: face,
          },
        }).then((data) => {
          if (data.data.move) {
            console.log(data.data.move);
          }
        });
      }
      if (x === 68) {
        if (this.positionY < 390 && this.positionY >= 0) {
          this.Fr++;
          if (this.Fr % 3 === 0) {
            face = this.face[0]["R2"];
            this.currentP = this.face[0]["R2"];
          } else if (this.Fr % 2 === 0) {
            face = this.face[0]["R1"];
            this.currentP = this.face[0]["R1"];
          } else {
            face = this.face[0]["R0"];
            this.currentP = this.face[0]["R0"];
          }
          this.positionY = this.positionY + 10;
          axios({
            method: "post",
            url: "/position",
            data: {
              positionX: this.positionX,
              positionY: this.positionY + 10,
              name: this.name,
              id: this.Id,
              Face: "right",
              skin: this.skin,
              face: face,
            },
          }).then((data) => {
            if (data.data.move) {
              console.log(data.data.move);
            }
          });
        }
      }
      if (x === 83) {
        if (this.positionY >= 130 && this.positionX < 390) {
          this.Fd++;
          if (this.Fd % 3 === 0) {
            face = this.face[0]["D2"];
            this.currentP = this.face[0]["D2"];
          } else if (this.Fd % 2 === 0) {
            face = this.face[0]["D1"];
            this.currentP = this.face[0]["D1"];
          } else {
            face = this.face[0]["D0"];
            this.currentP = this.face[0]["D0"];
          }
          this.positionX = this.positionX + 10;
          axios({
            method: "post",
            url: "/position",
            data: {
              positionX: this.positionX + 10,
              positionY: this.positionY,
              name: this.name,
              id: this.Id,
              Face: "Down",
              skin: this.skin,
              face: face,
            },
          }).then((data) => {
            if (data.data.move) {
              console.log(data.data.move);
            }
          });
        }
      }
      setTimeout(() => {
        this.$emit("UnmountP", this.positionX, this.positionY);
      }, 100);
    },
  },
};
</script>

<style scoped>
/* .avatar-img {
  position: absolute;
} */
</style>
