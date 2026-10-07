# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<img width="600" height="150" alt="Image" src="https://github.com/user-attachments/assets/5746c27f-0276-4eb3-b7da-6f249578a58d" /></a>
</p>

<br>

# 🎓 Graduação ON em Inteligência Artificial  
## 📚 Cap 1 - A Busca de Dados: Preparando o Terreno para a Inteligência Cardiológica

## 👨‍🎓 Integrantes: 
- <a href="https://www.linkedin.com/in/paulo-pereira-de-souza-junior-mba-msc-0b497825/">Paulo Pereira de Souza Junior</a>

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
   
<img width="220" height="140" alt="Image" src="https://github.com/user-attachments/assets/0ac0c841-19c0-4413-a489-17b4f19ebc6c" />
