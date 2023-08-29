<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* Seus estilos aqui */
    </style>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto&display=swap">
</head>
<body>
    <!-- Seu conteúdo HTML aqui -->

    <script>
        let vitorias = JSON.parse(localStorage.getItem('vitorias')) || [];

        function registrarVitoria() {
            const time = document.getElementById("time").value;
            const pontos = parseInt(document.getElementById("pontos").value);

            vitorias.push({ time: time, pontos: pontos });

            localStorage.setItem('vitorias', JSON.stringify(vitorias));

            updateVitoriasList();
            updateTimeDoMes();
        }

        function updateVitoriasList() {
            const lista = document.getElementById("vitoriasLista");
            lista.innerHTML = "";

            vitorias.forEach(vitoria => {
                const item = document.createElement("li");
                item.textContent = `${vitoria.time}: ${vitoria.pontos} pontos`;
                lista.appendChild(item);
            });
        }

        function updateTimeDoMes() {
            let timeMaisVitorias = "Nenhum time registrado";
            let maiorPontuacao = 0;

            vitorias.forEach(vitoria => {
                if (vitoria.pontos > maiorPontuacao) {
                    maiorPontuacao = vitoria.pontos;
                    timeMaisVitorias = vitoria.time;
                }
            });

            document.getElementById("timeDoMes").textContent = timeMaisVitorias;
        }

        function zerarPontuacao() {
            vitorias = [];
            localStorage.setItem('vitorias', JSON.stringify(vitorias));
            updateVitoriasList();
            updateTimeDoMes();
        }

        window.onload = function () {
            updateVitoriasList();
            updateTimeDoMes();
        };
    </script>
</body>
</html>
