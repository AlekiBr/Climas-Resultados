# Climas-Resultados

Desafio proposto Na aula de Monitoramento de Pragas e Doeças pela Prof.:RENATA BRUNA DOS SANTOS COSCOLIN FAVAN na Fatec Shunji Nishimura - Big Data no Agronegócio, ...

<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Análise de Risco Climático</title>
    <style>
        style>
            body {
            font-family: 'Roboto', sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            transition: background-color 0.3s ease;
        }

        .container {
            max-width: 500px;
            background-color: #fff;
            border-radius: 15px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            padding: 30px;
            transition: box-shadow 0.3s ease;
        }

        h1 {
            text-align: center;
            margin-bottom: 30px;
            color: #444;
            font-size: 2em;
        }

        label {
            font-weight: bold;
            color: #666;
            font-size: 1.2em;
        }

        input[type="number"],
        select {
            width: calc(100% - 16px);
            padding: 12px;
            margin-bottom: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-sizing: border-box;
            transition: border 0.3s ease;
        }

        button {
            width: 100%;
            padding: 15px;
            background-color: #008cff;
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #006cb3;
        }

        .resposta {
            margin-top: 30px;
            padding: 30px;
            border-radius: 8px;
            background-color: #fafafa;
            border: 1px solid #ddd;
            color: #444;
            transition: border 0.3s ease;
        }
    </style>

    </style>
</head>

