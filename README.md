# Introdução passo a passo ao framework React

📖 **Leia o tutorial: [https://stahe.github.io/br-react-etape-par-etape-sept-2026/](https://stahe.github.io/br-react-etape-par-etape-sept-2026/)**

Este curso ensina a construir uma aplicação web com a biblioteca [React](https://react.dev) 19.3: uma **aplicação de página única** (SPA), em que as páginas são renderizadas **no navegador** a partir de dados JSON vindos de um servidor.

Ele dá continuidade ao curso [Introdução passo a passo ao framework web NestJS](https://stahe.github.io/br-nestjs-html-sept-2026/), oferecendo uma perspectiva diferente, e segue o roteiro dos cursos [Introdução passo a passo ao framework Vue.js](https://stahe.github.io/br-vuejs-step-by-step-sept-2026/) e [Introdução passo a passo ao framework Angular](https://stahe.github.io/br-angular-etape-par-etape-sept-2026/): mesmo servidor, mesmas páginas, escritas no estilo React.

| Curso NestJS | Curso React |
|---|---|
| o servidor gera páginas HTML (Handlebars) | o navegador gera as páginas (React) |
| o navegador exibe o que recebe | o servidor devolve apenas JSON |
| controllers, views, `res.render` | componentes, roteador, hooks |
| guards `JwtAuthGuard`, `RolesGuard` | guards do roteador (middleware do React Router); o servidor mantém os seus |
| dicionários lidos pelo servidor | dicionários no cliente (i18next); o servidor devolve apenas chaves |
| mensagem flash em um cookie | mensagem flash em um store de estado |

As páginas em si permanecem inalteradas: são as da aplicação **RdvMedecins**, já apresentada com os outros frameworks.

## A abordagem: muitos exemplos curtos, depois um estudo de caso

O curso é estruturado em torno de **25 exemplos curtos**, cada um focado em um único conceito. Eles formam um único projeto Vite: um único comando `npm install`, seguido de `npm start <exemplo>` para executar um deles.

| Capítulo | Conteúdo | Exemplos |
|---|---|---|
| Primeiros passos | um projeto Vite, componentes de função, JSX, estado (`useState`, `useReducer`), eventos, campos controlados, validação, React Hook Form, formatação (`Intl`) | 01–09 |
| Componentes | props, props de função, `children`, ciclo de vida (`useEffect`, `useEffectEvent`), contextos, hooks personalizados, diálogo de confirmação (`createPortal`) | 10–16 |
| Roteamento | React Router 8: rotas, parâmetros, query, carregamento tardio (lazy loading), `<title>`, middleware | 17–18 |
| Operações assíncronas e estado compartilhado | timers, anti-bounce, respostas expiradas, `use()` + `<Suspense>`, Zustand, `localStorage`, `<Activity>` | 19–20 |
| Internacionalização | i18next / react-i18next: parâmetros, plurais, datas, valores monetários | 21 |
| O servidor: uma caixa-preta | instalação do servidor JSON, sua API, 48 exemplos com `curl` | – |
| Comunicação com o servidor | `fetch`, proxy do Vite, cookies `httpOnly`, `useActionState`, camada de acesso à API, TanStack Query, erros do servidor associados aos campos | 22–25 |

Cada exemplo é apresentado com seu código completo, comentado linha a linha, e uma captura de tela de sua execução.

## O servidor: uma caixa-preta

O servidor é o servidor NestJS da lição anterior, cujos controllers devolvem **JSON** — o mesmo dos clientes Vue.js e Angular. Esta lição o trata como uma **caixa-preta**: nós o instalamos, estudamos sua API e o consultamos com `curl` — mas não precisamos ler seu código (fornecido e comentado para os curiosos).

- Todos os erros têm o mesmo formato: `{ "statusCode": 409, "cle": "ERRORS.LOGIN_TAKEN", "params": {...}, "champs": {...} }` — **chaves** para tradução, nunca texto simples;
- Autenticação por meio de um token JWT em um cookie `httpOnly` / `sameSite=strict`: o código JavaScript do cliente nunca vê o token;
- Proteção CSRF: cookie `sameSite`, e todas as requisições POST devem ser em JSON;
- Um "modo de teste" para o CAPTCHA, para que você possa consultar a API com `curl`.

## O estudo de caso: o cliente React do RdvMedecins

Uma aplicação completa de **agendamento de consultas em um consultório médico**, com **todos** os seus arquivos (cerca de quarenta) listados e comentados.

- **React moderno**: componentes de função e hooks, form actions, `<title>` nos componentes, React Router 8 no modo "data" (middleware, carregamento de páginas sob demanda), TanStack Query para os dados do servidor, Zustand para o estado compartilhado.
- **Três papéis**: `ADMIN` (gerencia médicos e clientes), `DOCTOR` (agenda e cancela consultas), `USER` (o paciente: agenda consultas para si mesmo, gerencia sua conta).
- **Privacidade**: um paciente nunca recebe os nomes de outros pacientes — o servidor não os envia.
- **Todo o estado da página na URL**: `/agenda?idMedecin=1&jour=2026-10-05&reserver=7` reabre a janela de reserva depois de pressionar F5; os botões Anterior/Próximo funcionam.
- **Validação no servidor**: Os formulários exibem, abaixo de cada campo, os erros devolvidos pela API; bloqueio otimista, nomes duplicados, nome de usuário já em uso etc.
- **Sessão**: Restaurada depois de pressionar F5 (`GET /api/auth/moi`), expiração gerenciada em um único local (a função comum a todas as requisições, resposta 401).
- **Francês / inglês**, títulos de abas traduzidos, janela de confirmação acessível pelo teclado, Bootstrap 5.
- **Implantação**: o cliente compilado é servido pelo próprio servidor JSON (mesma origem, sem CORS).

## Conteúdo do repositório

```
exemples-react/            os 25 exemplos curtos (um único projeto Vite)
rdvmedecins-nestjs-json/   o servidor JSON do RdvMedecins (a "caixa-preta")
rdvmedecins-react/         o cliente React do estudo de caso
```

## Tecnologias

React 19.3 · TypeScript 6.0 · Vite 8 · React Router 8.4 · TanStack Query 5 · Zustand 5 · i18next 26 / react-i18next 17 · React Hook Form 7 (exemplo 08) · Bootstrap 5.3 · no servidor: NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Pré-requisitos

- Conhecimento básico de JavaScript (ou TypeScript), HTML e do protocolo HTTP.
- Node.js 24 (ou pelo menos 22.22), Visual Studio Code, a extensão de navegador React Developer Tools e um servidor MySQL (por exemplo, o Laragon no Windows) para o servidor JSON. As instruções de instalação são fornecidas nos apêndices do curso.

## Autor

Este curso, seus exemplos, o servidor JSON e o estudo de caso foram escritos por **Claude**, a IA da [Anthropic](https://www.anthropic.com) (setembro de 2026), a pedido de **Serge Tahé**.
