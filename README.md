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


## Correção aplicada nesta versão

- Botão **Limpar orçamento** na barra superior.
- Botão **Limpar peças/serviços** na aba de áudio e em Configuração.
- IA agora aplica, por padrão, substituição dos itens atuais antes de preencher, evitando duplicidade.
- IA orientada a não inventar peças, serviços, valores, cliente, veículo ou diagnóstico.
- Padronização em MAIÚSCULO para cliente, veículo, peças, serviços, defeito e diagnóstico.
- Deduplicação local: mesmo que a IA devolva item repetido, o sistema não lança duplicado.
- Aba Configuração com painéis minimizáveis e maximizáveis para celular e computador.

Importante: se o navegador já tiver orçamento salvo antigo no localStorage, clique em **Limpar orçamento** ou **Limpar dados locais** depois de publicar esta versão.

## Correção 2 - modo celular e fidelidade do áudio

- O menu lateral agora pode ser escondido/aberto pelo botão **Menu**.
- Por padrão o sistema abre direto na tela **Preencher por áudio**.
- Existe botão flutuante **Áudio direto** para uso no celular.
- A configuração tem a opção de iniciar com menu escondido ou escolher a tela inicial.
- A IA agora usa **modo fiel absoluto**: descarta serviço/peça genérica, repetida ou que não aparece claramente no texto transcrito.
- Serviço com valor total informado e sem TMO passa a somar corretamente no total do serviço, sem transformar o valor em descrição.
- Serviços genéricos inventados continuam bloqueados. Exceção: se o áudio disser literalmente **"serviço 500"** ou **"mão de obra 500"**, o sistema lança descrição **SERVIÇO/MÃO DE OBRA** com valor total de R$ 500,00.

## Correção 3 - lista falada de peças e serviço

- Frase como **"kit junto à tampa de válvula 383, tampa de válvula usada 400 reais, dois discos de freio 640, jogo de pastilha 293 e serviço 500"** agora é interpretada corretamente.
- Peças faladas em lista, mesmo sem repetir a palavra "peça", entram como peças quando terminam com valor.
- Quantidade falada por extenso é reconhecida: "dois discos de freio 640" vira quantidade 2.
- Quando a quantidade é maior que 1 e o áudio não diz "valor unitário" ou "cada", o valor falado é tratado como total da linha e dividido pela quantidade para manter a soma fiel.
- Preferências antigas de menu salvas no navegador são ignoradas nesta versão para o sistema voltar a abrir direto no áudio com menu escondido.
- Frase como **"R$400,00 a serviço R$119,00"** agora não joga serviço em peças: lança **SERVIÇO** com valor total de R$ 119,00. O valor solto de R$ 400,00 fica sem lançamento porque não tem descrição confiável no áudio.

## Correção 4 - serviço com descrição vazia da IA

- Se a Groq devolver `servicos: [{ descricao: "", valorTotal: 1109 }]`, o sistema agora corrige antes de salvar.
- Quando a transcrição contém **serviço** ou **mão de obra**, o item recebe descrição **SERVIÇO** ou **MÃO DE OBRA** e o valor fica em `valorTotal`.
- Para áudio, o sistema não depende mais de TMO ou valor/hora. Valor falado de serviço é tratado como total do serviço.
- A tela mostra o aviso **VERSÃO 10.12** para confirmar que o GitHub Pages está rodando a versão correta.

Após subir no GitHub Pages, use **Ctrl+F5** no computador ou limpe o cache no celular. Também clique em **Limpar orçamento** para apagar dados antigos salvos no navegador.
