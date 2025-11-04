# 🚀 Organização Android – Apps em React Native (Expo)

![doc-android](https://github.com/user-attachments/assets/eca24de9-54e9-4454-b575-6c38d5f167d4)

> **Escopo:** Esta organização no GitHub hospeda **apenas aplicativos Android** desenvolvidos em **React Native com Expo**.  
> Padronizamos estrutura, automações, qualidade e publicação (Google Play) para acelerar entregas e manter consistência entre projetos.

---

## 🧭 Visão Geral

- **Plataforma alvo:** Android (a organização é exclusivamente Android).

- **Stack base:** Expo (React Native + TypeScript), EAS Build/Submit, GitHub Actions, ESLint/Prettier, Jest, Detox.  
- **Publicação:** Google Play Console (tracks: *internal*, *alpha*, *beta*, *production*).  
- **Configuração de apps:** gerenciadas via `app.json/app.config.ts` e variáveis de ambiente.  
- **Armazenamento e backends:** cada app define seu backend (ex.: Supabase, Firebase, REST/GraphQL).  
- **Distribuição interna:** EAS + Play Internal Testing (testadores por grupo).

---

## 🗂️ Estrutura da Organização

```
android-expo-org/
├── templates/                  # Modelos iniciais (boilerplates) para novos apps
│   ├── expo-minimal/
│   ├── expo-supabase/
│   └── expo-monorepo/
├── design-system/              # Biblioteca de UI compartilhada (tokens, componentes)
├── tooling/                    # Scripts e ações reutilizáveis (GH Actions, linters, hooks)
├── docs/                       # Documentos padrão (guias, políticas, checklists)
└── apps/                       # Repositórios dos aplicativos Android
    ├── app-foo/
    ├── app-bar/
    └── app-baz/
```

**Observação:** É permitido **monorepo** (`apps/*` + `packages/*`) ou **multi-repo** (um repo por app). Escolha deve ser justificada no README do projeto.

---

## 🧰 Stack Técnica (padrão)

- **React Native + Expo** (SDK mais recente estável)
- **TypeScript** (strict mode)
- **Navegação:** Expo Router ou React Navigation
- **Estado:** React Query + Zustand (ou Redux Toolkit quando necessário)
- **Estilo/UI:** NativeWind (Tailwind RN) + Design System interno
- **Build/Distribuição:** **EAS Build** + **EAS Submit**
- **CI/CD:** GitHub Actions (lint, tests, build, submit)
- **Testes:** Jest (unit), React Native Testing Library (componentes), Detox (e2e essencial)
- **Qualidade:** ESLint, Prettier, Husky + lint-staged
- **Monitoramento (opcional):** Sentry (crashes), Expo Updates (OTA) quando aplicável
- **Notificações (opcional):** Expo Push (sem dependência direta de FCM no app)
- **Analytics (opcional):** Expo Analytics/Segment

---

## 🏗️ Padrões de Projeto

- **Arquitetura por feature:** `app/ (rotas)`, `features/*`, `components/*`, `services/*`, `stores/*`, `assets/*`
- **Camadas limpas:** *domain* (regras), *data* (API/DB), *app* (UI)
- **Acessibilidade:** labels, foco, contraste, tamanhos escaláveis
- **Performance:** memoização, FlatList/FlashList, imagens otimizadas, lazy loading
- **Internacionalização:** `pt-BR` padrão; pronto para i18n
- **Offline-first (quando fizer sentido):** cache + revalidação

---

## 🧪 Qualidade e Segurança

- **Commits:** Conventional Commits
- **Branches:** `main` (release) e `dev` (integração) — feature branches: `feat/...`, `fix/...`
- **PRs:** exigem aprovação + checks verdes (lint, tests, build)
- **Sem segredos no código:** use **GitHub Secrets** / **EAS secrets**
- **Permissões Android:** declarar apenas o necessário e documentar no README
- **Licenças:** compatibilidade e registro de terceiros em `docs/licenses.md`

---

## 🔁 Fluxo de CI/CD (padrão)

1. **A cada PR**: Lint + Testes + Build Android (debug).  
2. **Merge na `main`**: EAS Build (release) + EAS Submit (Internal Testing).  
3. **Promover tracks** no Play Console: Internal → Alpha → Beta → Production.  
4. **Tags & Releases**: gerar *changelog* automático (conventional-changelog).

**Exemplo de Jobs (alto nível):**
- `ci:lint-test`
- `ci:build-android-debug`
- `release:build-android`
- `release:submit-play-internal`

---

## 🧾 Versão, Changelog e Naming

- **Versionamento:** **SemVer** (`MAJOR.MINOR.PATCH`) + `versionCode` incremental Android
- **Changelog:** gerado em cada release, anexado ao GitHub Release
- **Nomes de pacotes:** `com.org.appname` (documentar no README do app)

---

## 📦 Templates Oficiais

1. **expo-minimal** – app base com navegação, theming, lint, tests.  
2. **expo-supabase** – autenticação e CRUD com Supabase (Auth/DB/Storage).  
3. **expo-monorepo** – Turborepo (apps + packages), design system compartilhado.

Cada template contém:
- README com **setup passo a passo**
- Scripts `npm run dev/lint/test/build/android`
- **GitHub Actions** e **eas.json** exemplo

---

## 📝 Guia de Contribuição (ORG)

- **Issues:** use templates (`bug`, `feature`, `chore`)
- **Labels:** `prio:alta`, `tipo:bug/feature/docs`, `plataforma:android`, `status:em-andamento/pronto`
- **PRs:** vinculados a issues; descrição clara; screenshots/gifs quando visual
- **Code Owners:** revisão obrigatória para áreas críticas (build, design system, segurança)

---

## 🧷 Gestão de Ambientes

- **Env vars:** `.env.example` + `app.config.ts` lendo envs
- **Segredos:** **NUNCA** em repositório; usar **GitHub Secrets**/**EAS Secrets**
- **Build profiles (eas.json):** `preview`, `internal`, `production`
- **Gatekeepers:** feature flags via arquivo/remote (ex.: JSON remoto)

---

## 🛠️ Publicação no Google Play

- **Certificados**: gerenciados pelo EAS (keystore)
- **Listagem:** título, descrição, gráficos, *feature graphic*, screenshots obrigatórios
- **Políticas:** privacidade, coleta de dados, permissões
- **Testes internos:** adicionar testadores por grupo
- **Checklist de release:** em `docs/release-checklist.md` (QA, perf, acessibilidade, permissões, notas)

---

## 🔒 Privacidade & Compliance

- **Política de privacidade:** link no app e na Play Store
- **Consentimentos:** para analytics/telemetria quando necessário
- **Retenção de dados:** documentada por app
- **Solicitações do usuário:** exportar/excluir dados (quando aplicável)

---

## 📚 Documentos Úteis (em `docs/`)

- `getting-started.md` – Como iniciar um projeto novo
- `ci-cd.md` – Pipelines e secrets
- `play-store.md` – Passo a passo de publicação
- `design-system.md` – Tokens, componentes, padrões visuais
- `security.md` – Boas práticas e auditoria
- `testing.md` – Estratégia de testes (unit/e2e)
- `performance.md` – Dicas e métricas
- `accessibility.md` – Checklist A11y
- `release-checklist.md` – Itens obrigatórios antes de publicar

---

## 🤝 Suporte & Contato

- **Issues** nos repositórios individuais
- **Discussions** na organização para decisões de arquitetura/comuns
- **Responsáveis pela org:** manter templates, actions, design system e docs atualizadas

---

## ✅ Como criar um novo app Android (resumo)

1. **Crie o repositório** em `apps/` a partir de um **template oficial**.  
2. Atualize `app.config.ts`, pacote Android (`com.org.seuapp`) e ícones/splash.  
3. Configure **GitHub Secrets** e **EAS** (`eas login`, `eas secret:create ...`).  
4. Ajuste **CI/CD** (workflows) e `eas.json` (profiles).  
5. Rode `npm run lint && npm test`.  
6. Faça **EAS Build** (`eas build -p android`) e **Submit** (`eas submit -p android`).  
7. Abra PR, peça revisão e siga o **Checklist de Release**.

---

> **Imagem do topo:** salve `banner-android.jpg` na raiz do repositório de documentação (ou ajuste o caminho no Markdown).

