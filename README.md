// Dados de exemplo de notícias para o jogo
const newsData = [
    { text: "Cientistas descobrem que comer chocolate todos os dias faz bem à saúde!", isTrue: false },
    { text: "Estudo revela que o uso de máscara reduz a propagação de vírus respiratórios.", isTrue: true },
    { text: "NASA anuncia missão para Marte que vai trazer água de volta à Terra!", isTrue: false }
];

let currentNewsIndex = 0;

// Elementos do HTML
const startButton = document.getElementById('startButton');
const gameSection = document.getElementById('gameSection');
const feedbackSection = document.getElementById('feedbackSection');
const newsText = document.getElementById('newsText');
const trueButton = document.getElementById('trueButton');
const falseButton = document.getElementById('falseButton');
const feedbackText = document.getElementById('feedbackText');
const nextButton = document.getElementById('nextButton');

// Função para iniciar o jogo
startButton.addEventListener('click', () => {
    startButton.style.display = 'none';
    gameSection.style.display = 'block';
    showNews();
});

// Exibe a notícia atual
function showNews() {
    const news = newsData[currentNewsIndex];
    newsText.textContent = news.text;
}

// Função para verificar a resposta
function checkAnswer(isTrue) {
    const news = newsData[currentNewsIndex];
    if ((isTrue && news.isTrue) || (!isTrue && !news.isTrue)) {
        feedbackText.textContent = "Resposta correta! Você identificou a fake news.";
    } else {
        feedbackText.textContent = "Resposta incorreta. Tente novamente!";
    }
    gameSection.style.display = 'none';
    feedbackSection.style.display = 'block';
}

// Eventos dos botões
trueButton.addEventListener('click', () => checkAnswer(true));
falseButton.addEventListener('click', () => checkAnswer(false));

// Avançar para a próxima notícia
nextButton.addEventListener('click', () => {
    currentNewsIndex++;
    if (currentNewsIndex < newsData.length) {
        showNews();
        feedbackSection.style.display = 'none';
        gameSection.style.display = 'block';
    } else {
        feedbackText.textContent = "Você completou o jogo! Parabéns!";
        nextButton.style.display = 'none';
    }
});
