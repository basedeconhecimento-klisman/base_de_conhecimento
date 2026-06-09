<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Base de Conhecimento SIGO</title>
    <style>
        :root {
            --azul-petroleo: #004d4d;
            --azul-claro: #006666;
            --branco: #ffffff;
            --cinza-claro: #f4f4f4;
            --transicao: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
        }

        body {
            font-family: 'Segoe UI', sans-serif;
            background-color: var(--azul-petroleo);
            color: var(--branco);
            margin: 0;
            padding: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        header {
            width: 100%;
            max-width: 1000px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 40px;
            position: relative;
            min-height: 120px;
        }

        .btn-seta-voltar {
            position: absolute;
            left: 0;
            background: none;
            border: 1.5px solid rgba(255, 255, 255, 0.4);
            color: white;
            font-size: 1.5rem;
            width: 45px;
            height: 40px;
            border-radius: 8px;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            transition: var(--transicao);
        }

        .logo {
            width: 100px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        h1 {
            margin-left: 20px;
            font-size: 2.4rem;
            text-shadow: 2px 2px 5px rgba(0,0,0,0.3);
            text-align: center;
        }

        .container-botoes {
            width: 100%;
            max-width: 1000px;
            display: flex;
            flex-direction: column;
            gap: 15px;
            align-items: center;
        }

        .btn-lateral-esquerda {
            padding: 15px 25px;
            font-size: 1.1rem;
            width: 100%;
            max-width: 450px;
            text-align: left;
            text-transform: uppercase;
        }

        .btn-principal {
            background-color: var(--branco);
            color: var(--azul-petroleo);
            border: none;
            font-weight: bold;
            border-radius: 12px;
            cursor: pointer;
            transition: var(--transicao);
            box-shadow: 0 4px 6px rgba(0,0,0,0.2);
        }

        #lista-modulos .btn-principal, .sub-menu-container .btn-principal, #sub-menu-suporte .btn-principal {
            padding: 25px 50px;
            font-size: 1.4rem;
            text-align: center;
            width: auto;
            min-width: 200px;
        }

        .btn-principal:hover {
            background-color: #e0e0e0;
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(0,0,0,0.4);
        }

        #lista-modulos, #sub-menu-suporte {
            display: none;
            gap: 25px;
            justify-content: center; 
            flex-wrap: wrap;
            width: 100%;
            margin-top: 20px;
            animation: fadeIn 0.4s ease;
        }

        .sub-menu-container {
            display: flex;
            gap: 25px;
            justify-content: center;
            flex-wrap: wrap;
            width: 100%;
        }

        .quebra-linha {
            width: 100%;
            display: flex;
            justify-content: center;
            margin-top: 10px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .modal-overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(4px);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal-content {
            background-color: var(--branco);
            color: #333;
            padding: 40px;
            border-radius: 20px;
            width: 90%;
            max-width: 700px;
            max-height: 85vh;
            overflow-y: auto;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .lista-opcoes { list-style: none; padding: 0; margin: 20px 0; }
        .lista-opcoes li {
            background: var(--cinza-claro);
            margin: 10px 0; padding: 18px;
            border-radius: 10px; cursor: pointer;
            font-weight: bold; color: var(--azul-petroleo);
            transition: var(--transicao);
            border-left: 6px solid var(--azul-petroleo);
            text-align: left;
        }

        .lista-opcoes li:hover { background: #d1eaea; transform: scale(1.01); padding-left: 25px; }
        
        .perfil-item {
            text-align: left; padding: 15px; margin: 10px 0;
            background: #f9f9f9; border-bottom: 1px solid #eee;
            font-size: 1.1rem; color: #444;
        }

        .btn-voltar {
            margin-top: 25px; background-color: var(--azul-petroleo);
            color: white; border: none; padding: 12px 35px;
            border-radius: 8px; cursor: pointer; font-weight: bold;
            transition: var(--transicao);
        }

        .btn-voltar-submenu {
            background-color: #ffcccc !important;
            color: #990000 !important;
            min-width: 150px !important;
            padding: 15px 30px !important;
            font-size: 1.1rem !important;
        }
    </style>
</head>
<body>

    <header>
        <button id="btn-seta" class="btn-seta-voltar" onclick="voltarInicio()" title="Voltar">←</button>
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQqZZVK8LVpZiZQ433xI3xJ6bloo_5CvD3DhQ&s" alt="Logo SIGO" class="logo">
        <h1>Base de conhecimento SIGO</h1>
    </header>

    <div class="container-botoes" id="container-principal">
        <button id="btn-liberacao" class="btn-principal btn-lateral-esquerda" onclick="mostrarModulos()">Liberação de acessos sistemas SIGO</button>
        <button id="btn-suporte-mestre" class="btn-principal btn-lateral-esquerda" onclick="mostrarSuporte()">Suporte ao Usuário</button>
        <button id="btn-config" class="btn-principal btn-lateral-esquerda" onclick="alert('Módulo em desenvolvimento')">Configurações / Parametrizações SIGO</button>
        <button id="btn-orientacoes" class="btn-principal btn-lateral-esquerda" onclick="alert('Módulo em desenvolvimento')">Orientações recorrentes</button>

        <!-- SUB-MENU SUPORTE AO USUÁRIO -->
        <div id="sub-menu-suporte">
            <button class="btn-principal" onclick="alert('Botão 1 selecionado')">Botão 1</button>
            <button class="btn-principal" onclick="alert('Botão 2 selecionado')">Botão 2</button>
            <button class="btn-principal" onclick="alert('Botão 3 selecionado')">Botão 3</button>
            <button class="btn-principal" onclick="alert('Botão 4 selecionado')">Travas por Especialidade</button>
            <!-- BOTÃO ATUALIZADO ABAIXO -->
            <button class="btn-principal" onclick="abrirMenuTermos()">Termos de compromisso</button>
            <div class="quebra-linha">
                <button class="btn-principal btn-voltar-submenu" onclick="voltarInicio()">VOLTAR</button>
            </div>
        </div>

        <div id="lista-modulos">
            <button id="btn-gercon-master" class="btn-principal" onclick="expandirMenu('gercon')">GERCON</button>
            <button id="btn-gerint-master" class="btn-principal" onclick="expandirMenu('gerint')">GERINT</button>
            <div id="outros-modulos" style="display: flex; gap: 25px; justify-content: center; flex-wrap: wrap;">
                <button class="btn-principal" onclick="abrirMenu('GERPAC')">GERPAC</button>
            </div>

            <div id="sub-menu-gercon" class="sub-menu-container" style="display: none;">
                <button class="btn-principal" onclick="abrirMenu('GERCON')">GERCON</button>
                <button class="btn-principal" onclick="abrirMenu('GERCON - TRS')">GERCON - TRS</button>
                <div class="quebra-linha">
                    <button class="btn-principal btn-voltar-submenu" onclick="voltarMenuMaster()">VOLTAR</button>
                </div>
            </div>

            <div id="sub-menu-gerint" class="sub-menu-container" style="display: none;">
                <button class="btn-principal" onclick="abrirMenu('GERINT')">GERINT</button>
                <button class="btn-principal" onclick="abrirMenu('GERINT - FATURAMENTO')">GERINT - FATURAMENTO</button>
                <div class="quebra-linha">
                    <button class="btn-principal btn-voltar-submenu" onclick="voltarMenuMaster()">VOLTAR</button>
                </div>
            </div>
        </div>
    </div>

    <div id="modal" class="modal-overlay">
        <div class="modal-content" id="modal-body"></div>
    </div>

    <script>
        const modal = document.getElementById('modal');
        const modalBody = document.getElementById('modal-body');
        const btnSeta = document.getElementById('btn-seta');

        const perfisExecutanteTRS = ["NIR e Administrativo de Unidade Executante"];
        const perfisRegulacaoTRS = ["Profissional Regulador"];
        const perfisPadraoTRS = ["Administrativo de Unidade Executante", "Administrativo de Secretaria de Saúde"];

        const baseDados = {
            "GERCON": {
                "Solicitante": ["Administrativo de Secretaria de Saúde", "Administrativo de Unidade Solicitante"],
                "Executante": ["Administrativo de Unidade Executante", "NIR (Para cadastro de Regularização do Acesso)"],
                "Regulação": ["Profissional Regulador (Médicos)", "Apoio à Regulação (Administrativos de Apoio à Regulação)", "Administrativo de Central de Regulação (Administrativos Operacionais)"],
                "Visualização": ["Consultor (Visualiza informações Clínicas)", "Visualizador (NÃO visualiza informações Clínicas)"]
            },
            "GERCON - TRS": {
                "POLICLINICA ESTADUAL DA REGIAO SAO PATRICIO - GOIANESIA": perfisExecutanteTRS,
                "POLICLINICA ESTADUAL DA REGIAO DO ENTORNO - FORMOSA": perfisExecutanteTRS,
                "POLICLINICA ESTADUAL DA REGIAO NORDESTE POSSE": perfisExecutanteTRS,
                "POLICLINICA ESTADUAL DA REGIAO SUDOESTE- QUIRINOPOLIS": perfisExecutanteTRS,
                "CLIMER - ÁGUAS LINDAS DE GOIÁS": perfisExecutanteTRS,
                "COMPLEXO REGULADOR ANAPOLIS": perfisRegulacaoTRS,
                "COMPLEXO REGULADOR REGIONAL SAO PATRICIO - CERES": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO DR EDSON ORLANDO DE OLIVEIRA - CATALÃO": perfisRegulacaoTRS,
                "COMPLEXO REGULADOR MUNICIPAL DE GOIÂNIA": perfisRegulacaoTRS,
                "COMPLEXO REGULADOR REGIONAL DE IPORA": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO DE ITUMBIARA": perfisRegulacaoTRS,
                "COMPLEXO REGULADOR REGIONAL SUDOESTE II (JATAÍ)": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO DE LUZIANIA SISREG - LUZIANIA": perfisRegulacaoTRS,
                "REGULACAO DE SERVICOS DE SAUDE SAO LUIS DE M BELOS GO": perfisRegulacaoTRS,
                "COMPLEXO REGULADOR REGIONAL SERRA DA MESA - URUAÇU": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO DE SERVICOS DE SAUDE - APARECIDA DE GOÂNIA": perfisRegulacaoTRS,
                "COMPLEXO REGULADOR MUNICIPAL DE RIO VERDE": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO MEDICA DAS URGENCIAS DE PORANGATU": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO - CALDAS NOVAS": perfisRegulacaoTRS,
                "CENTRAL DE REGULACAO DE VALPARAISO DE GOIAS": perfisRegulacaoTRS,
                "DEMAIS UNIDADES COM O TERMO DA TRS": perfisPadraoTRS
            },
            "GERINT": {
                "Solicitante": ["Apoio de Unidade Solicitante"],
                "Executante": ["Apoio de Unidade Executante"],
                "Regulação": ["Profissional Regulador (Médicos)", "Apoio à Regulação (Administrativos de Apoio à Regulação)", "Administrativo de Central de Regulação (Administrativos Operacionais)"],
                "Visualização": ["Consultor (Visualiza informações Clínicas)", "Visualizador (NÃO visualiza informações Clínicas)"]
            },
            "GERINT - FATURAMENTO": {
                "Executante - Faturamento": ["Faturamento"],
                "Regulação": [
                    "Avaliador (Médicos Autorizadores)", 
                    "Administrador NACH (Operacional Regulação)", 
                    "Apoio à avaliação (Administrativos de Apoio a avaliação)"
                ]
            },
            "GERPAC": {
                "Executante": ["Profissional de Apoio - Executante"],
                "Regulação": ["Profissional Autorizador", "Apoio à Autorização", "Administrador de Central de Autorização"],
                "Visualização": ["Consultor (Visualiza informações Clínicas)", "Visualizador (NÃO visualiza informações Clínicas)"]
            }
        };

        function mostrarModulos() {
            esconderBotoesIniciais();
            document.getElementById('lista-modulos').style.display = 'flex';
            btnSeta.style.display = 'flex';
        }

        function mostrarSuporte() {
            esconderBotoesIniciais();
            document.getElementById('sub-menu-suporte').style.display = 'flex';
            btnSeta.style.display = 'flex';
        }

        function esconderBotoesIniciais() {
            document.getElementById('btn-liberacao').style.display = 'none';
            document.getElementById('btn-suporte-mestre').style.display = 'none';
            document.getElementById('btn-config').style.display = 'none';
            document.getElementById('btn-orientacoes').style.display = 'none';
        }

        function expandirMenu(tipo) {
            document.getElementById('btn-gercon-master').style.display = 'none';
            document.getElementById('btn-gerint-master').style.display = 'none';
            document.getElementById('outros-modulos').style.display = 'none';
            
            if(tipo === 'gercon') {
                document.getElementById('sub-menu-gercon').style.display = 'flex';
            } else if(tipo === 'gerint') {
                document.getElementById('sub-menu-gerint').style.display = 'flex';
            }
        }

        function voltarMenuMaster() {
            document.getElementById('btn-gercon-master').style.display = 'block';
            document.getElementById('btn-gerint-master').style.display = 'block';
            document.getElementById('outros-modulos').style.display = 'flex';
            document.getElementById('sub-menu-gercon').style.display = 'none';
            document.getElementById('sub-menu-gerint').style.display = 'none';
        }

        function voltarInicio() {
            voltarMenuMaster();
            document.getElementById('btn-liberacao').style.display = '';
            document.getElementById('btn-suporte-mestre').style.display = '';
            document.getElementById('btn-config').style.display = '';
            document.getElementById('btn-orientacoes').style.display = '';
            
            document.getElementById('lista-modulos').style.display = 'none';
            document.getElementById('sub-menu-suporte').style.display = 'none';
            btnSeta.style.display = 'none';
        }

        function abrirMenu(modulo) {
            let html = `<h2>Opções ${modulo}</h2><p>Selecione uma opção:</p><ul class="lista-opcoes">`;
            if(baseDados[modulo]) {
                Object.keys(baseDados[modulo]).forEach(opcao => {
                    html += `<li onclick="exibirPerfis('${modulo}', '${opcao}')">${opcao}</li>`;
                });
            }
            html += `</ul><button class="btn-voltar" onclick="fechar()">Sair</button>`;
            modalBody.innerHTML = html;
            modal.style.display = 'flex';
        }

        // NOVA FUNÇÃO PARA O MODAL DE TERMOS
        function abrirMenuTermos() {
            let html = `
                <h2>Termos de Compromisso</h2>
                <p>Selecione o documento para visualizar:</p>
                <ul class="lista-opcoes">
                    <li onclick="window.open('https://goiasgovbr-my.sharepoint.com/:b:/g/personal/klisman_sousa_fornecedores_goias_gov_br/IQB-V3A-HbV5RaU-Xn2au-QbARiASl5TGlz9SO6LfBTuKQk?e=yIf9Ik', '_blank')">📄 GERCON e GERINT</li>
                    <li onclick="window.open('https://goiasgovbr-my.sharepoint.com/:b:/g/personal/klisman_sousa_fornecedores_goias_gov_br/IQBaxSFUAH0MToubRoWZ2Xa2AZqaNKi_53c9C8CVEuH8jEM?e=GXQp4r', '_blank')">📄 GERPAC e GERINT FATURAMENTO</li>
                    <li onclick="window.open('https://goiasgovbr-my.sharepoint.com/:b:/g/personal/klisman_sousa_fornecedores_goias_gov_br/IQDso_vbzm4bTKdZ3nqyf6vCAV1gXNGMr7BWITQC6zNUkZE?e=4rAJ0U', '_blank')">📄 GERCON TRS</li>
                    <li onclick="window.open('https://goiasgovbr-my.sharepoint.com/:b:/g/personal/klisman_sousa_fornecedores_goias_gov_br/IQDenW1E7tLySq5emFmqArybAVKTKNOq3zm92jkF73wzoiM?e=j6y03V', '_blank')">📄 REGNET</li>
                </ul>
                <button class="btn-voltar" onclick="fechar()">Sair</button>
            `;
            modalBody.innerHTML = html;
            modal.style.display = 'flex';
        }

        function exibirPerfis(modulo, categoria) {
            const perfis = baseDados[modulo][categoria];
            let html = `<h2>${categoria}</h2><p>Módulo: ${modulo}</p><div>`;
            perfis.forEach(p => {
                html += `<div class="perfil-item">✔️ ${p}</div>`;
            });
            html += `</div><button class="btn-voltar" onclick="abrirMenu('${modulo}')">Voltar</button>`;
            modalBody.innerHTML = html;
        }

        function fechar() { modal.style.display = 'none'; }
        window.onclick = (e) => { if (e.target == modal) fechar(); }
    </script>
</body>
</html>
