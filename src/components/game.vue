<template>
<div>
    <img :src="enemy[0].srcservant" 
          style="width:450px; 
          position: absolute; top: 10%; right: 29%;"  >
    <img :src="enemy[0].src" 
          style="width:400px; 
          position: absolute; top: 5%; right: 10%;"  >
    <img :src="player[0].srcservant" 
          style="width:550px; 
          position: absolute; top: 37%; left: 20%;" >
    <img :src="player[0].src"   
          style="width:300px; 
          position: absolute; top: 50%; left: 10%;" >
    
    <div style="position: absolute; 
                border-radius: 10px; top: 5%; left: 5%;
                width: 40%; height: 15%; 
                background: #F8F8D8; 
                border: 10px solid #FF0000;"> 

        <p style="margin-top:20px;">{{enemy[0].name}}</p>
        <div class="progress">
            <div class="progress-bar progress-bar-striped progress-bar-animated bg-danger" 
                 role="progressbar" aria-valuenow="{{enemy[0].hp}}" aria-valuemin="0" aria-valuemax="150" 
                 v-bind:style="enemyHpBar">{{enemy[0].hp}}</div>
        </div>
    </div>

    <div style="position: absolute; 
                border-radius: 10px; bottom:20%; right: 0%;
                width: 40%; height: 15%;                 
                background: #F8F8D8; 
                border: 10px solid #00FF00;">

        <p style="margin-top:20px;">{{player[0].name}}</p>
        <div class="progress">
            <div class="progress-bar progress-bar-striped progress-bar-animated bg-success" 
                 role="progressbar" aria-valuenow="{{player[0].hp}}" aria-valuemin="0" aria-valuemax="200" 
                 v-bind:style="playerHpBar">{{player[0].hp}}</div>
        </div>
    </div>

    <div style=" position: absolute; 
                 width: 100%; bottom: 0%; height: 20%; 
                 background: #FFD700; border: solid 6px #8A2BE2;}">

        <div style="position: absolute; width: 50%; left: 0%; height: 95%;">
            <div>
                <p style="color: #000000; margin-top:9%">{{OrderServant}}</p>
            </div>
        </div>
        <div v-if="optionsOn" style=" position: absolute; width: 40%; top: 1%; right: 0%; height: 98%; background: #F8F8F8; border: solid 6px #000000;">
            <button @click="useOption(1)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Order</button>
            <button @click="useOption(2)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Servant</button>
            <button @click="useOption(3)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Command Spell</button>
            <button @click="useOption(4)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Run</button>
        </div>
        <div v-if="fightOn" style=" position: absolute; width: 40%; top: 0%; right: 0%; height: 98%; background: #F8F8F8; border: solid 6px #6F677F;">
            <button @click="useAttackOption(1)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Normal Attack</button>
            <button @click="useAttackOption(2)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Gae Bol</button>
            <button @click="useAttackOption(3)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Mana Burst</button>
            <button @click="useAttackOption(4)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Lord of Camelot</button>
        </div>
        <div v-if="endOn" style=" position: absolute; width: 40%; top: 0%; right: 0%; height: 98%; background: #F8F8F8; border: solid 6px #6F677F;">
            <button @click="processEnd(1)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">Yes</button>
            <button @click="processEnd(2)" style="width:50%; height:50%; border: solid 1px #FFFFFF;" class="btn btn-primary">No</button>
        </div>
    </div>
</div>
</template>

