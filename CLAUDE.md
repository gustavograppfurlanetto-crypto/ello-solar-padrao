# Ello Solar — Sistema de Gestão

## Visão Geral
Sistema de gestão interno da Ello Solar com múltiplos módulos desenvolvidos em HTML/CSS/JavaScript puro com banco de dados Supabase.

## Links
- **Sistema principal:** https://gustavograppfurlanetto-crypto.github.io/ello-solar-padrao/
- **Avaliação de clientes:** https://gustavograppfurlanetto-crypto.github.io/ello-avaliacao/
- **Painel de avaliações:** https://gustavograppfurlanetto-crypto.github.io/ello-solar-padrao/avaliacoes.html
- **Onboard:** https://gustavograppfurlanetto-crypto.github.io/ello-solar-padrao/onboard.html
- **Troca de Titularidade:** https://gustavograppfurlanetto-crypto.github.io/ello-solar-padrao/titularidade.html

## Banco de Dados (Supabase)
- **Project ID:** zsaomhnehwervejkldam
- **URL:** https://zsaomhnehwervejkldam.supabase.co
- **Anon Key:** eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InpzYW9taG5laHdlcnZlamtsZGFtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzY5NzI5MzcsImV4cCI6MjA5MjU0ODkzN30._QYsLEIHxQV6UV90SPMWxds9BaGVvWuDy_6URN7Pavg
- **Região:** us-west-2
- **Storage bucket:** fotos-padrao (público)

## Tabelas principais
- **pedidos** — sistema de troca de padrão de entrada
- **titularidade** — sistema de troca de titularidade
- **executores** — lista de executores/técnicos
- **onboards** — plataforma de onboard de clientes
- **avaliacoes** — avaliações NPS dos clientes
- **documentos** — documentos anexados aos pedidos

## Identidade Visual
- **Cor primária:** #004358 (azul escuro)
- **Cor secundária:** #FD7400 (laranja)
- **Verde limão:** #BEDB39
- **Teal:** #1F8A70
- **Azul céu:** #58AFDA
- **Fonte:** Outfit (Google Fonts) + DM Mono
- **Logo:** base64 inline no HTML ou via Supabase Storage

## Hospedagem
- **Frontend:** GitHub Pages (deploy automático ao fazer push na branch main)
- **Banco:** Supabase (us-west-2)
- **Avaliação:** repositório separado github.com/gustavograppfurlanetto-crypto/ello-avaliacao

## Arquivos do projeto
- **index.html** — sistema principal de troca de padrão
- **titularidade.html** — sistema de troca de titularidade
- **onboard.html** — painel interno de onboard
- **onboard-cliente.html** — portal do cliente para confirmar dados
- **avaliacoes.html** — painel de avaliações NPS
- **avaliacao-standalone.html** — página pública de avaliação

## Desenvolvedor
Gustavo Grapp Furlanetto

## Observações importantes
- Sempre usar ALTER TABLE IF NOT EXISTS para novas colunas
- Storage bucket "fotos-padrao" já existe e é público
- GitHub Pages demora 1-2 minutos para publicar após push
- Executores são compartilhados entre todos os módulos (tabela executores)
- Senha para deletar avaliações: Ello123!
