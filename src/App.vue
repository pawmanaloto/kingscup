<template>
  <div id="app">
    <header>
      <span>Vue.js PWA</span>
    </header>
    <main>
      <img @click="showNewCard" :src="img" alt="Vue.js PWA">
      <h1>{{cardTitle}}</h1>
      <div class="card-description">
        <p>{{description}}</p>
      </div>
    </main>
  </div>
</template>

<script>
import Hello from './components/Hello'
import data from './cards.json'

export default {
  name: 'app',
  components: {
    Hello
  },
  data(){
    return{
      img:'',
      description:'',
      cardTitle:'',
      cardDescription:{
        ace:{
          title:'Waterfall',
          desc:'Once someone picks an Ace, everyone must start chugging their drink. The person who picked the card to stop whenever they want; this allows the person to his/her right to stop drinking whenever. When that person stops drinking, the person to his/her can stop. This goes on until everyone is no longer drinking. '
        },
        two:{
          title:'You',
          desc:'The person who picks two, points to another person and that person drinks. '
        },
        three:{
          title:'Me',
          desc:'If you pick a three, you are drinking.'
        },
        four:{
          title:'"Whores"',
          desc:'"Whores" is not the word I would choose, but if someone picks a four, all the ladies drink. '
        },
        five:{
          title:'Never have I ever',
          desc:'When someone picks a five, each player puts up 3-5 fingers. The person who picked the five starts with saying something they have never done, if you have done it, you put a finger down. The first person to put down all their fingers, loses and drinks. '
        },
        six:{
          title:'"Dicks"',
          desc:'Another subpar choice of words in pursuit of a good rhyme. Six means all the guys take a drink. '
        },
        seven:{
          title:'Heaven',
          desc:'When a seven is picked, every player must raise their hand to \'heaven\'. The last player to do so drinks. This is a great time to ask for forgiveness for this game. '
        },
        eight:{
          title:'Mate',
          desc:'This isn\'t the type of \'mate\' you want. The person that picks an eight, picks another player to be their \'mate\'. When one of the \'mates\' drinks, the other has to as well.'
        },
        nine:{
          title:'Rhyme',
          desc:'This card will feel a little like a game you would play at summer camp as a kid. Don\'t get cocky, it\'s a little harder when you\'re a couple drinks deep. Whoever picks the nine says a word. The person to the right has to say a word that rhymes with it; this goes on until someone cannot think of a rhyme. That person has to take a drink. '
        },
        ten:{
          title:'Categories',
          desc:'Ten cards bring back the camp games, but this times it\'s a little more....adult. The person that picks a ten has to come up with a category (liquors, countries, etc..) and the person to his/her right has to say something in the category. When someone can\'t come up with something in that category, he/she drinks.'
        },
        jack:{
          title:'Rule',
          desc:'It might not rhyme, but this card is still fun. Whoever picks the jack comes up with a rule (you can only drink with your left hand, don\'t use first names, etc..) and whoever breaks the rule throughout the game drinks.'
        },
        queen:{
          title:'Questions',
          desc:'The person that picks a queen poses a question to anyone in the game. That person has to respond to the question with another question (What time is it? Is it around midnight?). This goes on until someone does not respond with a question and they (you guessed it) drink.'
        },
        king:{
          title:'King\'s Cup',
          desc:'When the first three kings are drawn, that player pours some of their drink into the King\'s cup. The person who draws the fourth and final king loses the game and drinks the contents of the cup.'
        },
      }
    }
  },
  methods:{
    showNewCard(){
      let firstChar
      this.img = data[Math.floor(Math.random()*data.length)]
      firstChar = this.img
      firstChar = firstChar.slice(firstChar.lastIndexOf(".") - 2)
      firstChar = firstChar.split('.')[0];
      firstChar = firstChar.charAt(0);

      switch(firstChar){
        case "A":
          this.cardTitle = this.cardDescription.ace.title
          this.description = this.cardDescription.ace.desc
          break
        case "2":
          this.cardTitle = this.cardDescription.two.title
          this.description = this.cardDescription.two.desc
          break
        case "3":
          this.cardTitle = this.cardDescription.three.title
          this.description = this.cardDescription.three.desc
          break
        case "4":
          this.cardTitle = this.cardDescription.four.title
          this.description = this.cardDescription.four.desc
          break
        case "5":
          this.cardTitle = this.cardDescription.five.title
          this.description = this.cardDescription.five.desc
          break
        case "6":
          this.cardTitle = this.cardDescription.six.title
          this.description = this.cardDescription.six.desc
          break
        case "7":
          this.cardTitle = this.cardDescription.seven.title
          this.description = this.cardDescription.seven.desc
          break
        case "8":
          this.cardTitle = this.cardDescription.eight.title
          this.description = this.cardDescription.eight.desc
          break
        case "9":
          this.cardTitle = this.cardDescription.nine.title
          this.description = this.cardDescription.nine.desc
          break
        case "0":
          this.cardTitle = this.cardDescription.ten.title
          this.description = this.cardDescription.ten.desc
          break
        case "J":
          this.cardTitle = this.cardDescription.jack.title
          this.description = this.cardDescription.jack.desc
          break
        case "Q":
          this.cardTitle = this.cardDescription.queen.title
          this.description = this.cardDescription.queen.desc
          break
        case "K":
          this.cardTitle = this.cardDescription.king.title
          this.description = this.cardDescription.king.desc
          break

      }
    }
  },
  mounted(){
    this.showNewCard()
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background: rgba(178,51,70,1);
  background: -moz-radial-gradient(center, ellipse cover, rgba(178,51,70,1) 0%, rgba(151,24,43,1) 100%);
  background: -webkit-gradient(radial, center center, 0px, center center, 100%, color-stop(0%, rgba(178,51,70,1)), color-stop(100%, rgba(151,24,43,1)));
  background: -webkit-radial-gradient(center, ellipse cover, rgba(178,51,70,1) 0%, rgba(151,24,43,1) 100%);
  background: -o-radial-gradient(center, ellipse cover, rgba(178,51,70,1) 0%, rgba(151,24,43,1) 100%);
  background: -ms-radial-gradient(center, ellipse cover, rgba(178,51,70,1) 0%, rgba(151,24,43,1) 100%);
  background: radial-gradient(ellipse at center, rgba(178,51,70,1) 0%, rgba(151,24,43,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#b23346', endColorstr='#97182b', GradientType=1 );
  min-height: 100vh;
}

h1{
  color: #fff;
}

.card-description{
  color: #fff;
  max-width: 500px;
  margin: auto;
}

main {
  text-align: center;
  margin-top: 40px;
}

header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495E;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: .02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
</style>
