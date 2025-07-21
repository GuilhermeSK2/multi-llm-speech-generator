# Gerador de Discursos com Múltiplos LLMs (Streamlit, Gemini e Ollama)

Este projeto implementa um aplicativo web interativo que demonstra como combinar e orquestrar diferentes Large Language Models (LLMs) em uma cadeia de processamento. Ele utiliza o Streamlit para a interface, o Google Gemini (via API) para gerar o título de um discurso, e o modelo Mistral (executando localmente via Ollama) para escrever o discurso completo.

## Visão Geral

A orquestração de múltiplos LLMs é uma técnica avançada que permite aproveitar os pontos fortes de diferentes modelos para tarefas específicas dentro de um fluxo de trabalho. Neste projeto, o processo é o seguinte:

1.  **Entrada do Usuário:** O usuário fornece um `tópico` para o discurso através de uma interface Streamlit.
2.  **Primeira Cadeia (Geração de Título - LLM via API):**
    * Uma `PromptTemplate` instrui o modelo Google Gemini (`gemini-2.5-flash`), acessado via API, a atuar como um "escritor de discursos experiente".
    * O Gemini gera um **título único e impactante** com base no `tópico` fornecido.
    * Um `StrOutputParser` garante que apenas a string do título seja retornada.
    * O título gerado é exibido imediatamente na interface do Streamlit.
3.  **Segunda Cadeia (Geração de Discurso - LLM Local):**
    * A saída da primeira cadeia (o título gerado) é passada como entrada para a segunda cadeia.
    * Uma nova `PromptTemplate` instrui o modelo Mistral (executando localmente via Ollama) a escrever um **discurso de 350 palavras** com base nesse `título`.
4.  **Cadeia Final e Exibição:** As duas cadeias são encadeadas. O discurso completo gerado pelo Mistral é então exibido na interface do Streamlit.

Esta arquitetura demonstra uma abordagem híbrida, utilizando recursos de nuvem (Gemini API) e modelos locais (Ollama) de forma eficiente.

## Estrutura do Projeto

* `multiple_llms_demo.py`: O script principal do aplicativo Streamlit.

## Tecnologias Utilizadas

* **Python 3**
* **Streamlit**: Para construir a interface web interativa.
* **LangChain Google Generative AI (`langchain_google_genai`)**: Para interagir com o modelo Gemini.
* **LangChain Ollama (`langchain_ollama`)**: Para interagir com LLMs locais via Ollama.
* **LangChain PromptTemplate**: Para criar prompts estruturados.
* **LangChain Core Output Parsers (`StrOutputParser`)**: Para formatar a saída das cadeias.
* **Google Gemini API**: Para o modelo de linguagem (`gemini-2.5-flash`).
* **Ollama**: Plataforma para executar LLMs localmente.
* **Mistral**: Modelo de linguagem grande (LLM) executado via Ollama.


## Uso do Aplicativo

Na interface do Streamlit, você encontrará um campo de texto para inserir o tópico do discurso. Digite o tópico desejado (ex: "O futuro do trabalho remoto" ou "A importância da sustentabilidade") e, em seguida, o aplicativo gerará e exibirá o título (via Gemini) e o discurso completo (via Mistral).

## Exemplo de uso:

<img width="642" height="918" alt="Image" src="https://github.com/user-attachments/assets/bd4f84c9-6c5c-4f78-9f10-2ab098cbe14d" />
