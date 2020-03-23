<template>
  <div id="app">
    <header class="d-flex justify-content-between">
      <div id="logo" class="d-block"><img src="@/assets/kingcuplogo.png" /></div>
      <div class=""><button @click.prevent="reset" class="btn btn-outline-primary btn-lg">Reset Game</button></div>
    </header>
    <main>
      <section class="container h-100 d-flex align-items-center justify-content-center">
        <div class="d-block">
          <h4 class="text-white my-5">Cards drawn: {{cardDrawnTotal}}</h4>
          <div class="card-container d-block">
            <div class="cards-show position-relative">
              <img @click.prevent="showNewCard" :src="img" class="card-primary" />
              <img src="@/assets/cards/filler-card.png" class="card-filler" v-if="cardDrawnTotal <= 50" />
              <img src="@/assets/cards/filler-card.png" class="card-filler card-filler--two" v-if="cardDrawnTotal <= 51" />
            </div>
            <div class="card-info mt-4">
              <h1>{{ cardTitle }}</h1>
              <div class="card-description">
                <p>{{ description }}</p>
              </div>
            </div>

          </div>
          <div class="card-nav__next text-center">
            <button @click.prevent="showNewCard" class="btn btn-primary btn-lg" v-if="cardDrawnTotal !== cardsTotal">Next Card</button>
            <button @click.prevent="reset" class="btn btn-primary btn-lg" v-if="cardDrawnTotal === cardsTotal">Reset Game</button>
          </div>
        </div>
        
      </section>
    </main>
  </div>
</template>

<script>
import data from "./cards.json";

const images = require.context('@/assets/cards', false, /\.png$|\.jpg$/)

