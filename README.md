# SOS Orçamentos IA - thIAguinho Soluções Digitais

Sistema 100% frontend para orçamento/oficina, inspirado no padrão visual do PDF enviado da S.O.S. Valêncio.

## Arquivos

- `index.html` - sistema principal.
- `config.js` - chaves e dados da oficina.

## Como subir no GitHub Pages

1. Crie um repositório novo.
2. Envie `index.html` e `config.js` para a raiz.
3. Edite `config.js` e cole sua chave da Groq em `GROQ_API_KEY`.
4. Ative GitHub Pages em `Settings > Pages > Deploy from branch > main / root`.
5. Abra o link gerado.

## Verdade importante sobre chave API

Chave em `config.js` no GitHub Pages fica exposta para qualquer pessoa que abrir o site e inspecionar o código. Para uso interno/MVP isso pode ser aceitável se você controlar a chave e limites de uso. Para produção profissional, o correto é usar backend/proxy serverless para esconder a chave.

## Funções principais

- Cadastro de dados do orçamento/OS.
- Peças, serviços, valores, desconto e total automático.
- Resumo por seção de mão de obra.
- Gravação de áudio no navegador.
- Transcrição via Groq Whisper.
- IA via Groq para transformar fala em itens de orçamento.
- Geração de PDF com padrão parecido com o PDF modelo.
- Mensagem pronta para WhatsApp via wa.me.
- Exportar/importar JSON do orçamento.
- Salvamento local automático no navegador.

## Exemplo de fala

"Cliente Polícia Militar, veículo Renault Duster placa FBO3E02, ano 2020, km 241601. Defeito reclamado checklist completo. Adicionar serviço mecânica substituir bateria, TMO 0,3, valor hora 152,25, desconto 29%. Adicionar peça bateria 60 amperes, quantidade 1, valor unitário 420 reais. Diagnóstico técnico bateria com baixa carga."