<script>
export default {
    data: function () {
        return {
            player: [{
                name: "Mash-Alter",
                hp: 200,
                srcservant: require("../assets/mash.png"),
                src: require("../assets/emiya.png"),
            }, ],

            enemy: [{
                name: "Altria-Pendragon",
                hp: 150,
                srcservant: require("../assets/saber.png"),
                src: require("../assets/kiri.png"),
            }, ],


            OrderServant: "Order your servant.",
            playerAttackDamage: [15, 30, 40, 55],
            enemyAttack: ["Normal Attack", "Mana Brust", "Excaliber", "Excaliber Morgan"],
            enemyAttackDamage: [15, 40, 50, 60],
            fightOn: false,
            endOn: false,
            optionsOn: true,

            playerHpBar: {
                width: "200%"
            },
            enemyHpBar: {
                width: "150%"
            },
            enemyFill: 150,
            playerFill: 200,
        };

    },
    methods: {
        useOption: function (option) {
            switch (option) {
                case 1:
                    //handle fight
                    this.optionsOn = false;
                    this.fightOn = true;
                    break;
                case 2:
                    //handle servant
                    setTimeout(() => {
                        this.OrderServant = "Order your servant.";
                    }, 2000);

                    this.OrderServant = "No more servant!";

                    break;
                case 3:
                    //handle item
                    setTimeout(() => {
                        this.OrderServant = "Order your servant.";
                    }, 2000);
                    this.OrderServant = "No Command Spell.";
                    break;
                case 4:
                    //handle run
                    setTimeout(() => {
                        this.OrderServant = "Order your servant.";
                    }, 2000);
                    this.OrderServant = "Can't escape.";
                    break;
            }
        },
        useAttackOption: function (attack) {
            switch (attack) {
                case 1:
                    //handle Attack 1
                    this.enemy[0].hp -= this.playerAttackDamage[0];
                    this.enemyFill -= this.playerAttackDamage[0];
                    this.enemyHpBar.width = this.enemyFill + "%"
                    //edit if HP !== 0
                    if (this.enemy[0].hp <= 0) {
                        this.OrderServant = "Altia-Pendragon fainted! Play again?";
                        this.endOn = true;
                        this.fightOn = false;
                        this.optionsOn = false;
                    } else {
                        setTimeout(() => {
                            this.processenemyAttack();
                        }, 2000);

                        this.OrderServant = "Mash-Alter used " + this.fightOptions[attack - 1] + "!";

                        //call enemy attack function
                        setTimeout(() => {
                            if (this.player[0].hp > 0) {
                                setTimeout(() => {
                                    this.OrderServant = "Order your servant.";
                                }, 2000);
                            }
                        }, 2000);
                    }
                    break;
                case 2:
                    //handle Attack 2
                    this.enemy[0].hp -= this.playerAttackDamage[1];
                    this.enemyFill -= this.playerAttackDamage[1];
                    this.enemyHpBar.width = this.enemyFill + "%"
                    //edit if HP !== 0
                    if (this.enemy[0].hp <= 0) {
                        this.OrderServant = "Altia-Pendragon fainted! Play again?";
                        this.endOn = true;
                        this.fightOn = false;
                        this.optionsOn = false;
                    } else {
                        setTimeout(() => {
                            this.processenemyAttack();
                        }, 2000);

                        this.OrderServant = "Mash-Alter used " + this.fightOptions[attack - 1] + "!";
                        //call enemy attack function
                        setTimeout(() => {
                            if (this.player[0].hp > 0) {
                                setTimeout(() => {
                                    this.OrderServant = "Order your servant.";
                                }, 2000);
                            }
                        }, 2000);
                    }
                    break;
                case 3:
                    //handle Attack 3
                    this.enemy[0].hp -= this.playerAttackDamage[2];
                    this.enemyFill -= this.playerAttackDamage[2];
                    this.enemyHpBar.width = this.enemyFill + "%"
                    //edit if HP !== 0
                    if (this.enemy[0].hp <= 0) {
                        this.OrderServant = "Altia-Pendragon fainted! Play again?";
                        this.endOn = true;
                        this.fightOn = false;
                        this.optionsOn = false;
                    } else {
                        setTimeout(() => {
                            this.processenemyAttack();
                        }, 2000);

                        this.OrderServant = "Mash-Alter used " + this.fightOptions[attack - 1] + "!";
                        //call enemy attack function
                        setTimeout(() => {
                            if (this.player[0].hp > 0) {
                                setTimeout(() => {
                                    this.OrderServant = "Order your servant.";
                                }, 2000);
                            }
                        }, 2000);
                    }
                    break;
                case 4:
                    //handle Attack 4
                    this.enemy[0].hp -= this.playerAttackDamage[3];
                    this.enemyFill -= this.playerAttackDamage[3];
                    this.enemyHpBar.width = this.enemyFill + "%"
                    //edit if HP !== 0
                    if (this.enemy[0].hp <= 0) {
                        this.OrderServant = "Altia-Pendragon fainted! Play again?";
                        this.endOn = true;
                        this.fightOn = false;
                        this.optionsOn = false;
                    } else {
                        setTimeout(() => {
                            this.processenemyAttack();
                        }, 2000);

                        this.OrderServant = "Mash-Alter used " + this.fightOptions[attack - 1] + "!";
                        //call enemy attack function
                        setTimeout(() => {
                            if (this.player[0].hp > 0) {
                                setTimeout(() => {
                                    this.OrderServant = "Order your servant.";
                                }, 2000);
                            }
                        }, 2000);
                    }
                    break;
            }
        },
        processenemyAttack: function () {
            //generate random number
            var random = Math.floor((Math.random() * 4) + 1);
            //do damage to player
            this.player[0].hp -= this.enemyAttackDamage[random - 1];
            this.playerFill -= this.enemyAttackDamage[random - 1];
            this.playerHpBar.width = this.playerFill + "%"
            if (this.player[0].hp <= 0) {
                this.OrderServant = "Mash-Alter fainted! Play again?";
                this.endOn = true;
                this.fightOn = false;
                this.optionsOn = false;
            } else if (this.player[0].hp > 0) {
                //continue battle
                this.OrderServant = "Altria-Pendragon used " + this.enemyAttack[random - 1] + "!";
                this.fightOn = false;
                this.optionsOn = true;
            }
        },
        processEnd: function (optionEnd) {
            switch (optionEnd) {
                case 1:
                    this.resetBattle()
                    break;
            }
        },
        resetBattle: function () {
            //reset data to start new game
            this.endOn = false;
            this.fightOn = false;
            this.optionsOn = true;
            this.OrderServant = "Order your servant."
            this.enemyHP = 150
            this.playerFill = 200
            this.enemyFill = 150
            this.playerHpBar.width = "200%"
            this.enemyHpBar.width = "150%"
            this.enemy[0].hp = 150
            this.player[0].hp = 200
        }
    }
};
</script>

<style>
body {
    background-image: url("https://thumbs.gfycat.com/AggressiveBonyFlatfish-max-1mb.gif");
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: 100%;
}
</style>
