# Plano de Teste — Shortz-App

## 1. Identificação
- **Projeto:** Shortz-App
- **Versão:** 1.0 (Módulo de Usuários e Autenticação)
- **Grupo:** Stéfani Paula Sant'ana Cruz
- **Data de criação:** 17/03/2026
- **Objetivo:** Este plano de teste tem como objetivo definir o escopo, a estratégia, os riscos e os critérios de verificação das funcionalidades do Shortz-App. Nesta fase, o foco principal será o módulo de usuários e autenticação, buscando detectar defeitos nas funcionalidades de cadastro, login, logout, sessão e edição de perfil antes da entrega da atividade.

## 2. Escopo

### O que SERÁ testado
- Cadastro de usuário
- Validação de campos obrigatórios no cadastro
- Validação de unicidade de nome de usuário e e-mail
- Login com e-mail e senha
- Login com nome de usuário e senha
- Manutenção de sessão autenticada
- Logout
- Controle de acesso a rotas protegidas
- Visualização de perfil próprio e de outros usuários
- Edição de perfil (nome completo, biografia e foto)
- Validação de tamanho e formato da foto de perfil
- Feedback visual de sucesso e erro nas telas de autenticação e perfil

### O que NÃO será testado (nesta fase)
- Testes de carga e performance
- Streaming de vídeo
- Upload de vídeo
- Feed priorizado/global
- Busca de conteúdo
- Curtidas e comentários
- Playlists
- Notificações
- Painel administrativo completo
- Testes E2E completos com navegador

## 3. Estratégia

### Níveis de Teste
- **Unitários:** validação de e-mail, validação de senha, validação de tamanho da biografia, validação de formato/tamanho da foto de perfil, regras de sessão e autenticação.
- **Integração:** rotas de cadastro, login, logout, edição de perfil e acesso a rotas protegidas, verificando integração entre controller, serviço, banco de dados e sessão.
- **Sistema/Manual:** fluxo de cadastro, login, logout e edição de perfil, com base nos protótipos das telas.

### Técnicas de Teste
- Partição de equivalência
- Análise de valor-limite
- Tabela de decisão
- Teste exploratório
- Testes de cenários de sucesso, falha e borda

### Ferramentas
- Vitest
- GitHub Actions

## 4. Riscos Identificados

| ID | Descrição | Categoria | Prob. | Impacto | Prioridade |
|----|-----------|-----------|-------|---------|------------|
| R-01 | Cadastro permite e-mail em formato inválido | Funcional | Alta | Alto | Crítica |
| R-02 | Cadastro permite nome de usuário duplicado | Funcional | Média | Alto | Alta |
| R-03 | Cadastro permite e-mail duplicado | Funcional | Média | Alto | Alta |
| R-04 | Senha é armazenada sem hash no banco de dados | Não-Funcional (Segurança) | Média | Crítico | Crítica |
| R-05 | Login aceita credenciais inválidas | Funcional | Média | Crítico | Crítica |
| R-06 | Sessão não é mantida após login com “lembrar-me” | Funcional | Média | Médio | Média |
| R-07 | Logout não encerra corretamente a sessão | Funcional | Média | Alto | Alta |
| R-08 | Rotas protegidas podem ser acessadas sem autenticação | Funcional / Segurança | Média | Crítico | Crítica |
| R-09 | Biografia aceita texto acima do limite permitido | Funcional | Média | Médio | Média |
| R-10 | Upload de foto de perfil aceita arquivo fora do formato permitido | Funcional | Média | Alto | Alta |
| R-11 | Upload de foto de perfil aceita arquivo acima de 4MB | Funcional | Média | Médio | Média |
| R-12 | Campo de biografia ou nome completo permite XSS | Não-Funcional (Segurança) | Média | Alto | Crítica |

## 5. Estratégia de Mitigação dos Riscos Prioritários
- **R-01:** testes unitários e de integração para validar formatos válidos, inválidos e vazios de e-mail.
- **R-04:** teste de integração verificando que o valor armazenado no banco não corresponde à senha em texto puro.
- **R-05:** testes de integração com combinações válidas e inválidas de login.
- **R-08:** testes de integração acessando rotas protegidas sem cookie/token de sessão.
- **R-12:** testes de segurança e teste exploratório com inserção de scripts em campos textuais.

## 6. Recursos e Ambiente
- **Ambiente:** Node.js 20+, MySQL local ou SQLite em memória para testes, Vitest + Supertest.
- **Dados de teste:** fixtures com usuários válidos, usuários duplicados, credenciais inválidas, perfis com e sem foto.
- **Repositório:** GitHub, com branches por funcionalidade e revisão via pull request.
- **CI:** GitHub Actions executando a suíte de testes a cada push.
- **Equipe:** todos os integrantes participam da escrita, revisão e execução dos testes.

## 7. Cronograma

| Semana | Atividade | Entrega |
|--------|-----------|---------|
| 4 | Protótipo do Plano de Teste | `tests/manuais/plano-de-teste.md` |
| 5 | Especificação de casos de teste manuais | `tests/manuais/casos-de-teste.md` |
| 6 | Revisão e entrega final do Plano de Teste | Entrega 1 |
| 7 | Implementação de testes unitários principais | suíte inicial |
| 8 | Implementação de testes de integração do módulo de autenticação | suíte ampliada |

## 8. Critérios de Entrada, Saída e Suspensão
- **Entrada:** ambiente configurado, banco de testes disponível, build executando sem erro, requisitos do módulo de autenticação definidos.
- **Saída:** zero falhas em testes de prioridade Crítica; zero falhas bloqueadoras em autenticação; cobertura mínima de 70% no módulo de usuários e autenticação; plano revisado pela equipe.
- **Suspensão:** falha grave no ambiente, indisponibilidade do banco de testes, erro estrutural que impeça execução da suíte, ausência de requisitos mínimos para validar o comportamento esperado.

## 9. Referências
- Especificação do Software Shortz-App
- Protótipos de Telas - Shortz-App
- Apostila Aula 03 - Tipos de Teste e Plano de Testes
- Apostila Aula 04 - Planejamento de Testes
