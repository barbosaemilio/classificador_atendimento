HospTech Triagem IA

Projeto desenvolvido durante o curso Programação em Inteligência Artificial Generativa (40h) - SENAI , com o objetivo de aplicar na prática os conceitos de integração com modelos de IA generativa via API, construção de back-end em Python e deploy de aplicações web.

Sobre o projeto

O sistema simula uma triagem hospitalar inteligente: o usuário descreve os sintomas do paciente em um formulário, e um modelo de IA generativa analisa o relato e retorna a especialidade médica recomendada, o nível de prioridade do atendimento (Emergência, Urgência ou Pouco Urgente) e uma justificativa clínica breve — tudo em formato JSON estruturado.

Back-end

O back-end foi construído em Python, utilizando o micro-framework Flask para expor a rota da aplicação e servir o front-end.

Principais bibliotecas utilizadas:

Flask — criação da aplicação web, rotas e renderização de templates
Requests — comunicação HTTP com a API da OpenRouter
json (biblioteca padrão) — interpretação e validação das respostas em JSON retornadas pela IA
os (biblioteca padrão) — leitura de variáveis de ambiente, como a chave de API
Gunicorn — servidor WSGI utilizado em produção no deploy

O fluxo da aplicação recebe o relato de sintomas via requisição POST, monta um prompt de sistema com as regras de triagem (especialidades e níveis de prioridade permitidos), envia a requisição para a API da OpenRouter e trata a resposta, validando os campos obrigatórios antes de devolver o resultado ao front-end. O código também trata erros comuns, como timeout, falhas HTTP da API e respostas fora do formato esperado.

Modelos de IA generativa (OpenRouter)

A integração com a inteligência artificial é feita através da OpenRouter, uma plataforma que unifica o acesso a diversos modelos de IA generativa de diferentes provedores por meio de uma única API.

Durante o desenvolvimento, o projeto utilizou modelos disponíveis na camada gratuita (:free) da OpenRouter, entre eles:

inclusionai/ling-3.0-flash:free
nvidia/nemotron-3-ultra-550b-a55b:free

Um ponto de aprendizado importante do projeto foi lidar com a rotatividade dos modelos gratuitos: a OpenRouter atualiza periodicamente sua lista de modelos disponíveis sem custo, podendo descontinuar ou migrar modelos para a camada paga. Isso exigiu monitoramento e ajustes no código para trocar o modelo configurado sempre que necessário, reforçando a importância de tratamento de erros e de manter o back-end flexível quanto ao modelo utilizado.

Front-end

A interface foi construída com HTML e estilizada com o framework Bootstrap, garantindo um layout responsivo e organizado sem a necessidade de escrever CSS extenso do zero. O front-end é responsável por:

Apresentar o formulário de entrada dos sintomas do paciente
Enviar a requisição para o back-end via fetch
Exibir o resultado da triagem (especialidade, prioridade e justificativa)
Apresentar uma legenda explicativa dos níveis de prioridade
Deploy

A aplicação foi publicada na plataforma Render, com o seguinte fluxo de deploy:

Build automático a partir do repositório no GitHub
Instalação das dependências listadas no requirements.txt
Execução da aplicação em produção com Gunicorn
Configuração da chave da API da OpenRouter como variável de ambiente (OPENROUTER_API_KEY), mantendo a credencial fora do código-fonte
Aprendizados

Este projeto consolidou, na prática, conceitos como:

Consumo de APIs de IA generativa e engenharia de prompt para obter respostas estruturadas em JSON
Tratamento de erros em integrações externas (timeout, erros HTTP, respostas inválidas)
Organização de um back-end Flask simples e funcional
Deploy de aplicações Python em ambiente de produção
Boas práticas de versionamento com Git/GitHub
