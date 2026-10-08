# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<img width="600" height="150" alt="Image" src="https://github.com/user-attachments/assets/5746c27f-0276-4eb3-b7da-6f249578a58d" /></a>
</p>

<br>

# 🎓 Graduação ON em Inteligência Artificial  
## 📚  FASE 2: Diagnóstico Automatizado – IA no Estetoscópio Digital

## 👨‍🎓 Integrantes: 
- <a href="https://www.linkedin.com/in/paulo-pereira-de-souza-junior-mba-msc-0b497825/">Paulo Pereira de Souza Junior</a>

## 👨‍🎓 Apresentacao: 
- <a href="https://youtu.be/AEN0-wvo57s">Video Apresentação - YOUTUBE</a>

## 📚  Objetivo

Nesta etapa trabalharemos com 2 exercicios, o objetivo central destas duas atividades é simular o funcionamento de um sistema inteligente de triagem e apoio ao diagnóstico médico através do processamento de linguagem natural e da estruturação de dados em Python. O processo inicia-se com a análise de relatos textuais de pacientes para a extração automática de sintomas, os quais são mapeados e armazenados num ficheiro tabular de modo a expandir a base de conhecimento do sistema e sugerir diagnósticos preliminares. Em seguida, essa análise evolui para o desenvolvimento de um classificador de texto focado na avaliação da gravidade das expressões extraídas, permitindo categorizar os pacientes entre baixo e alto risco para simular a priorização de atendimentos num cenário real de triagem clínica.

## 📚 Lista de Doenças e Sintomas

Lista de sintomas com possiveis doenças, consideramos 2 sintomas principais para direcionamento do diagnostico, a figura abaixo apresenta a estrutura da tabela principal.

<img width="734" height="241" alt="Image" src="https://github.com/user-attachments/assets/41af0e81-fdd1-4cbb-8f93-73d717fc82a0" />

## 📚 Relato de Pacientes

Lista de relato de pacientes contendo informações de sintomas e informações para análise de criticidade da doença.

<img width="634" height="448" alt="Image" src="https://github.com/user-attachments/assets/f593f19d-51fb-40c2-90e1-5500922910ac" />

## 📚 Tabela de Classificação de Gravidade

A tabela de classificação utiliza palavras-chave para direcionar a análise de gravidade, enquanto o modelo desenvolvido avalia a raiz de cada palavra para identificar e categorizar eficientemente cada relato.

<img width="185" height="308" alt="Image" src="https://github.com/user-attachments/assets/a19a4167-ecdc-467f-bea5-e48e89b99ab7" />

## 📚 Tabela de Diagnostico (Resultados Obtidos)

A tabela de classificação utiliza palavras-chave para direcionar a análise de gravidade, enquanto o modelo desenvolvido avalia a raiz de cada palavra para identificar e categorizar eficientemente cada relato.

#### Coluna Relato:

Descreve o relato do paciente, contendo informações basicas de sintomas, historio e apontamentos para classificação da gravidade da doença identificada.

#### Coluna Sintoma_Principa:

Coluna resultado do modelo de análise de texto, identifica o sintoma principal baseado na tabela "Lista de Doenças e Sintomas", esta coluna é utilizada para definir a doença associada ao relato

#### Coluna doenca_associada:

Esta coluna apresenta a doença associada obtida através do cruzamento entre os sintomas identificados no relato e a tabela de referência "Lista de Doenças e Sintomas".

#### Coluna Nivel_Sintoma:

Esta coluna apresenta o diagnóstico do nível de gravidade do sintoma ou doença, utilizando como referência a "Tabela de Classificação de Gravidade" e avaliando palavras-chave específicas para determinar o risco de cada paciente.

#### Coluna Palavra_Chave_Referencia:

Apresenta a palavra chave identificada e utilizada para classificação do modelo de diagnostico, esta palavra é determinais para avaliação do risco de cada paciente.

#### Coluna Detalhe_Palavras_Localizadas

Esta etapa classifica outras palavras identificadas no relato dos pacientes, avaliando todo o texto para encontrar termos adicionais que ajudem a determinar com maior precisão o nível de risco do paciente.

a tabela a seguir, apresenta a estrutura da tabela resultado e diagnostico 

<img width="812" height="307" alt="Image" src="https://github.com/user-attachments/assets/00d790fe-cc89-42b2-b7b9-3627bd79ceb2" />

