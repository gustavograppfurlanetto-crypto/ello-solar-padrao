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

## Estrutura de arquivos do projeto

```
ello-solar-padrao/
│
├── index.html              ← Sistema principal de Troca de Padrão de Entrada
├── titularidade.html       ← Sistema de Troca de Titularidade
├── onboard.html            ← Painel interno de Onboard de Clientes
├── onboard-cliente.html    ← Portal público do cliente para confirmar dados
├── avaliacoes.html         ← Painel interno de avaliações NPS (ao vivo)
├── avaliacao-standalone.html ← Formulário público de avaliação (com campo nome)
├── avaliacao.html          ← Formulário público de avaliação (sem campo nome)
│
└── CLAUDE.md               ← Este arquivo (contexto do projeto)
```

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

---

## Histórico de funcionalidades

### index.html — Troca de Padrão de Entrada

**Layout e navegação**
- Sidebar fixa lateral com logo Ello Solar (via Supabase Storage, fallback texto)
- Menu de navegação: Todos os pedidos, Em aberto, Aguardando, Em andamento, Concluídos, Arquivados
- Seção "Configurações" no menu: gerenciamento de Executores
- Seção "Outros serviços" no menu: links para Troca de Titularidade e Onboard
- Rodapé da sidebar com contador total de pedidos ativos (DM Mono)
- Topbar com título dinâmico e botões de ação (Cadastro rápido, Novo pedido)

**Dashboard de estatísticas**
- 4 cards de contagem: Abertos, Aguardando, Em andamento, Concluídos
- Contadores atualizados automaticamente ao filtrar/arquivar

**Tabela de pedidos**
- Colunas: Nome do contrato, Nome do titular, CPF, UC, Cidade, Tipo, Status, Executor, Custo, Negociado, Data
- Busca em tempo real por: nome do titular, nome do contrato, CPF, unidade consumidora
- Filtro por tipo de solicitação (dropdown)
- Filtro por status (dropdown)
- Filtro por cidade (dropdown preenchido dinamicamente)
- Grupo de filtros toggle "Execução Empresa / Execução Cliente" com contadores
- Grupo de filtros toggle "Completos / Incompletos" com contadores (baseado em nome do titular)
- Grupo de filtros toggle "Com docs / Sem docs" com contadores
- Ordenação por nome do contrato (toggle: asc → desc → original)
- Paginação (10 itens por página) com navegação e reticências para muitas páginas
- Indicador de cadastro incompleto (⚠️ amarelo quando CPF ou endereço ausentes)
- Badge "Incompleto" laranja quando pedido criado via cadastro rápido sem nome do titular
- Badge "Deslig." para pedidos com UC de desligamento vinculada
- Tag clicável "Execução Cliente" (toggle inline sem abrir modal)
- Tag clicável "Docs" (toggle inline para marcar documentos recebidos)

**Inline edit (edição direto na célula)**
- Clique na célula de Status: abre dropdown com os 4 status disponíveis
- Clique na célula de Executor: abre dropdown com executores ativos
- Clique na célula de Custo: abre input numérico (salva em centavos)
- Clique na célula de Negociado: abre input numérico
- Enter confirma, Escape cancela; feedback visual verde (sucesso) ou vermelho (erro)

**Modal Novo / Editar Pedido**
- Seção "Dados do titular": nome completo, nome do contrato, CPF (máscara), RG, data de nascimento, nome da mãe, nome do pai, telefone (máscara), e-mail
- Seção "Localização": UC (obrigatório), endereço, cidade, ponto de referência, link Google Maps
- Seção "Tipo de solicitação": Aumento de carga, Troca de padrão, Alteração de conexão, Desligamento
  - Tipo "Alteração de conexão": campo adicional de tipo de conexão (Bifásico / Trifásico)
  - Trifásico + Alteração de conexão: checkbox para UC a ser desligada (bloco laranja expansível)
    - UC de desligamento: número da UC + opção de mesmo titular ou outro titular (com todos os dados do titular alternativo)
    - Botão "Adicionar outra UC" para múltiplas UCs extras (apenas em Trifásico)
- Seção "Atribuição": seleção de executor + valor acordado (máscara de moeda)
- Seção "Foto do padrão atual": upload de imagem com preview
- Modo edição: pré-preenche todos os campos incluindo UCs extras

**Modal Cadastro Rápido**
- Cria pedido apenas com nome do contrato (campo único)
- Permite completar os demais dados via edição depois

**Modal Detalhe do Pedido**
- Exibe badge de status + tipo de solicitação + data de criação
- Alerta de cadastro incompleto (faltam CPF, endereço, nascimento ou telefone)
- Todos os dados do titular organizados em grid
- Bloco de desligamento vinculado (com múltiplas UCs extras se trifásico)
- Foto do padrão atual (se anexada)
- Botões de mudança de status (excluindo o status atual)
- Botão arquivar (apenas para pedidos concluídos) / desarquivar
- Seção de documentos recebidos: botão "Anexar documento" com lista de arquivos por pedido
- Botões de footer: OS Solicitação, OS Execução, Editar, Excluir

