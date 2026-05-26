# 🇯🇵 Teste de Nivelamento — Japonês

Um aplicativo web interativo de página única (Single Page Application) desenvolvido para avaliar o nível de proficiência em língua japonesa (equivalente do N5 ao N1 do JLPT). O projeto é executado de forma estática no **GitHub Pages** e envia de maneira integrada os resultados dos participantes diretamente para uma planilha do **Google Sheets**.

---

## 🚀 Funcionalidades

- **30 Questões Progressivas:** Divisão metodológica que cobre conteúdos de vocabulário, gramática e interpretação de texto do nível básico (N5) ao avançado (N1).
- **Embaralhamento Inteligente de Alternativas:** Sistema dinâmico que reorganiza as opções de resposta (A, B, C, D) de forma aleatória a cada carregamento de página, mantendo o gabarito intacto (anti-cola).
- **Tempo Limite de 30 Minutos:** Cronômetro regressivo integrado no cabeçalho fixo com alerta visual (muda de cor nos 5 minutos finais) e envio automático do teste ao zerar o tempo.
- **Visualização Responsiva e Minimalista:** Design polido com paleta de cores neutras, tipografia elegante utilizando fontes japonesas e adaptabilidade completa para celulares, tablets e computadores.
- **Integração Direta com Google Sheets:** Envio assíncrono dos resultados utilizando requisições `fetch` estruturadas para processamento seguro via Google Apps Script.
- **Card de Pré-visualização para WhatsApp:** Configuração de metadados Open Graph para gerar pré-visualizações completas com título, descrição e imagem ao compartilhar o link.

---

## 🛠️ Arquitetura do Projeto

O sistema é dividido em duas partes integradas:

1. **Frontend (GitHub Pages):** 
   - Arquivo `index.html` contendo a marcação estrutural, estilização CSS e inteligência em JavaScript.
   - Faz a renderização das perguntas, controle do tempo, embaralhamento e montagem do pacote de dados (*payload*).
   
2. **Backend (Google Apps Script):**
   - Script associado a uma planilha do Google Sheets que disponibiliza um endpoint seguro por método `POST`.
   - Recebe o pacote de dados do teste em formato JSON e o adiciona como uma nova linha na planilha em tempo real.

---

## 🧠 Critérios de Avaliação

O sistema classifica o participante de forma automatizada com base na pontuação geral obtida:

- **Até 10 acertos (≤ 35%):** Iniciante — Equivalente a N5–N4
- **De 11 a 19 acertos (36% - 65%):** Intermediário — Equivalente a N3–N4
- **De 20 a 25 acertos (66% - 85%):** Avançado — Equivalente a N2
- **De 26 a 30 acertos (> 85%):** Fluente / Expert — Equivalente a N1

---

## ⚙️ Instruções de Configuração

### 1. Preparação da Planilha (Google Sheets)
1. Crie uma nova planilha no seu Google Drive.
2. Na barra de ferramentas superior, acesse **Extensões > Apps Script**.
3. Substitua o código existente pela função de processamento `doPost(e)` que recebe e escreve os dados JSON na planilha.
4. Clique em **Implantar > Nova implantação**, configure o acesso como "Aplicativo da Web", escolha executar como "Eu" e defina o acesso para "Qualquer pessoa".
5. Copie a **URL do aplicativo da Web** gerada.

### 2. Configuração do Frontend (GitHub)
1. No seu arquivo `index.html`, localize a constante `SHEET_URL` nas primeiras linhas do script:
   ```javascript
   const SHEET_URL = "SUA_URL_DO_APPS_SCRIPT_AQUI";
