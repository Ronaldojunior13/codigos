<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo de Perguntas ou Consequências</title>
    <style>
        body {
            background-color: #333;
            text-align: center;
            font-family: Arial, sans-serif;
            color: white;
        }
        #game-container {
            margin-top: 100px;
        }
        .button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 20px;
            margin: 10px;
            cursor: pointer;
        }
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        #respostas {
            display: none;
            margin-top: 20px;
        }
        #respostas ul {
            list-style-type: none;
            padding: 0;
        }
        #respostas li {
            margin: 10px 0;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div id="game-container" class="container">
        <div id="historias">
            <button class="button" id="bt2">Iniciar Jogo</button>
        </div>

        <div id="jogo" style="display: none;">
            <button class="button" id="bt-iniciar">Iniciar</button>
        </div>

        <div id="perguntas" style="display: none;">
            <p id="pergunta"></p>
            <input type="text" id="resposta" class="button">
            <button class="button" id="bt-enviar">Enviar</button>
        </div>

        <div id="respostas">
            <h2>Respostas anteriores:</h2>
            <ul id="lista-respostas"></ul>
        </div>
    </div>

    <script>
        const historias = document.getElementById("historias");
        const bt2 = document.getElementById("bt2");
        const btIniciar = document.getElementById("bt-iniciar");
        const respostasDiv = document.getElementById("respostas");
        const perguntaDiv = document.getElementById("perguntas");
        const respostaInput = document.getElementById("resposta");
        const listaRespostas = document.getElementById("lista-respostas");

        const perguntas = [
            "Você namora?",
            "Você já casou?",
            "Você já viajou para o exterior?",
            "Você gosta de esportes?",
            "você possui algum vicio?",
            "ja treinou um dia, e olhou-se no espelho e achou que estava forte",

            
        ];

        const respostas = [];

        let currentIndex = 0;

        bt2.addEventListener("click", function iniciar() {
            const rp1 = prompt("Você tem certeza que quer jogar?");

            if (rp1 && rp1.toLowerCase() === "sim") {
                exibirPergunta();
            } else {
                alert("Retire-se do jogo");
            }
        });

        function exibirPergunta() {
            historias.style.display = "none";
            bt2.style.display = "none";
            document.getElementById("jogo").style.display = "block";
            btIniciar.addEventListener("click", mostrarPergunta);
        }

        function mostrarPergunta() {
            document.getElementById("jogo").style; display = "none";
            perguntaDiv.style.display = "block";
            document.getElementById("pergunta").textContent = perguntas[currentIndex];
            btIniciar.removeEventListener("click", mostrarPergunta);

            const btEnviar = document.getElementById("bt-enviar");
            btEnviar.addEventListener("click", gravarResposta);
        }

        function gravarResposta() {
            const resposta = respostaInput.value;
            respostas.push(resposta);
            respostaInput.value = "";
            currentIndex++;
            if (currentIndex < perguntas.length) {
                mostrarPergunta();
            } else {
                exibirRespostas();
            }
        }

        function exibirRespostas() {
            perguntaDiv.style.display = "none";
            respostasDiv.style.display = "block";
            listaRespostas.innerHTML = "";
            respostas.forEach((resposta, index) => {
                const li = document.createElement("li");
                li.textContent = `Pergunta ${index + 1}: ${perguntas[index]} - Resposta: ${resposta}`;
                listaRespostas.appendChild(li);
            });
        }
    </script>

</body>
</html>

