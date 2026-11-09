# Cannot Get

## Visão geral

Solução de automação para receber imagens, vídeos e GIFs pelo WhatsApp, processar as mídias e devolver figurinhas. O projeto também contempla integrações controladas para publicação de mídia em destinos autorizados.

## Problema

O processamento de mídia em serviços de mensageria envolve eventos assíncronos, limites de tamanho, falhas de download, duplicidades e risco de envio indevido. A solução organiza esse caminho em componentes separados e adiciona controles operacionais.

## Funcionalidades implementadas

- Recepção de eventos e mídias por WhatsApp.
- Integração com n8n por webhooks.
- Conversão de imagem, vídeo e GIF para WebP com FFmpeg.
- Filas com limite e controle de concorrência.
- Deduplicação de mensagens e respostas.
- Rate limiting por remetente.
- Limites de tamanho e duração de mídia.
- Allowlist de destinos e modo de execução sem envio real.
- Métricas de fila, healthchecks e logs para diagnóstico.

## Duas arquiteturas independentes

### OpenWA

Ponte própria em **Node.js, Express e whatsapp-web.js**, responsável pela sessão do WhatsApp, recepção de eventos, fila de entrada, encaminhamento ao n8n e envio da figurinha processada.

### Evolution API

Fluxo separado baseado em **Evolution API, Baileys e n8n**, utilizando webhook de mensagens, obtenção de mídia, validação, conversão e envio da figurinha pela API.

OpenWA e Evolution API são integrações distintas e não compartilham a mesma implementação.

## Infraestrutura e tecnologias

**Node.js, JavaScript, n8n, OpenWA, whatsapp-web.js, Evolution API, Baileys, Docker, FFmpeg, webhooks e APIs REST.**

Os serviços são separados em contêineres e possuem restrições de filesystem, recursos, privilégios e exposição de portas. O conversor utiliza diretórios temporários e remove os arquivos após cada processamento.

## Diagnóstico e confiabilidade

O projeto exigiu investigação de falhas distribuídas por meio da correlação entre logs, webhooks, filas, execuções n8n e processamento de mídia. Um endpoint saudável ou uma sessão conectada não foram tratados como prova de funcionamento ponta a ponta.

## Atuação

Definição dos fluxos, integração dos serviços, implementação de guardrails, diagnóstico de incidentes e evolução das regras de uso. A atuação combina automação, integração de APIs e resolução de problemas em sistemas distribuídos.

## Status

Piloto operacional em evolução. O código e os ambientes são privados por conterem configurações e integrações sensíveis.
