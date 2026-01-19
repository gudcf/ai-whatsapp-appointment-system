# 🤖 High-Performance AI Scheduling Architecture

> **Technical Showcase / Proof of Concept**
> Arquitetura de microsserviços orientada a eventos projetada para automatizar agendamentos via WhatsApp em alta escala.

---

## 🎯 O Objetivo Técnico
Desenvolver uma solução robusta capaz de escalar o atendimento ao cliente sem aumentar proporcionalmente a equipe humana. O foco deste projeto foi criar uma **arquitetura resiliente**, capaz de lidar com picos de tráfego, garantindo disponibilidade 24/7 e integridade de dados.

* **Stack:** n8n, OpenAI GPT-4, PostgreSQL, Redis, Docker.
* **Capacidade Projetada:** 50.000+ mensagens/mês.
* **Modelo:** Event-Driven Architecture.

---

## 🏗️ Design da Arquitetura

O sistema foi desenhado para eliminar gargalos comuns em automações de WhatsApp (como timeouts e alucinações de IA).

```mermaid
graph TD
    A[WhatsApp Cloud API] -->|Webhook| B(n8n Orchestrator)
    B --> C{Message Buffer / Redis}
    C --> D[AI Processing Agent]
    D <-->|Context| E[(Redis Memory)]
    D <-->|Logic| F[GPT-4o]
    D -->|Tool Call| G[PostgreSQL DB]
    G -->|Availability| D
    D -->|Response| H[WhatsApp Sender]
Componentes Chave
Buffer de Mensagens (Redis): Implementação de fila para garantir que mensagens recebidas fora de ordem (comum em redes móveis) sejam processadas na sequência correta (FIFO).

Memória de Conversa (Sliding Window): O sistema mantém apenas o contexto relevante das últimas interações no Redis, otimizando custos de tokens e latência.

Segurança de Transação: Utilização de Row-Level Locking no PostgreSQL para impedir que dois clientes agendem o mesmo horário simultaneamente durante picos de acesso.

⚡ Diferenciais Técnicos
🗣️ Processamento de Linguagem Natural (NLP)
Integração com Whisper API para transcrição de áudio em tempo real.

Tratamento de gírias e erros de digitação comuns no português brasileiro.

🛡️ Compliance & Estabilidade
Utilização exclusiva da Meta Cloud API (Oficial), eliminando riscos de desconexão associados a bibliotecas de emulação.

Sanitização de inputs para evitar Prompt Injection.

📍 Inteligência Geográfica
Algoritmo implementado para cálculo de distância (Haversine) entre coordenadas do cliente e unidades de atendimento, sugerindo a opção logisticamente mais viável.

📊 Performance (Stress Tests)
Testes de carga e validação técnica demonstraram:

Métrica,Resultado
Throughput,Capaz de processar 50+ conversas simultâneas
Latência Média,< 2 segundos (Round-trip)
Disponibilidade,Arquitetura containerizada pronta para HA (High Availability)
Custo,Otimização de prompts reduziu consumo de tokens em 40%

🛠️ Stack Tecnológica
Orquestração: n8n (Self-hosted para controle total de dados)

AI Core: OpenAI GPT-4o (Function Calling)

Banco de Dados: PostgreSQL (com extensão pgvector)

Cache/Fila: Redis

Infraestrutura: Docker Compose, Nginx (Reverse Proxy)

👨‍💻 Sobre o Desenvolvedor
Gustavo Resende Full Stack Developer & Cloud Infrastructure

Especialista em criar soluções de automação que unem infraestrutura sólida (Docker/Cloud) com as mais recentes capacidades de IA Generativa.
