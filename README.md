# 🤖 Agente de IA para WhatsApp com n8n

Um chatbot inteligente para WhatsApp construído com n8n que usa IA para responder mensagens automaticamente. O bot registra conversas no Google Sheets e utiliza ferramentas de IA como Wikipedia e Calculadora para fornecer respostas úteis. Criado com fins didáticos para consolidar o aprendizado em automações usando a ferramenta n8n.

## 📋 Visão Geral

Este workflow n8n cria um assistente automatizado para WhatsApp que:
- Recebe mensagens de WhatsApp via webhook
- Filtra mensagens de grupos, newsletters e transmissões
- Armazena informações de contato no Google Sheets
- Usa IA para gerar respostas humanizadas
- Mantém contexto de conversação com memória
- Envia respostas automatizadas de volta aos usuários

## 📊 Fluxo de Dados

1. **Mensagem Recebida** → Z-API envia requisição POST para o webhook
2. **Filtragem** → Apenas mensagens individuais, não de grupos, passam
3. **Extração de Dados** → Número de telefone, mensagem e nome são extraídos
4. **Armazenamento de Contato** → Informações do contato salvas/atualizadas no Google Sheets
5. **Processamento IA** → Mensagem enviada ao agente IA com contexto
6. **Uso de Ferramentas** → IA pode usar Wikipedia ou Calculadora se necessário
7. **Geração de Resposta** → IA cria resposta humanizada
8. **Mensagem Enviada** → Resposta enviada de volta via Z-API