**Geração de Ordens de Serviço (OS)**
- OS de Solicitação: abre janela de impressão com dados do pedido formatados
- OS de Execução: abre janela de impressão com dados de execução

**Gerenciamento de Executores**
- View separada (ativada pelo menu "Executores")
- Tabela de executores com nome e status (ativo/inativo)
- Modal para criar novo executor: nome + toggle ativo
- Edição inline de executor existente
- Executores inativos ficam ocultos nos dropdowns de seleção

**Arquivamento**
- Pedidos concluídos podem ser arquivados individualmente ou em lote ("Arquivar concluídos")
- View "Arquivados" separada no menu
- Pedidos arquivados podem ser desarquivados

**Exportação**
- Botão "Exportar" gera planilha Excel (.xlsx) dos pedidos filtrados (via SheetJS)

**Documentos por pedido**
- Seção no modal de detalhe para anexar documentos (múltiplos por pedido)
- Upload para Supabase Storage (bucket `fotos-padrao`, pasta por pedido)
- Listagem de documentos anexados com link de acesso

---

### titularidade.html — Troca de Titularidade

**Layout e navegação**
- Mesma estrutura de sidebar fixa do index.html
- Menu com status específicos: Novo pedido, Documentação, Solicitação, Aguardando aprovação, Aprovados, Arquivados
- Links para outros sistemas: Troca de Padrão, Onboard
- Rodapé com contador total

**Dashboard de estatísticas**
- 5 cards: Novo pedido, Documentação, Solicitação, Aguardando aprovação, Aprovado

**Tabela de pedidos**
- Colunas: Nome do contrato, Nome do novo titular, CPF, UC, Cidade, Status, Executor, Custo, Negociado, Docs, Data
- Busca por nome do novo titular, CPF e UC
- Filtros: Status, Cidade, Executor (com dropdown populado dinamicamente)
- Ordenação por nome do novo titular
- Badge de documentos "X/Y docs" (verde = completo, cinza dashed = incompleto)
- Badge "Incompleto" quando UC não preenchida

**Inline edit (edição direto na célula)**
- Clique em Status, Executor, Custo ou Negociado para edição inline
- Mesmo comportamento e feedback visual do index.html

**Modal Novo / Editar Pedido**
- Seção "Dados da UC": nome do contrato, UC, cidade, endereço
- Seção "Novo titular": nome (obrigatório), CPF (máscara), RG, data de nascimento, telefone (máscara), e-mail, nome da mãe, nome do pai
- Checkbox "Imóvel pertence a terceiro" com aviso de que será necessária declaração
- Seção "Atribuição": executor, custo, negociado
- Seção "Observações": campo de texto livre

**Modal Cadastro Rápido**
- Cria pedido apenas com nome do novo titular

**Modal Detalhe do Pedido**
- Badge de status + indicador "Imóvel de terceiro" se aplicável
- Seções: Dados da UC, Novo titular, Atribuição, Observações
- Seção de documentos com slots fixos por tipo:
  - Procuração (sempre)
  - Documento do novo titular (sempre)
  - Documento de posse do imóvel (sempre)
  - Declaração de autorização (apenas se imóvel de terceiro)
- Upload por slot com botão "Enviar" → Supabase Storage (`titularidade/{id}/`)
- Exclusão individual de documento com confirmação
- Contagem de docs atualiza badge na tabela imediatamente
- Botões de mudança de status
- Botão Arquivar (apenas para aprovados) / Desarquivar

**Arquivamento**
- Disponível apenas para pedidos com status "Aprovado"
- View de arquivados com opção de desarquivar

---

### onboard.html — Painel Interno de Onboard

**Layout**
- Header simples (sem sidebar) com logo e link "← Voltar ao sistema"
- Tabela centralizada com max-width 1200px

**Tabela de onboards**
- Colunas: Nome do cliente, Número da proposta, Vendedor, Status, Data, Ações
- 3 status: Aguardando (amarelo), Confirmado (verde), Pendente (laranja)
- Botões de ação por linha: Ver detalhes, Copiar link, Excluir

**Modal Novo Onboard — Fluxo em 2 etapas**
- Etapa 1 (Upload): área de upload para arquivo .docx do documento "Negócio Fechado"
  - Botão "Extrair dados do documento" usa mammoth.js para ler o Word no navegador
  - Mapeamento de labels do documento para campos do sistema (LABEL_MAP)
  - Extração automática do CEP a partir do endereço
  - Indicador de loading durante extração
  - Exibição de erro se extração falhar