<body>
    <h1>Análise de Risco Climático</h1>

    <div id="formulario">
        <label for="cultura">Qual o plantio:</label>
        <select id="cultura">
            <option value="1">Cana de açúcar</option>
            <option value="2">Soja</option>
            <option value="3">Café</option>
        </select><br>

        <label for="clima_atual">Qual o clima atual:</label>
        <input type="text" id="clima_atual"><br>

        <label for="clima_maximo">Qual o clima máximo:</label>
        <input type="number" id="clima_maximo"><br>

        <label for="clima_minimo">Qual o clima mínimo:</label>
        <input type="number" id="clima_minimo"><br>

        <label for="umidade">Qual a umidade:</label>
        <input type="number" id="umidade"><br>

        <label for="temperatura">Qual a temperatura:</label>
        <input type="number" id="temperatura"><br>

        <button onclick="analisarRisco()">Analisar Risco</button>
    </div>

    <div id="resultado" class="resposta">
        <!-- O resultado da análise será exibido aqui -->
    </div>

    <script>
        function analisarRisco() {
            var cultura = document.getElementById('cultura').value;
            var clima_atual = document.getElementById('clima_atual').value;
            var clima_maximo = parseFloat(document.getElementById('clima_maximo').value);
            var clima_minimo = parseFloat(document.getElementById('clima_minimo').value);
            var umidade = parseFloat(document.getElementById('umidade').value);
            var temperatura = parseFloat(document.getElementById('temperatura').value);

            var resultado = "Análise de Risco:<br>";
            resultado += "Risco: " + analisarRiscoClimatico(cultura, clima_atual, clima_maximo, clima_minimo, umidade, temperatura) + "<br><br>";
            resultado += "Ação Recomendada:<br>";
            resultado += acaoRecomendada(cultura, clima_atual, temperatura) + "<br><br>";
            resultado += "Pragas Associadas:<br>";
            resultado += pragasAssociadas(cultura, temperatura) + "<br><br>";
            resultado += "Controle de Pragas:<br>";
            resultado += controlePragas(cultura) + "<br>";

            document.getElementById('resultado').innerHTML = resultado;
        }

        function analisarRiscoClimatico(cultura, clima_atual, clima_maximo, clima_minimo, umidade, temperatura) {
            if (cultura === '1') {  // Cana de açúcar
                if (temperatura < 22 || temperatura > 30) {
                    return 'Alto risco';
                } else {
                    return 'Baixo risco';
                }
            } else if (cultura === '2') {  // Soja
                if (temperatura <= 10 || temperatura > 40) {
                    return 'Alto risco';
                } else {
                    return 'Baixo risco';
                }
            } else if (cultura === '3') {  // Café
                if (clima_atual === 'seca' || temperatura > 24 || temperatura < 18) {
                    return 'Alto risco';
                } else {
                    return 'Baixo risco';
                }
            } else {
                if (clima_atual === 'seca' || temperatura > clima_maximo) {
                    return 'Alto risco';
                } else if (clima_atual === 'chuva' && umidade > 80) {
                    return 'Risco moderado';
                } else if (temperatura < clima_minimo) {
                    return 'Risco moderado';
                } else {
                    return 'Baixo risco';
                }
            }
        }

        function acaoRecomendada(cultura, clima_atual, temperatura) {
            var risco = analisarRiscoClimatico(cultura, clima_atual, temperatura);
            if (risco === 'Alto risco') {
                return 'O alto risco pode levar a pragas e morte nas plantas. Recomenda-se aumentar a irrigação e monitorar de perto as condições das plantas.';
            } else if (risco === 'Risco moderado') {
                return 'O risco moderado pode levar a algumas perdas na produção. Recomenda-se ajustar a irrigação e talvez considerar o uso de coberturas para proteger as plantas.';
            } else {
                return 'O risco é baixo. Continue monitorando as condições e mantenha as práticas agrícolas normais.';
            }
        }

        function pragasAssociadas(cultura, temperatura) {
            if (cultura === '1') {  // Cana de açúcar
                if (temperatura < 18) {
                    return 'Broca da cana-de-açúcar (Diatrea sacchralis) é uma praga que pode se desenvolver em temperaturas mais baixas.<br><br>Sintomas: Perfurações nos colmos, descoloração das folhas, murcha e morte de parte da planta.<br><br>Impacto na planta: As pragas podem causar danos diretos aos colmos, raízes e folhas da cana-de-açúcar, enfraquecendo a planta, reduzindo seu crescimento e diminuindo a produção de açúcar.';
                } else if (temperatura >= 18 && temperatura <= 30) {
                    return 'Cigarrinha-das-raízes (Mahanarva fimbriolata) e cupim da cana-de-açúcar são pragas comuns em temperaturas médias.<br><br>Sintomas: Perfurações nos colmos, descoloração das folhas, murcha e morte de parte da planta.<br><br>Impacto na planta: As pragas podem causar danos diretos aos colmos, raízes e folhas da cana-de-açúcar, enfraquecendo a planta, reduzindo seu crescimento e diminuindo a produção de açúcar.';
                } else {
                    return 'Broca da cana-de-açúcar (Diatrea sacchralis) e bicudo da cana-de-açúcar (Sphenophorus levis) podem se multiplicar mais rapidamente em altas temperaturas.<br><br>Sintomas: Perfurações nos colmos, descoloração das folhas, murcha e morte de parte da planta.<br><br>Impacto na planta: As pragas podem causar danos diretos aos colmos, raízes e folhas da cana-de-açúcar, enfraquecendo a planta, reduzindo seu crescimento e diminuindo a produção de açúcar.';
                }
            } else if (cultura === '2') {  // Soja
                if (temperatura < 10) {
                    return 'Larvas de mariposas, como a lagarta elasmo, coró, piolho de cobra, caramujo, lesmas, grilos, gafanhotos, tamanduá e vaquinha, podem ser pragas problemáticas em temperaturas mais baixas.<br><br>Sintomas: Desfolha, perfurações nas folhas, danos nos brotos e podridão dos frutos.<br><br>Impacto na planta: As larvas se alimentam das folhas, brotos e frutos, reduzindo a área fotossintética, enfraquecendo a planta e comprometendo sua produção.';
                } else if (temperatura >= 10 && temperatura <= 40) {
                    return 'Lagarta da soja (Anticarsia gemmatalis), lagarta do cartucho (Spodoptera frugiperda), lagarta-elasmo (Elasmopalpus lignosellus), lagarta-falsa-medideira (Chrysodeixis includens) e mosca-branca (Bemisia sp.) são pragas comuns em temperaturas médias.<br><br>Sintomas: Desfolha, perfurações nas folhas, danos nos brotos e podridão dos frutos.<br><br>Impacto na planta: As larvas se alimentam das folhas, brotos e frutos, reduzindo a área fotossintética, enfraquecendo a planta e comprometendo sua produção.';
                } else {
                    return 'Percevejos e lagartas podem se multiplicar mais rapidamente em altas temperaturas.<br><br>Sintomas: Desfolha, perfurações nas folhas, danos nos brotos e podridão dos frutos.<br><br>Impacto na planta: As larvas se alimentam das folhas, brotos e frutos, reduzindo a área fotossintética, enfraquecendo a planta e comprometendo sua produção.';
                }
            } else if (cultura === '3') {  // Café
                if (temperatura < 18) {
                    return 'Broca-do-café (Hypothenemus hampei) é uma praga que pode se desenvolver em temperaturas mais baixas.<br><br>Sintomas: Perfurações circulares nos grãos de café, danificando a qualidade e o rendimento da colheita.<br><br>Impacto na planta: A broca-do-café penetra nos frutos do café, causando danos diretos à semente. Isso pode enfraquecer a planta e reduzir sua produção.';
                } else if (temperatura >= 18 && temperatura <= 24) {
                    return 'Bicho-mineiro (Leucoptera coffeella) é uma praga comum em temperaturas médias.<br><br>Sintomas: Minas ou galerias nas folhas, causando descoloração e deformação.<br><br>Impacto na planta: A alimentação das larvas dentro das folhas pode enfraquecer a planta, reduzindo sua capacidade de fotossíntese e, consequentemente, afetando seu crescimento e produção.';
                } else {
                    return 'Ácaro vermelho pode se tornar uma praga problemática em altas temperaturas.<br><br>Sintomas: Descoloração das folhas, pequenas manchas amareladas e teias finas sobre a planta.<br><br>Impacto na planta: Os ácaros se alimentam dos tecidos foliares, causando danos que podem levar à queda prematura das folhas e à redução da produção de frutos.';
                }
            } else {
                return 'Não tenho informações sobre as pragas associadas a essa cultura.';
            }
        }

        function controlePragas(cultura) {
            if (cultura === '1') {  // Cana de açúcar
                return 'Existem várias formas de controle de pragas na cana-de-açúcar, incluindo: plantio de variedades resistentes ou tolerantes; corte de cana sem desponte; moagem rápida após o corte; eliminação de plantas hospedeiras próximas ao canavial (milho, milheto).';
            } else if (cultura === '2') {  // Soja
                return 'O controle de pragas da soja é realizado através do tratamento de sementes ou de pulverizações, aplicadas no sulco de semeadura ou na parte aérea das plantas de soja.';
            } else if (cultura === '3') {  // Café
                return 'O controle de pragas do café pode ser realizado através de várias estratégias, incluindo o uso de produtos biológicos, o manejo integrado de pragas, e a preservação de inimigos naturais no agroecossistema.';
            } else {
                return 'Não tenho informações sobre o controle de pragas para essa cultura.';
            }
        }
    </script>
</body>

</html>
