<template>
<div id='app'>
  <!-- Questions: display a div for each question -->
  <!-- show only if the index of the question is equal to the question index -->
  <div v-for="(quiz, index) in quizez" v-show="index === questionindex">
    <!-- Display the quiz category -->
    <h1>{{ quiz.category}}</h1>
    <!-- Display the question -->
    <h2> {{quiz.question}} </h2>
    <!-- Responses: display a li for each possible response with a radio button -->
    <ul>
      <!-- display thr quiz options -->
      <li v-for="answer in quiz.incorrect_answers">
        <label>
        <!-- bind the options to the array index of the answers array that matches this index -->
        <input type="radio" name="answer" v-model="answers[index]" :value="answer">{{answer}}
        </label>

      </li>
    </ul>
  </div>
  <!-- do not display if the question index exceeds the length of all quizez -->
  <div v-if="questionindex < quizez.length">
    <!-- display only if question index is greater than zero -->
    <!-- onclick of this button, call the previous function, and show last question -->
    <button v-if="questionindex > 0" v-on:click="prev">
       Previous
       </button>

    <!-- onclick of this button, call the next function and show next question -->
    <button v-on:click="next">
       Next
       </button>
  </div>

  <!-- show total score if the questions are completed -->
  <span v-if="questionindex== quizez.length">Your total score is {{score}}/{{quizez.length}}</span>
</div>
</template>

<script>
// an array of questions to be asked. Length of 10 questions.
var quizQuestions = [{
    'category': 'Entertainment: Film',
    'type': 'multiple',
    'difficulty': 'easy',
    'question': 'Who directed \'E.T. the Extra-Terrestrial\' (1982)?',
    'correct_answer': 'Steven Spielberg',
    'incorrect_answers': [
      'Steven Spielberg',
      'Stanley Kubrick',
      'James Cameron',
      'Tim Burton'
    ]
  },
  {
    'category': 'Entertainment: Video Games',
    'type': 'multiple',
    'difficulty': 'medium',
    'question': 'What is the main character of Metal Gear Solid 2?',
    'correct_answer': 'Raiden',
    'incorrect_answers': [
      'Raiden',
      'Solidus Snake',
      'Big Boss',
      'Venom Snake'
    ]
  },
  {
    'category': 'Science & Nature',
    'type': 'multiple',
    'difficulty': 'easy',
    'question': 'What is the hottest planet in the Solar System?',
    'correct_answer': 'Venus',
    'incorrect_answers': [
      'Venus',
      'Mars',
      'Mercury',
      'Jupiter'
    ]
  },
  {
    'category': 'Entertainment: Books',
    'type': 'multiple',
    'difficulty': 'hard',
    'question': 'What is Ron Weasley\'s middle name?',
    'correct_answer': 'Bilius',
    'incorrect_answers': [
      'Bilius',
      'Arthur',
      'John',
      'Dominic'
    ]
  },
  {
    'category': 'Politics',
    'type': 'multiple',
    'difficulty': 'medium',
    'question': 'Before 2011, \'True Capitalist Radio\' was known by a different name. What was that name?',
    'correct_answer': 'True Conservative Radio',
    'incorrect_answers': [
      'True Conservative Radio',
      'True Republican Radio',
      'Texan Capitalist Radio',
      'United Capitalists'
    ]
  },
  {
    'category': 'Entertainment: Film',
    'type': 'multiple',
    'difficulty': 'medium',
    'question': 'This movie contains the quote, \'I love the smell of napalm in the morning!\'',
    'correct_answer': 'Apocalypse Now',
    'incorrect_answers': [
      'Apocalypse Now',
      'Platoon',
      'The Deer Hunter',
      'Full Metal Jacket'
    ]
  },
  {
    'category': 'History',
    'type': 'multiple',
    'difficulty': 'medium',
    'question': 'The Herero genocide was perpetrated in Africa by which of the following colonial nations?',
    'correct_answer': 'Germany',
    'incorrect_answers': [
      'Germany',
      'Britain',
      'Belgium',
      'France'
    ]
  },
  {
    'category': 'Entertainment: Music',
    'type': 'boolean',
    'difficulty': 'medium',
    'question': 'Ashley Frangipane performs under the stage name Halsey.',
    'correct_answer': 'True',
    'incorrect_answers': [
      'True',
      'False'
    ]
  },
  {
    'category': 'Entertainment: Books',
    'type': 'multiple',
    'difficulty': 'easy',
    'question': 'Under what pseudonym did Stephen King publish five novels between 1977 and 1984?',
    'correct_answer': 'Richard Bachman',
    'incorrect_answers': [
      'Richard Bachman',
      'J. D. Robb',
      'Mark Twain',
      'Lewis Carroll'
    ]
  },
  {
    'category': 'History',
    'type': 'multiple',
    'difficulty': 'medium',
    'question': 'In what prison was Adolf Hitler held in 1924?',
    'correct_answer': 'Landsberg Prison',
    'incorrect_answers': [
      'Landsberg Prison',
      'Spandau Prison',
      'Ebrach Abbey',
      'Hohenasperg'
    ]
  }
]

export default {
  // name of the component
  name: 'app',
  // function that returns data to the components
  data: function() {
    return {
      // question index, used to show the current question
      questionindex: 0,
      // set the variable quizez to the questions defined earlier
      quizez: quizQuestions,
      // create an array of the length of the questions, and assign them to an empty value.
      answers: Array(quizQuestions.length).fill('')
    }
  },

  // methods to be called in the component
  methods: {
    // Go to the next question
    next: function() {
      this.questionindex++
    },
    // Go to the previous question
    prev: function() {
      this.questionindex--
    }
  },
  computed: {
    // calculate total score of the quiz person
    score: function() {
      var total = 0
      for (var i = 0; i < this.answers.length; i++) {
        if (this.answers[i] === this.quizez[i].correct_answer) {
          total += 1
        }
      }
      return total
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