- Etapa 2 (Revisão): formulário pré-preenchido com todos os dados extraídos
  - Campos de dados pessoais: vendedor, nome, CPF, RG, profissão, estado civil, nascimento, e-mail, telefone
  - Campos do projeto: UC geradora, CEP, endereço, coordenadas, UCs remotas, troca de titularidade, troca de padrão, sistema kWp, qtd módulos, tipo inversor, qtd inversores, valor do projeto, forma de pagamento, prazo de entrega, padrão, valor negociado do padrão, padrão de entrada, tipo de alimentação, UC do padrão novo, UCs desligadas, número da proposta
  - Todos os campos editáveis para correção antes de salvar
  - Botão "Salvar e gerar link" → salva no Supabase e exibe link do cliente
  - Link gerado com token único via `onboard-cliente.html?token=...`
  - Botão copiar link + Compartilhar via WhatsApp

**Modal Detalhe do Onboard**
- Exibe link do cliente com botão copiar
- Dados pessoais em grid
- Dados do projeto em grid
- Observações do cliente (preenchidas pelo próprio cliente no portal)
- Documentos enviados pelo cliente: links para RG, CPF, comprovante de residência

---

### onboard-cliente.html — Portal do Cliente

**Acesso e validação**
- Página pública acessada via URL com parâmetro `?token=<uuid>`
- Busca o onboard no Supabase pelo token
- Estados: Loading (spinner), Erro (link inválido), Sucesso (já confirmado), Formulário
- Se status já for "confirmado", exibe mensagem de confirmação anterior e bloqueia novo envio

**Fluxo em 3 etapas com indicador de progresso**
- Etapa 1 — Dados pessoais:
  - Campos pré-preenchidos e editáveis: nome, CPF, RG, profissão, estado civil, nascimento, e-mail, telefone
- Etapa 2 — Dados do projeto:
  - Cards read-only com os dados do projeto (UC geradora, endereço, sistema kWp, módulos, inversores, valor, pagamento, prazo)
  - Campo de observações livre para o cliente acrescentar informações
- Etapa 3 — Documentos:
  - Upload de foto do RG (frente e verso)
  - Upload de foto do CPF
  - Upload de comprovante de residência
  - Preview inline de imagem após seleção
  - Upload imediato para Supabase Storage (`onboards/{token}/{tipo}.{ext}`) com upsert
  - Indicador "✓ Documento enviado" por slot
  - Validação: todos os 3 documentos obrigatórios antes de confirmar
- Confirmação final:
  - Salva dados corrigidos do cliente no Supabase
  - Atualiza status para "confirmado"
  - Registra `dados_confirmados_em` timestamp
  - Exibe tela de agradecimento

---

### avaliacoes.html — Painel de Avaliações NPS

**Layout**
- Header com logo + badge "AO VIVO" (laranja)
- Layout sem sidebar, centralizado (max-width 1100px)

**Estatísticas**
- 4 cards com barra colorida no topo: Média Geral (azul), Total de Avaliações (laranja), Promotores % (verde), Detratores % (vermelho)
- Promotores = notas 9 e 10; Detratores = notas 0 a 6

**Gráfico de distribuição**
- Gráfico de barras verticais para cada nota de 0 a 10
- Cores: vermelho (0-6), amarelo (7-8), verde (9-10)
- Altura proporcional ao máximo de respostas numa nota
- Exibe contagem acima de cada barra (apenas se > 0)

**Tabela de avaliações**
- Colunas: Data/hora, Nome, Nota (pill colorido), Comentário
- Pill da nota: vermelho (0-6), amarelo (7-8), verde (9-10)
- Sem comentário: texto em itálico cinza
- Botão de excluir (ícone lixeira, aparece ao hover)

**Exclusão com senha**
- Modal de confirmação com campo de senha
- Senha correta: Ello123!
- Feedback de erro com campo destacado em vermelho
- Fechar modal clicando fora ou tecla Escape

**Atualização automática**
- `setInterval` a cada 60 segundos recarrega todas as avaliações

---

### avaliacao-standalone.html — Formulário Público de Avaliação (com nome)

**Formulário NPS**
- Campo de nome obrigatório (com validação e destaque de erro)
- Grade de 11 botões (0-10) com gradiente de cores (vermelho → amarelo → verde)
- Efeito de seleção: botão selecionado aumenta, outros ficam opacos
- Campo de comentário opcional
- Botão "Enviar avaliação" habilitado apenas após selecionar nota
- Validação: nome obrigatório + nota obrigatória

**Tela de agradecimento**
- Exibe logo + ícone estrela + mensagem + badge com nome e nota enviada
- Substitui o formulário após envio bem-sucedido

---

### avaliacao.html — Formulário Público de Avaliação (sem nome)

**Variação mais simples da avaliacao-standalone.html**
- Sem campo de nome (avaliação anônima)
- Mesma grade de botões NPS 0-10 com as mesmas cores
- Campo de comentário opcional
- Tela de agradecimento após envio com nota registrada
- Logo via Supabase Storage (com fallback texto)
