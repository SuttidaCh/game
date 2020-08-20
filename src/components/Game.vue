<template>
  <div >
    <p>HP Player {{random(1, 3)}}
        {{player[random(1, 3) - 1].name}}
        </p>+รูป
         <hr />
        name = {{aPlayer.name}}
        HP = {{aPlayer.hp}}
        img = {{aPlayer.img}}
        <hr />
    <p>HP Monster {{random(1,3)}}
        {{monster[random(1,3)-1].name}}</p>+รูป

        <hr />
        name = {{aMonster.name}}
        HP = {{aMonster.hp}}
        img = {{aMonster.img}}
        <hr />

     <button @click ="start()" class="btn btn-dark ml-2" >Start </button>
    <button  @click ="attack()" class="btn btn-dark ml-2" >Attack</button>
    <button  @click ="SpecialAttack()" class="btn btn-dark ml-2" >Special Attack</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
        aPlayer: { name: "" , hp: 0, imag: ''},
        // ชื่อ player[1].name  randomเอา
      player: [
        { name: "Anakin", hp: 90, imag: 'a' },
        { name: "Iron Man", hp: 150 ,imag: 'b'},
        { name: "Doraemon", hp: 200 ,imag: 'c' },
      ],
       aMonster: { name: "" , hp: 0, imag: ''},
      monster: [
        { name: "Thanons", hp: 300 ,imag: '' },
        { name: "Darth vader", hp: 20 ,imag: 'y' },
        { name: "Cell", hp: 20 ,imag: 'z' },
      ],
    };
  },
  methods: {
    random: function (min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },

    start:function(){
        //1.random player 1-3  ชื่อ hp รูป 
        this.aPlayer = this.player[this.random(1,3)-1 ]
        this.aMonster = this.monster[this.random(1,3)-1 ]
        //
        //
    },
    attack:function(){
        //1. player  >>> monster
        
        //2. player  <<< monster
        //3. player.HP <<<=0 =>>> ?
        //4. monster.HP <<<=0 =>>> ?
        //5. 
    },
  },
};
</script>

<style >
div{
     color: rgb(255, 255, 255);
}
</style>