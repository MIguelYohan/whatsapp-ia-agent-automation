# 🤖 Agente de IA para WhatsApp com n8n

Um chatbot inteligente para WhatsApp construído com n8n que usa IA para responder mensagens automaticamente. O bot registra conversas no Google Sheets e utiliza ferramentas de IA como Wikipedia e Calculadora para fornecer respostas úteis.

## 📋 Visão Geral

Este workflow n8n cria um assistente automatizado para WhatsApp que:
- Recebe mensagens de WhatsApp via webhook
- Filtra mensagens de grupos, newsletters e transmissões
- Armazena informações de contato no Google Sheets
- Usa IA para gerar respostas humanizadas
- Mantém contexto de conversação com memória
- Envia respostas automatizadas de volta aos usuários

## 🏗️ Arquitetura

<img width="795" height="275" alt="Captura de tela 2026-02-04 194824" src="https://github.com/user-attachments/assets/c5701267-6644-47ce-bf5d-aacf35771d5f" />

## 🔧 Componentes

### 1. **Webhook** (Receptor de Mensagens)
- **Endpoint**: `/receber-msg-zapi`
- **Método**: POST
- Recebe mensagens recebidas da integração Z-API WhatsApp

### 2. **Nó If** (Filtro de Mensagens)
Filtra mensagens para processar apenas:
- ✅ Conversas individuais (não grupos)
- ✅ Mensagens regulares (não newsletters)
- ✅ Mensagens iniciadas pelo usuário (não transmissões)
- ✅ Mensagens não-API (não de automação)

### 3. **Edit Fields** (Extração de Dados)
Extrai e formata:
- `NumeroTelefone`: Número de telefone do contato
- `Mensagem`: Texto da mensagem
- `Nome`: Nome do remetente

### 4. **Integração Google Sheets**
- **Documento**: Planilha WppN8N
- **Operação**: Adicionar ou Atualizar
- **Colunas**: Nome, NumWpp
- Mantém um banco de dados de todos os contatos que interagem com o bot

### 5. **Agente IA**
O núcleo de inteligência do bot com:

**Prompt do Sistema**: 
```
Você é um super agente de IA que responde conversas no whatsapp, 
responda de forma humanizada e educada com a utilização de emojis 
e de forma descontraida.
```

**Capacidades**:
- 🧠 **Modelo de Linguagem**: Groq Chat (gpt-oss-safeguard-20b)
- 💾 **Memória**: Buffer window memory (mantém contexto da conversa por usuário)
- 🔧 **Ferramentas**:
  - Wikipedia (para consultas de conhecimento geral)
  - Calculadora (para cálculos matemáticos)

### 6. **HTTP Request** (Enviador de Respostas)
Envia a resposta gerada pela IA de volta via Z-API:
- **Endpoint**: Z-API send-text
- **Autenticação**: Client token incluído nos headers
- **Payload**: Número de telefone + resposta da IA

## 📊 Fluxo de Dados

1. **Mensagem Recebida** → Z-API envia requisição POST para o webhook
2. **Filtragem** → Apenas mensagens individuais, não de grupos, passam
3. **Extração de Dados** → Número de telefone, mensagem e nome são extraídos
4. **Armazenamento de Contato** → Informações do contato salvas/atualizadas no Google Sheets
5. **Processamento IA** → Mensagem enviada ao agente IA com contexto
6. **Uso de Ferramentas** → IA pode usar Wikipedia ou Calculadora se necessário
7. **Geração de Resposta** → IA cria resposta humanizada
8. **Mensagem Enviada** → Resposta enviada de volta via Z-API

## 🎯 Casos de Uso

- **Suporte ao Cliente**: Suporte automatizado de primeira linha para empresas
- **Bot de FAQ**: Responder perguntas comuns automaticamente
- **Assistente Pessoal**: Ajuda com cálculos, busca de informações
- **Captura de Leads**: Coletar e armazenar informações de contato
- **Disponibilidade 24/7**: Responder mensagens mesmo quando você está offline

## 📈 Estrutura do Google Sheets

Sua planilha deve ter estas colunas:

| Nome | NumWpp |
|------|--------|
| João Silva | 5511999999999 |
| Maria Santos | 5511888888888 |

O workflow cria ou atualiza linhas automaticamente com base no número de telefone.

## 📝 Licença

Este projeto é fornecido como está para uso educacional.
## 🤝 Contribuindo

Sinta-se à vontade para fazer fork deste workflow e customizá-lo para suas necessidades. Compartilhe melhorias e casos de uso!
