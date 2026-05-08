# FinanceiroPro Elite

> Web App de gestão financeira profissional, com foco especial em **motoristas de aplicativo** e **profissionais autônomos**. Funciona 100% no navegador, sem backend, com persistência local.

![Status](https://img.shields.io/badge/status-stable-success)
![License](https://img.shields.io/badge/license-MIT-blue)
![PWA](https://img.shields.io/badge/PWA-ready-orange)
![No Build](https://img.shields.io/badge/build-zero%20config-yellow)

---

## Sumário

- [Demonstração](#demonstração)
- [Funcionalidades](#funcionalidades)
- [Stack Técnica](#stack-técnica)
- [Como Executar](#como-executar)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Atalhos de Teclado](#atalhos-de-teclado)
- [Privacidade dos Dados](#privacidade-dos-dados)
- [Roadmap](#roadmap)
- [Como Contribuir](#como-contribuir)
- [Licença](#licença)
- [Apoie o Projeto](#apoie-o-projeto)

---

## Demonstração

Interface 100% responsiva com **dark mode** (padrão) e **light mode** opcional. Identidade visual em gradiente Amarelo → Laranja Neon, tipografia Plus Jakarta Sans, layout mobile-first.

| Dashboard | Motorista | Análise |
|-----------|-----------|---------|
| Saldo total, entradas/saídas do mês, metas, gráficos | R$/km, R$/hora, lucro líquido, heatmap dia × hora | Score de saúde, comparativo 6 meses, projeções |

---

## Funcionalidades

### Core

- **Gestão de Entradas e Saídas** com diferenciação de **Salário Fixo** vs **Ganhos Variáveis** (motorista de app)
- **Categorização completa** — Combustível, Manutenção, Alimentação, Lazer, Contas Fixas, e categorias customizáveis
- **Múltiplas carteiras** — Conta Bancária, Dinheiro, Cartão de Crédito (saldo individual por carteira)
- **Transações recorrentes** — lançamento mensal automático
- **Anexar comprovante** — foto até 800KB salva em base64
- **Busca textual** por descrição
- **Filtros avançados** — período (dia/semana/mês/todos) + categoria

### Métricas para Motorista de App

- **R$ por KM** e **R$ por Hora** (bruto)
- **Lucro líquido** (ganho − combustível − manutenção)
- **Custo por KM real**
- **Heatmap de horários** — descubra os dias e horas mais lucrativos
- **Metas diárias e semanais** com barras de progresso

### Análise

- **Score de Saúde Financeira** (0–100) — baseado em % poupado, % comprometido com fixos e saldo
- **Comparativo Mês a Mês** — gráfico de barras dos últimos 6 meses
- **Projeção fim do mês** — baseada no ritmo atual de entradas e saídas
- **Top 5 maiores despesas**
- **Gráfico de evolução do saldo** (30 dias)
- **Distribuição de despesas** (gráfico de pizza)

### Persistência e Backup

- **localStorage** — dados ficam apenas no seu dispositivo
- **Exportar JSON** — backup completo
- **Importar JSON** — restaurar de backup
- **Exportar CSV** (UTF-8 com BOM, abre direto no Excel)

### Experiência

- **PWA instalável** — manifest dinâmico, funciona como app no celular
- **Dark/Light theme** com toggle
- **Onboarding** em 3 telas no primeiro acesso
- **Toasts** de feedback
- **Atalhos de teclado**
- **Safe-area** para iPhone com notch

---

## Stack Técnica

| Camada | Tecnologia |
|--------|------------|
| UI | React 18 (UMD via CDN) |
| Estilização | Tailwind CSS (CDN) + CSS Variables |
| Tipografia | Plus Jakarta Sans (Google Fonts) |
| Gráficos | SVG inline (sem dependências externas) |
| Ícones | SVG inline (estilo Lucide) |
| Estado | `useState` / `useEffect` / `useMemo` |
| Persistência | `localStorage` |
| PWA | Web App Manifest (blob dinâmico) |
| Build | **Zero config** — arquivo único `index.html` |

> **Por que sem build?** Para máxima portabilidade. Basta abrir o `index.html` no navegador, ou hospedar em qualquer servidor estático (GitHub Pages, Netlify, Vercel, S3, etc.).

---

## Como Executar

### Opção 1 — Abrir direto no navegador

Faça download do `index.html` e abra com duplo clique. Pronto.

### Opção 2 — Servidor local

```bash
# Clone o repositório
git clone https://github.com/ClaytonApps/financeiropro-elite.git
cd financeiropro-elite

# Sirva com qualquer servidor estático
npx serve .
# ou
python -m http.server 8000
```

Abra `http://localhost:8000` (ou a porta indicada).

### Opção 3 — GitHub Pages

1. Vá em **Settings → Pages**
2. Selecione branch `main` e pasta `/ (root)`
3. Salve. O app ficará disponível em `https://ClaytonApps.github.io/financeiropro-elite/`

---

## Estrutura do Projeto

```
financeiropro-elite/
├── index.html          # Aplicação completa (HTML + CSS + JS)
├── README.md           # Este arquivo
└── LICENSE             # MIT
```

Arquivo único, intencionalmente. Toda a lógica está em `index.html`.

---

## Atalhos de Teclado

| Tecla | Ação |
|-------|------|
| `N` | Nova transação |
| `F` | Abrir/fechar filtros |
| `/` | Focar busca |
| `Esc` | Fechar modal aberto |

---

## Privacidade dos Dados

**Nenhum dado sai do seu dispositivo.** Todas as transações ficam em `localStorage` no seu navegador. Não há servidor, telemetria, analytics ou tracking.

> ⚠️ Limpar o cache do navegador apaga seus dados. Use **Configurações → Backup → JSON** para guardar uma cópia.

---

## Roadmap

Funcionalidades planejadas para próximas versões:

- [ ] **Sincronização em nuvem** opcional (Supabase / Firebase)
- [ ] **IndexedDB** no lugar de localStorage (suporte a comprovantes maiores)
- [ ] **Service Worker** para offline real
- [ ] **Recorrências semanais e anuais**
- [ ] **Migração de schema** entre versões
- [ ] **Internacionalização** (i18n) — EN, ES
- [ ] **Tags livres** em transações
- [ ] **Relatórios em PDF**
- [ ] **Dashboard configurável** (drag & drop de cards)
- [ ] **Notificações push** para metas
- [ ] **Modo família** (múltiplos perfis no mesmo navegador)

---

## Como Contribuir

Contribuições são muito bem-vindas! 🧡

1. Faça um fork do projeto
2. Crie uma branch para sua feature: `git checkout -b feat/minha-feature`
3. Commit suas alterações: `git commit -m 'feat: adiciona X'`
4. Push para a branch: `git push origin feat/minha-feature`
5. Abra um Pull Request descrevendo o que mudou e por quê

### Padrões

- Mensagens de commit no padrão **Conventional Commits** (`feat:`, `fix:`, `docs:`, `refactor:`)
- Mantenha o app em **arquivo único** — esse é um princípio do projeto
- Teste manualmente em **mobile e desktop** antes de abrir o PR
- Sem dependências de build — o app deve continuar rodando ao abrir o `index.html` direto

### Reportar Bugs

Abra uma [Issue](https://github.com/ClaytonApps/financeiropro-elite/issues) descrevendo:

- Passos para reproduzir
- Comportamento esperado vs observado
- Navegador e versão
- Screenshots, se possível

---

## Licença

Distribuído sob a licença **MIT**. Veja [`LICENSE`](LICENSE) para mais detalhes.

```
Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy...
```

Você pode usar, modificar, distribuir e até comercializar este projeto, desde que mantenha o aviso de copyright.

---

## Apoie o Projeto

Se este projeto te ajudou a organizar suas finanças, considere apoiar o desenvolvimento. Cada contribuição mantém o projeto vivo, gratuito e em código aberto. 🧡

### 💛 Pix via Mercado Pago

**👉 [Apoiar agora — clique aqui](https://mpago.la/2z5Uj6E)**

Ou copie o link: `https://mpago.la/2z5Uj6E`

### Outras formas de apoiar

- ⭐ **Dê uma estrela no repositório** — ajuda muito na visibilidade
- 🐛 **Reporte bugs** ou sugira melhorias nas Issues
- 🔀 **Contribua com código** via Pull Request
- 📢 **Compartilhe o projeto** com outros motoristas de app e autônomos
- ✍️ **Escreva sobre o app** em blogs, redes sociais, grupos

---

<div align="center">

**FinanceiroPro Elite**

Feito com 🧡 para quem precisa de controle financeiro de verdade.

[⬆ Voltar ao topo](#financeiropro-elite)

</div>
