```
function question(number, text, option_1, option_2, option_3, option_4, ans) {  
    this.id = number
	this.questionText = text
	this.option1 = option_1
	this.option2 = option_2
	this.option3 = option_3
	this.option4 = option_4
	this.correctAnswer = ans
}

var q1 = new question (
	1,
	'How many Jimmy Johns are in Columbia, MO?',
	'1', '2', '4', '5',
	4
)

var q2 = new question (
	2,
	'Jimmy Johns was established in what year?',
	'1975', '1983', '1989', '1996',
	2
)

var q3 = new question (
	3,
	'What is the difference between the Slims and the Originals and Favorites?',
	'They only have meat and/or cheese', 'The amount of meat on them', 'The bread they are on', 'They have extra vegetables',
	1
)

var q4 = new question (
	4,
	'What does it mean to "Jimmy it up?"',
	'The sandwich is made extra fast', 'The sandwich comes on the full loaf', 'The sandwich comes with every meat', 'The sandwich comes with herbs, peppers, onions and sauce',
	4
)

var q5 = new question (
	5,
	'How old was Jimmy when he started the company?',
	'19', '24', '32', '36',
	1
)

var q6 = new question (
	6,
	'Which of these politicians served Jimmy Johns on their campaign bus for president',
	'Barack Obama', 'John McCain', 'Mitt Romney', 'George W. Bush',
	3
)

var q7 = new question (
	7,
	'How many different sandwiches were on the original menu in 1983',
	'2', '4', '8', '10',
	2
)

var q8 = new question (
	8,
	'What is the franchises official record for fastest made sub?',
	'6 seconds', '9 seconds', '12 seconds', '16 seconds',
	3
)

var q9 = new question (
	9,
	'Roughly how many Jimmy Johns stores are there across the US',
	'1100', '1600', '2200', '2800',
	4
)

var q10 = new question (
	10,
	'What does it mean to "slop up" your sandwich',
	'No Lettuce', 'Extra Mayo', 'Extra oil and vinegar', 'All of the above', 
	4
)
var questions = [q1, q2, q3, q4, q5, q6, q7, q8, q9, q10]

$(document).ready(function () {
	var correct = 0
		wrong = 0
		question = 0
	var disabled = false
	let shuffledQuestions

	$('.start').on('click', function(startGame) {
		$('.qText').show()
		$('.answers').show()
		$('.result').show()
		$('.reset').show()
		$('.start').hide()
		shuffledQuestions=questions.sort(() => Math.random()-.5)
		nextQuestion()
	})
	
	function nextQuestion(){
		disabled = false
		$('.result').text('')
		var obj = shuffledQuestions[question]
		
		var qText = obj.questionText
		$('.qText').text(qText)
		
		var qAnswers = [obj.option1, obj.option2, obj.option3, obj.option4]
		$('.answers').text('')
		for (var i = 0; i < qAnswers.length; i++) {
			var ans = qAnswers[i]
			var id = i + 1
			var first = '<li id="'+id+'">'
			var last = '</li>'
			$('.answers').append(first+ans+last)
		}
		$('#1').click(function(){
			answerTime(1)
		})
		$('#2').click(function(){
			answerTime(2)
		})
		$('#3').click(function(){
			answerTime(3)
		})
		$('#4').click(function(){
			answerTime(4)
		})


	}
	function answerTime(num) {
		if(disabled) {
			return
		}
		var count = question
		var obj = shuffledQuestions[count]
		var correctNum = obj.correctAnswer
		if (num == correctNum) {
			correct++
			$('.result').text('Correct!')
		} else {
			wrong++
			$('.result').text('Incorrect!')
			$('#'+num).addClass('w3-red')
		}
		$('#'+correctNum).addClass('w3-green')
		$('.result').append('<br> Correct: ' + correct + '<br>')
		$('.result').append('Wrong: ' + wrong + '<br>')
		question++
		if (question < 10) {
			setTimeout(nextQuestion, 2000)
		} else {
			$('.answers').text('Press reset to go through them again in a different order')
			$('.qText').text('')
			$('.result').html('<br> Correct: ' + correct + '<br>')
			$('.result').append('Wrong: ' + wrong + '<br>')
		} 
		disabled = true
	}
	
})
```
