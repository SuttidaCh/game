<template>
  <div>
    <div class="row">
      <div class="col-6">
        <p>Player</p>
        {{aPlayer.name}}
        <br />
        <img  :src="hp1" height="40px" />
        HP {{aPlayer.hp}}
      </div>
      <div class="col-6">
        <p>Monster</p>
        {{aMonster.name}}
        <br />
        <img  :src="hp2" height="40px" />
        HP {{aMonster.hp}}
      </div>
    </div>
    <div class="row">
      <div class="col-5">
        <br />
        <div  style="position: absolute; z-index: 1;"><img  style="width:750px" :src="aura"></div>
        <div  style="position: absolute; z-index: 2;"><img style="width:50%" :src="aPlayer.img" /></div>
      </div>

      <div class="col-sm">
        <br />
          <div  v-if="aMonster.hp <=0 ">You Win <br><br />
             <img src="https://papuarza.github.io/project-game-pacman/img/monster-red.gif" width="60%"> 
          </div>
          <div v-else-if="aPlayer.hp <= 0 ">You Lose <br><br />
             <img src="https://papuarza.github.io/project-game-pacman/img/monster-yellow.gif" width="60%">
          </div>
        <br />
        <br />
        <br />
        <img src="img/vs.png" width="50%" />
      </div>
      <div class="col-5">
        <br />
        <div style="position: absolute; z-index: 3;"><img style="width:750px" :src="aura"></div>
       <div style="position: absolute; z-index: 4;"><img style="width:50%" :src="aMonster.img" /></div>
      </div>
    </div>
    <br />
    <br />
    <br />
    <br />
    <div class="d-flex justify-content-center">
      <div class="but">
        <div class="col">
          <button @click="start()" class="btn btn-light ml-2">Start</button>
          <button v-bind:disabled="end" @click="attack()" class="btn btn-light ml-2">Attack</button>
          <button v-bind:disabled="end" @click="specialattack()" class="btn btn-light ml-2">Special Attack</button>
          <button @click="reset()" class="btn btn-light ml-2">Reset</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      aura:"https://i.pinimg.com/originals/cd/14/68/cd1468741cb6d85d2b9d84b9ca6d1829.gif",
      win:"https://thumbs.gfycat.com/ContentNecessaryHorseshoebat-max-1mb.gif",
      playmax: "",
      monsmax: "",
      hp1:
        "https://thumbs.gfycat.com/MixedBiodegradableBluetonguelizard-size_restricted.gif",
      hp2:
        "https://thumbs.gfycat.com/MixedBiodegradableBluetonguelizard-size_restricted.gif",
      end: false,
      aPlayer: { name: "", hp:1, img: "", hp1: "" },
      // ชื่อ player[1].name  randomเอา
      player: [
        {
          name: "Hulk",
          hp: 370,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/9a145268-41e7-4aa6-93b1-564a57fd6f05/dcmdrj9-aa50fd90-e559-400e-bc3b-e71ef6c42bd8.png/v1/fill/w_1024,h_1304,strp/hulk_by_hz_designs_dcmdrj9-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0xMzA0IiwicGF0aCI6IlwvZlwvOWExNDUyNjgtNDFlNy00YWE2LTkzYjEtNTY0YTU3ZmQ2ZjA1XC9kY21kcmo5LWFhNTBmZDkwLWU1NTktNDAwZS1iYzNiLWU3MWVmNmM0MmJkOC5wbmciLCJ3aWR0aCI6Ijw9MTAyNCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19.qISYghbdZ3Bbd22A3i3t7r3957f8UZ0Igyj8vlTbsY4",
        },
        {
          name: "Iron Man",
          hp: 450,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/627fe721-846f-4f75-ac61-111ca00b27dd/dd5vz5r-a29da2d5-4039-410a-a362-6dc04290123a.png/v1/fill/w_1280,h_2009,strp/iron_man___avengers_end_game__render_1__by_alanmac95_dd5vz5r-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0yMDA5IiwicGF0aCI6IlwvZlwvNjI3ZmU3MjEtODQ2Zi00Zjc1LWFjNjEtMTExY2EwMGIyN2RkXC9kZDV2ejVyLWEyOWRhMmQ1LTQwMzktNDEwYS1hMzYyLTZkYzA0MjkwMTIzYS5wbmciLCJ3aWR0aCI6Ijw9MTI4MCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19.6eM_wtfFPFKCoovbNlAjkoP0JioBdwAKrjkg7tEltd0",
        },
        {
          name: "Antman",
          hp: 200,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/5b8d2b12-21e8-4931-8a6d-fb9ecdd60383/dcc5qj5-6d473056-8bbf-488d-b285-ef9f9803722a.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3sicGF0aCI6IlwvZlwvNWI4ZDJiMTItMjFlOC00OTMxLThhNmQtZmI5ZWNkZDYwMzgzXC9kY2M1cWo1LTZkNDczMDU2LThiYmYtNDg4ZC1iMjg1LWVmOWY5ODAzNzIyYS5wbmcifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6ZmlsZS5kb3dubG9hZCJdfQ.NjH9PWtUwnhQDSDR7aq0pxi3najiQxKwZOxTikb3VWQ",
        },
        {
          name: "Spiderman",
          hp: 310,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/bf71705b-0d8b-45c5-a07d-a62e1e85127d/dberjrc-0995759b-0bf1-4446-93c6-c38d0879d71d.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3sicGF0aCI6IlwvZlwvYmY3MTcwNWItMGQ4Yi00NWM1LWEwN2QtYTYyZTFlODUxMjdkXC9kYmVyanJjLTA5OTU3NTliLTBiZjEtNDQ0Ni05M2M2LWMzOGQwODc5ZDcxZC5wbmcifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6ZmlsZS5kb3dubG9hZCJdfQ.l7-nBOaH6WQhPOhhgpdbIgiQcZXWWCOTCT5hX_ZIiO4",
        },
        {
          name: "Captain Marvel",
          hp: 340,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/f359881d-6bb2-4391-aba6-779f7084edd4/dcu43e8-d127dc85-60e1-4467-bf64-8f5d15b42cf0.png/v1/fill/w_1280,h_2240,strp/captain_marvel___transparent_by_asthonx1_dcu43e8-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0yMjQwIiwicGF0aCI6IlwvZlwvZjM1OTg4MWQtNmJiMi00MzkxLWFiYTYtNzc5ZjcwODRlZGQ0XC9kY3U0M2U4LWQxMjdkYzg1LTYwZTEtNDQ2Ny1iZjY0LThmNWQxNWI0MmNmMC5wbmciLCJ3aWR0aCI6Ijw9MTI4MCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19.XtP-HwJQImnC2ThJx-dAzcFTbySur3_Tc-tTwgQT5Bg",
        },
      ],
      aMonster: { name: "", hp: 1, img: "", hp2: "" },
      monster: [
        {
          name: "Doctor Strange",
          hp: 460,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/9a145268-41e7-4aa6-93b1-564a57fd6f05/dcmdsic-b2d9387b-50d5-45f7-8879-db6881c3b313.png/v1/fill/w_1024,h_1222,strp/doctor_strange_by_hz_designs_dcmdsic-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0xMjIyIiwicGF0aCI6IlwvZlwvOWExNDUyNjgtNDFlNy00YWE2LTkzYjEtNTY0YTU3ZmQ2ZjA1XC9kY21kc2ljLWIyZDkzODdiLTUwZDUtNDVmNy04ODc5LWRiNjg4MWMzYjMxMy5wbmciLCJ3aWR0aCI6Ijw9MTAyNCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19.lnPCjjB12Uc2eQBNTQiX7_yZ7EzI8E-KvJ-TcAT4o18",
        },
        {
          name: "Captain America",
          hp: 350,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/9a145268-41e7-4aa6-93b1-564a57fd6f05/dcrcghw-961cdd71-218c-4be4-be33-df551ea0a0fd.png/v1/fill/w_1024,h_1563,strp/captain_america_by_hz_designs_dcrcghw-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0xNTYzIiwicGF0aCI6IlwvZlwvOWExNDUyNjgtNDFlNy00YWE2LTkzYjEtNTY0YTU3ZmQ2ZjA1XC9kY3JjZ2h3LTk2MWNkZDcxLTIxOGMtNGJlNC1iZTMzLWRmNTUxZWEwYTBmZC5wbmciLCJ3aWR0aCI6Ijw9MTAyNCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19._f9CeJH8w6gUoexoWjFA1iskkNtM9V648HWoawEugIg",
        },
        {
          name: "Rocket",
          hp: 300,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/bf71705b-0d8b-45c5-a07d-a62e1e85127d/dbfpfbj-566b57a8-641a-4198-9245-d24c13345f43.png/v1/fill/w_1024,h_1321,strp/rocket_by_cptcommunist_dbfpfbj-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0xMzIxIiwicGF0aCI6IlwvZlwvYmY3MTcwNWItMGQ4Yi00NWM1LWEwN2QtYTYyZTFlODUxMjdkXC9kYmZwZmJqLTU2NmI1N2E4LTY0MWEtNDE5OC05MjQ1LWQyNGMxMzM0NWY0My5wbmciLCJ3aWR0aCI6Ijw9MTAyNCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19.yzwYzpBZns31v07RhmNvcyTwyRZbhLs2bQgtb0VxPSY",
        },
        {
          name: "Black Widow",
          hp: 230,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/f359881d-6bb2-4391-aba6-779f7084edd4/d9yl3wa-8b6bf6bf-83fd-4d6a-9d6c-8c3a2742b53a.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3sicGF0aCI6IlwvZlwvZjM1OTg4MWQtNmJiMi00MzkxLWFiYTYtNzc5ZjcwODRlZGQ0XC9kOXlsM3dhLThiNmJmNmJmLTgzZmQtNGQ2YS05ZDZjLThjM2EyNzQyYjUzYS5wbmcifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6ZmlsZS5kb3dubG9hZCJdfQ.mHcA6T52C4z9-K4vHNT8kig-5yHM74G0Vhx30sGFBWc",
        },
        {
          name: "Gamora",
          hp: 200,
          img:
            "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/9a145268-41e7-4aa6-93b1-564a57fd6f05/dcmdsff-d769584e-ef4b-4a68-9c00-92cbf25d4d6b.png/v1/fill/w_1024,h_1125,strp/gamora_by_hz_designs_dcmdsff-fullview.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3siaGVpZ2h0IjoiPD0xMTI1IiwicGF0aCI6IlwvZlwvOWExNDUyNjgtNDFlNy00YWE2LTkzYjEtNTY0YTU3ZmQ2ZjA1XC9kY21kc2ZmLWQ3Njk1ODRlLWVmNGItNGE2OC05YzAwLTkyY2JmMjVkNGQ2Yi5wbmciLCJ3aWR0aCI6Ijw9MTAyNCJ9XV0sImF1ZCI6WyJ1cm46c2VydmljZTppbWFnZS5vcGVyYXRpb25zIl19.4OJ4WviMzQJnYNW0mudI4VhxS1MCzFX4aG9DTDvTZ5A",
        },
      ],
    };
  },
  methods: {
    random: function (min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },

    start: function () {
      //1.random player 1-3  ชื่อ hp รูป
      this.aPlayer = this.player[this.random(1, 5) - 1];
      this.aMonster = this.monster[this.random(1, 5) - 1];
      
    },
    attack: function () {
      this.playmax = Math.floor(Math.random() * 10 + 5);
      this.aPlayer.hp = this.aPlayer.hp - this.playmax;
      this.monsmax = Math.floor(Math.random() * 10 + 5);
      this.aMonster.hp = this.aMonster.hp - this.monsmax;
      if (this.aPlayer.hp <= 0) {
        this.aPlayer.hp <= 0;
        this.end = true;
      } else if (this.aMonster.hp <= 0) {
        this.aMonster.hp <= 0;
        this.end = true;
      }
    },
    specialattack: function () {
      this.playmax = Math.floor(Math.random() * 15 + 5);
      this.aPlayer.hp = this.aPlayer.hp - this.playmax;
      this.monsmax = Math.floor(Math.random() * 15 + 5);
      this.aMonster.hp = this.aMonster.hp - this.monsmax;
      if (this.aPlayer.hp <= 0) {
        this.aPlayer.hp = 0;
        this.end = true;
      } else if (this.aMonster.hp <= 0) {
        this.aMonster.hp = 0;
        this.end = true;
      }
    },
    reset: function () {
      window.location.reload();
    },
  },
};
</script>

<style >
div {
  font-size: 35px;
  color: rgb(180, 30, 30);
  margin: 0;
  padding: 0;
}
.but {
  position: fixed;
  bottom: 25px;
}

</style>