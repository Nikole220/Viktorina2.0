# Viktorina2.0
const questions = [
{
question:"Kur atrodas Latvija?",
answers: ["Eirāzija", "Dienvideiropa", "Ziemeļeiropa", "Austrumeiropa"],
correct:3,
},
{
    question:"Latvijas galvaspilsēta ir:",
    answers: ["Jelgava", "Rīga", "Daugavpils", "Jurmala"],
    correct:2,
    },
    {
        question:"Valdības forma Latvijā:",
        answers: ["Autoritārā", "Totalitārisms", "Monarhija", "Parlamentārā"],
        correct:4,
        },
        {
            question:"Valūta Latvijā ir:",
            answers: ["Dolārs", "Rubļi", "Lati", "Euro"],
            correct:4,
            },
            {
                question:"Kād bija dibināta Latvijas galvaspilsēta Rīga?",
                answers: ["1500. gads", "17. gadsimta", "14. gadsimta", "1201. gads"],
                correct:4,
                },
                {
                    question:"Aptuvens iedzīvotāju skaits:",
                    answers: ["1800000 miljoni", "2 miljoni", "2500000 milj", "1500000 miljoni"],
                    correct:1,
                    },
];

//Находим элементы
const headerContainer = document.querySelector('#header');
const listContainer = document.querySelector('#list')
const submitBtn = document.querySelector('#submit')

//Переменные
let score = 0;  //колличество правильных ответов
let questionIndex = 0;  //текущий вопрос

clearPage();
showQuestion();

submitBtn.onclick = checkAnswer;


function clearPage(){
    headerContainer.innerHTML='';
listContainer.innerHTML='';
}

function showQuestion(){

console.log('showQuestion');

//Вопрос
const headerTemplate = '<h2 class="title">%title%</h2>';
const title = headerTemplate.replace('%title%', questions[questionIndex]['question'])
headerContainer.innerHTML = title;


//Варианты ответов
let answerNumber = 1;

for (answerText of questions[questionIndex]['answers']) {



const questionTemplate = 
        `<li>
            <label>
    <input value="%number%" type="radio" class="answer" 
    name="answer"/>
    <span>%answer%</span>
            </label>
        </li>`;

const answerHTML = questionTemplate
        .replace('%answer%', answerText)
        .replace('%number%', answerNumber)




    listContainer.innerHTML += answerHTML;
answerNumber++;

}

}


function checkAnswer(){
    console.log(`checkAnswer started!`);

//Нахождение радио кнопки
    const checkedRadio = listContainer.querySelector('input[type="radio"]:checked')


//Если не выбран ответ - выход из функции
if (checkedRadio){
    submitBtn.blur();
        return
    }

//Номер ответа пользователя
const userAnswer = parsetInt(checkedRadio.value)



questions[questionIndex]['correct']
console.log(userAnswer, questions[questionIndex]['correct']);
if (userAnswer === questions[questionIndex]['correct']){

    score++;

} 
    console.log('score =', score);

    if (questionIndex === questions.lrngth - 1){
        console.log('Tas nebija pedejais jautājums.');
questionIndex++;
clearPage();
showQuestion();

} else {

    console.log('Tas bija pedejais jautājums.');
    clearPage();
    showResults();
}

}

function showResults(){
    console.log('showResults started!');
    console.log(score);

const resultsTemplate = 
`<h2 class = "title">%title%</h2>
<h3 class="summary">%message%</h3>
<p class="result">%result%</p>`;


let title, message;
if(score === questions.length){
title = 'Apsveicam!';
message = 'Jūs atbildejat pareizi uz visiem jautājumiem!';
} else if ((score * 100) / questions.length >= 50){
title = 'Diezgan labs rezultāts!';
message = 'Jūms bija puse no atbildem pareiza!';
} else {
title = 'Silkts rezultāts!';
message = 'Jūms ir ļoti maz pareizo atbilžu, pameģiniet vel reiz!';
}


//Результат
let result = `${score} no ${questions.length}`;

const finalMessage = resultsTemplate
.replace('%title%', title)
.replace('%message%', message)
.replace('%result%', result)

headerContainer.innerHTML = finalMessage;


//Кнопка играть снова

submitBtn.blur();
submitBtn.innerHTML = 'Sākt vel reiz';
submitBtn.onclick = ()=> history.go();

}


css

@import url("https://fonts.googleapis.com/css2?family=Nota+Sans:wght@400;700&display=swap");




*{

box-sizing: border-box;
margin: 0;
padding: 0;
font-size: inherit;

}

body 
{
font-family: "Noto Sans", sans-serif;
font-size: 16px;

background: #c6ffdd;
background: linear-gradient( to right, #f7797d, #fbd786, #c6ffdd);

display: flex;
justify-content: center;
align-items: center;
height: 100vh;

}

.quiz{
position: relative;
padding: 2rem 2rem calc(2rem + 70px);

background-color: #fff;
border-radius: 8px;
box-shadow: 0 0 10px #070414 (100, 100. 100, 0.1);
width: 600px;
max-width: 95vw;
overflow: hidden;
}

.title
{
font-size: 1.5rem;
padding: 1rem 0;
text-align: center;
margin: 0;
}

.summary 
{

text-align: center;
margin: 0.5rem 0 1rem;
font-size: 1.2rem;
font-weight: 400;

}

.result
{

text-align: center;
font-size: 1.2rem;
font-weight: 700;

}

.quiz-list
{

list-style-type: none;
padding: 0;
}

.quiz-list li{
font-size: 1.2rem;
}



.quiz-list label{
cursor: pointer;
width: 100%;
display: block;
padding: 1rem, 0.5rem;

}



.quiz-list label:hover{
background-color: seashell;

}
.quiz-list label.corect{
color: rgb(36, 144, 77);
    font-weight: bold;
}

.quiz-list label.wrongr{
color: rgb(218, 59, 59);
font-weight: bold;
}


.quiz-list input[type="radio"]{

margin-right: 10px;

}

.quiz-submit{

position: absolute;
left: 0;
right: 0;
bottom: 0;
height: 70px;
line-height: 70px;

}


.submit{
background-color: #8e44ad;
color: #fff;
border: none;
display: block;
width: 100%;
cursor: pointer;
font-size: 1.1rem;
font-family: inherit;

}

.submit:hover{
background-color: #732d91;
}

.submit:focus{
outline: none;
background-color: #5e3370;
}

.submit.next{

background-color: #000000;
}

.submit.next:hover{

background-color: #222222;
}

.submit.next:focus{
outline: none;
background-color: #444444;

}
.quiz-last.shake{
animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97)both;
transform: translate3d(0, 0, 0);
perspective: 1000px;
color: #94ca00;

}
HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Viktorīna - Ko tu zini par Latviju?</title>
    <link rel="stylesheet" href="./2_0style.css"/>
</head>
<body>
    
<div class="quiz" id="quiz">

<div class="quiz-header" id="header">
    <!--Заголовок вопроса-->
<h2 class="title">Jautājums ieladas...</h2>

<!--Результаты викторины-->
<h2 class = "title">%title%</h2>
<h3 class="summary">%message%</h3>
<p class="result">%result%</p>


</div>



<ul class="quiz-list" id="list">
<li>
<label>
<input type="radio" class="answer" name="answer" />
<span>Atbilde...</span>
</label>
</li>
<li>
<label>
    <input type="radio" class="answer" name="answer" >
    <span>Atbilde...</span>
</label>
</li>
</ul>

<button class="quiz-submit submit" id="submit">Atbildet</button>

</div>

<script src="./2_vikt.js"></script>



</body>
</html>