## 📚 Mecanismo de Busca por Similaridade (Modelo de Avaliação)
Quando um relato de paciente é processado pela função identificar_sintoma_e_doenca_melhorado:
1. Vetorização do relato: O texto do paciente é limpo e convertido para o mesmo formato matemático (TF-IDF).
2. Cálculo de Similaridade por Cosseno: O código compara o relato do paciente com todos os sintomas da base de dados e calcula uma pontuação de semelhança (cosine_similarity).
3. Filtro de Segurança (Regulador de Score): Se a maior nota de similaridade for menor que 0.25, o sistema considera o relato ambíguo ou inconclusivo e retorna "Sintoma Complexo / Inconclusivo" com a orientação "Encaminhar para Avaliação Médica Detalhada".
4. Cruzamento de Dados: Se passar no filtro, o código descobre qual é o sintoma mais parecido, faz uma busca no DataFrame de referência (sintomas_doencas) e encontra a respetiva Doenca_Associada.

A figura a seguir apresenta a estrutura principal do algoritmo.
<img width="590" height="278" alt="Image" src="https://github.com/user-attachments/assets/6e9a9f68-2471-4189-8d34-6f34ba4fdc7c" />

## 📚 Rotulagem Inicial por Palavras-Chave e Radical
A função analisa o relato de cada paciente utilizando um dicionário de referência (ref_avaliacao):

Limpeza e Radical (Stemming básico): O código limpa o texto e verifica se a palavra-chave está presente de forma exata ou se o seu radical (os primeiros 5 caracteres, como complic, sangr) aparece em algum termo do relato.

Hierarquia de Gravidade: Se um relato contiver múltiplas palavras-chave, o código prioriza o nível mais crítico encontrado. A ordem de prioridade é: Grave/Forte → Moderado → Leve (ou qualquer outro nível inicial).

1. Preparação e Filtragem dos Dados de Treino
   
• O código isola apenas os relatos que foram classificados com sucesso pelas palavras-chave para servirem como a base de treino do modelo.

• Filtro de segurança: Ele remove automaticamente do treino as classes (níveis de gravidade) que aparecem menos de duas vezes. Isto garante que o algoritmo tenha dados suficientes para aprender e permite realizar a divisão de validação.

2. Vetorização Avançada com TF-IDF
   
• Utiliza a lista de STOP_WORDS_PT para ignorar palavras que não trazem contexto clínico (como "ao", "da", "numa").

• Configura o TfidfVectorizer com trigramas (ngram_range=(1, 3)). Isto significa que o modelo vai analisar palavras isoladas, pares e expressões de até três palavras combinadas (ex: "muita dor de", "falta de ar"), tornando a interpretação do contexto do paciente muito mais rica.

3. Treinamento e Avaliação do Modelo Inteligente

• Divisão Estratificada: O código divide os dados em treino (80%) e teste (20%) de forma proporcional (stratify=y), garantindo que as classes de risco estejam igualmente distribuídas em ambas as partes.

• Random Forest: O modelo de florestas aleatórias é configurado com class_weight="balanced", o que corrige automaticamente o desequilíbrio caso existam muito mais relatos de "baixo risco" do que de "alto risco" na base de dados.

• Relatório de Métricas: Avalia o desempenho imprimindo a precisão e a cobertura (classification_report) com os dados de teste que o modelo nunca viu antes.

<img width="710" height="359" alt="Image" src="https://github.com/user-attachments/assets/521e0da6-5861-4821-92c4-42bd851d8080" />

## 📚 Rotulagem Inicial por Palavras-Chave e Radical (Acurácia do Modelo)

O Diagnóstico do Desempenho

Análise das Métricas:
   
	• Fraco (F1-Score: 0.67): O modelo acertou o caso "Fraco", obtendo 100% de recall (encontrou o que devia), mas a precisão foi de 50% porque ele provavelmente classificou tudo como "Fraco".

	• Forte (F1-Score: 0.00): O modelo errou o único caso "Forte" do teste, classificando-o incorretamente como "Fraco".

	• Exatidão (Accuracy) de 50%: Significa que, na prática, o modelo acertou metade das previsões (1 de 2 frases).

<img width="431" height="233" alt="Image" src="https://github.com/user-attachments/assets/2a27336b-907d-45b0-86c5-50233d595f19" />