export default {
  name: "app",
  data() {
    return {
      img: "",
      description: "",
      cardTitle: "",
      cardsDrawn: [],
      cardDescription: {
        ace: {
          title: "Waterfall",
          desc:
            "Once someone picks an Ace, everyone must start chugging their drink. The person who picked the card to stop whenever they want; this allows the person to his/her right to stop drinking whenever. When that person stops drinking, the person to his/her can stop. This goes on until everyone is no longer drinking. "
        },
        two: {
          title: "You",
          desc:
            "The person who picks two, points to another person and that person drinks. "
        },
        three: {
          title: "Me",
          desc: "If you pick a three, you are drinking."
        },
        four: {
          title: '"Whores"',
          desc:
            '"Whores" is not the word I would choose, but if someone picks a four, all the ladies drink. '
        },
        five: {
          title: "Never have I ever",
          desc:
            "When someone picks a five, each player puts up 3-5 fingers. The person who picked the five starts with saying something they have never done, if you have done it, you put a finger down. The first person to put down all their fingers, loses and drinks. "
        },
        six: {
          title: '"Dicks"',
          desc:
            "Another subpar choice of words in pursuit of a good rhyme. Six means all the guys take a drink. "
        },
        seven: {
          title: "Heaven",
          desc:
            "When a seven is picked, every player must raise their hand to 'heaven'. The last player to do so drinks. This is a great time to ask for forgiveness for this game. "
        },
        eight: {
          title: "Mate",
          desc:
            "This isn't the type of 'mate' you want. The person that picks an eight, picks another player to be their 'mate'. When one of the 'mates' drinks, the other has to as well."
        },
        nine: {
          title: "Rhyme",
          desc:
            "This card will feel a little like a game you would play at summer camp as a kid. Don't get cocky, it's a little harder when you're a couple drinks deep. Whoever picks the nine says a word. The person to the right has to say a word that rhymes with it; this goes on until someone cannot think of a rhyme. That person has to take a drink. "
        },
        ten: {
          title: "Categories",
          desc:
            "Ten cards bring back the camp games, but this times it's a little more....adult. The person that picks a ten has to come up with a category (liquors, countries, etc..) and the person to his/her right has to say something in the category. When someone can't come up with something in that category, he/she drinks."
        },
        jack: {
          title: "Rule",
          desc:
            "It might not rhyme, but this card is still fun. Whoever picks the jack comes up with a rule (you can only drink with your left hand, don't use first names, etc..) and whoever breaks the rule throughout the game drinks."
        },
        queen: {
          title: "Questions",
          desc:
            "The person that picks a queen poses a question to anyone in the game. That person has to respond to the question with another question (What time is it? Is it around midnight?). This goes on until someone does not respond with a question and they (you guessed it) drink."
        },
        king: {
          title: "King's Cup",
          desc:
            "When the first three kings are drawn, that player pours some of their drink into the King's cup. The person who draws the fourth and final king loses the game and drinks the contents of the cup."
        }
      }
    };
  },
  computed: {
    cardDrawnTotal() {
      return this.cardsDrawn.length;
    },
    cardsTotal() {
      return data.length
    }
  },
  methods: {
    showNewCard() {
      //Prevent from drawing card
      if (this.cardDrawnTotal == data.length) {
        return;
      }

      const randomImg = data[Math.floor(Math.random() * data.length)];
      this.img = this.loadImg(randomImg);
      let firstChar = randomImg.slice(randomImg.lastIndexOf(".") - 2).split(".")[0];

      //Dont show same cards
      if (this.cardsDrawn.includes(firstChar)) {
        this.showNewCard();
        return;
      }

      this.cardsDrawn.push(firstChar);
      firstChar = firstChar.charAt(0);

      switch (firstChar) {
        case "A":
          this.cardTitle = this.cardDescription.ace.title;
          this.description = this.cardDescription.ace.desc;
          break;
        case "2":
          this.cardTitle = this.cardDescription.two.title;
          this.description = this.cardDescription.two.desc;
          break;
        case "3":
          this.cardTitle = this.cardDescription.three.title;
          this.description = this.cardDescription.three.desc;
          break;
        case "4":
          this.cardTitle = this.cardDescription.four.title;
          this.description = this.cardDescription.four.desc;
          break;
        case "5":
          this.cardTitle = this.cardDescription.five.title;
          this.description = this.cardDescription.five.desc;
          break;
        case "6":
          this.cardTitle = this.cardDescription.six.title;
          this.description = this.cardDescription.six.desc;
          break;
        case "7":
          this.cardTitle = this.cardDescription.seven.title;
          this.description = this.cardDescription.seven.desc;
          break;
        case "8":
          this.cardTitle = this.cardDescription.eight.title;
          this.description = this.cardDescription.eight.desc;
          break;
        case "9":
          this.cardTitle = this.cardDescription.nine.title;
          this.description = this.cardDescription.nine.desc;
          break;
        case "0":
          this.cardTitle = this.cardDescription.ten.title;
          this.description = this.cardDescription.ten.desc;
          break;
        case "J":
          this.cardTitle = this.cardDescription.jack.title;
          this.description = this.cardDescription.jack.desc;
          break;
        case "Q":
          this.cardTitle = this.cardDescription.queen.title;
          this.description = this.cardDescription.queen.desc;
          break;
        case "K":
          this.cardTitle = this.cardDescription.king.title;
          this.description = this.cardDescription.king.desc;
          break;
      }
    },
    loadImg(imgPath) {
      return images('./' + imgPath)
    },
    reset() {
      this.cardsDrawn = [];
      this.showNewCard();
    }
  },
  mounted() {
    this.showNewCard();
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Poppins');

html, body, #app {
  height: 100%;
}

body {
  margin: 0;
}

#app {
  font-family: "Poppins", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background: rgba(178, 51, 70, 1);
  background: -moz-radial-gradient(
    center,
    ellipse cover,
    rgba(178, 51, 70, 1) 0%,
    rgba(151, 24, 43, 1) 100%
  );
  background: -webkit-gradient(
    radial,
    center center,
    0px,
    center center,
    100%,
    color-stop(0%, rgba(178, 51, 70, 1)),
    color-stop(100%, rgba(151, 24, 43, 1))
  );
  background: -webkit-radial-gradient(
    center,
    ellipse cover,
    rgba(178, 51, 70, 1) 0%,
    rgba(151, 24, 43, 1) 100%
  );
  background: -o-radial-gradient(
    center,
    ellipse cover,
    rgba(178, 51, 70, 1) 0%,
    rgba(151, 24, 43, 1) 100%
  );
  background: -ms-radial-gradient(
    center,
    ellipse cover,
    rgba(178, 51, 70, 1) 0%,
    rgba(151, 24, 43, 1) 100%
  );
  background: radial-gradient(
    ellipse at center,
    rgba(178, 51, 70, 1) 0%,
    rgba(151, 24, 43, 1) 100%
  );
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#b23346', endColorstr='#97182b', GradientType=1 );
}

.flex-1 {
  flex: 1!important;
}

h1 {
  color: #fff;
}

.card-description {
  color: #fff;
  max-width: 500px;
  margin: auto;
}

main {
  text-align: center;
  height: 100%;
}

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495e;
  color: #ffffff;
  display: flex!important;
  align-items: center;
  justify-content: center;
}

#logo img {
  height: 50px;
  width: auto;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: 0.02em;
  font-weight: 400;
  box-sizing: border-box;
}

.card-container {
  min-height: 600px;
}

.cards-show {
  z-index: 10;
}

.card-filler {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%) rotate(5deg);
  z-index: -1;
}

.card-filler--two {
  transform: translateX(-50%) rotate(-5deg);
}

/* .card-nav__next {
  position: fixed;
  bottom: 5rem;
  left: 0;
  width: 100%;
} */

.btn {
  border-radius: 80px!important;
  min-width: 180px!important;
  transition: opacity .3s ease-in-out!important;
}

.btn-primary {
  background-color: #f2ba49!important;
  border-color: #f2ba49!important;
}

.btn-outline-primary {
  color: #f2ba49!important;
  border-color: #f2ba49!important;
}

.btn:hover,
.btn:focus,
.btn:active {
  background-color: #f2ba49!important;
  border-color: #f2ba49!important;
  outline: none!important;
  box-shadow: none !important;
  opacity: 0.8!important;
}


</style>
