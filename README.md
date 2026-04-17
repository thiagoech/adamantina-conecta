# 🏙️ Adamantina Conecta

Marketplace local de serviços para Adamantina-SP. Conecta clientes a prestadores de serviços verificados.

---

## 🚀 Setup rápido

### 1. Pré-requisitos
- Node.js 18+
- PostgreSQL rodando localmente (ou Supabase / Railway)

### 2. Instalar dependências
```bash
npm install
```

### 3. Configurar variáveis de ambiente
Edite o arquivo `.env.local`:
```env
DATABASE_URL="postgresql://SEU_USER:SUA_SENHA@localhost:5432/adamantina_conecta"
NEXTAUTH_SECRET="mude-esta-chave-em-producao-use-openssl-rand-base64-32"
NEXTAUTH_URL="http://localhost:3000"
```

> 💡 Para gerar um `NEXTAUTH_SECRET` seguro:
> ```bash
> openssl rand -base64 32
> ```

### 4. Criar o banco e aplicar schema
```bash
npx prisma db push
```

### 5. Popular com dados de teste
```bash
npm run db:seed
```

### 6. Rodar o projeto
```bash
npm run dev
```

Acesse: [http://localhost:3000](http://localhost:3000)

---

## 👤 Usuários de teste

| Tipo       | E-mail                     | Senha    |
|------------|----------------------------|----------|
| Admin      | admin@adamantina.com        | senha123 |
| Cliente    | joao@gmail.com              | senha123 |
| Cliente    | maria@gmail.com             | senha123 |
| Prestador  | carlos@gmail.com            | senha123 |
| Prestador  | roberto@gmail.com           | senha123 |
| Prestador  | ana@gmail.com               | senha123 |

---

## 🗺️ Páginas do sistema

| Rota                    | Descrição                              |
|-------------------------|----------------------------------------|
| `/home`                 | Landing page pública                   |
| `/catalogo`             | Catálogo de prestadores por categoria  |
| `/servicos/[id]`        | Perfil detalhado do prestador          |
| `/login`                | Autenticação                           |
| `/cadastro`             | Registro de cliente ou prestador       |
| `/dashboard`            | Painel principal do usuário            |
| `/solicitacoes`         | Lista de solicitações do usuário       |
| `/solicitacoes/nova`    | Criar nova solicitação de serviço      |
| `/solicitacoes/[id]`    | Detalhes + ações de uma solicitação    |
| `/perfil`               | Editar perfil e dados profissionais    |
| `/pagamento`            | Histórico de pagamentos                |
| `/avaliacoes`           | Avaliações recebidas (prestadores)     |
| `/admin`                | Painel administrativo                  |

---

## 🏗️ Estrutura do projeto

```
adamantina-conecta/
├── app/
│   ├── api/
│   │   ├── auth/          # NextAuth + registro
│   │   ├── requests/      # CRUD solicitações
│   │   ├── reviews/       # Avaliações
│   │   ├── payments/      # Pagamentos simulados
│   │   ├── providers/     # Listagem de prestadores
│   │   ├── profile/       # Perfil do usuário
│   │   ├── notifications/ # Notificações
│   │   └── admin/         # Rotas administrativas
│   ├── home/              # Landing page
│   ├── catalogo/          # Catálogo público
│   ├── servicos/[id]/     # Perfil do prestador
│   ├── dashboard/         # Painel do usuário
│   ├── solicitacoes/      # Gestão de pedidos
│   ├── perfil/            # Editar perfil
│   ├── pagamento/         # Histórico financeiro
│   ├── avaliacoes/        # Avaliações (prestador)
│   └── admin/             # Painel admin
├── components/
│   ├── layout/            # Navbar, Footer
│   └── ui/                # StatusBadge, StarRating, Modal, Toast...
├── hooks/                 # useToast
├── lib/
│   ├── auth.ts            # Configuração NextAuth
│   ├── prisma.ts          # Singleton do PrismaClient
│   └── validations.ts     # Schemas Zod
├── prisma/
│   ├── schema.prisma      # Modelos do banco
│   └── seed.ts            # Dados iniciais
└── types/
    └── next-auth.d.ts     # Extensão de tipos
```

---

## 🛠️ Stack

- **Framework:** Next.js 14 (App Router)
- **Auth:** NextAuth.js v4 (JWT + Credentials)
- **DB:** PostgreSQL + Prisma ORM
- **UI:** Tailwind CSS (utility-first)
- **Validação:** Zod
- **Linguagem:** TypeScript

---

## 💳 Pagamentos

Os pagamentos são **simulados** (status `completed` imediato). Para produção:

- **PIX:** Integre [Mercado Pago SDK](https://www.mercadopago.com.br/developers)
- **Cartão:** Integre [Stripe](https://stripe.com/br) ou Mercado Pago

---

## 🔐 Controle de acesso

| Role       | Permissões                                                  |
|------------|-------------------------------------------------------------|
| `client`   | Criar/cancelar solicitações, pagar, avaliar                 |
| `provider` | Aceitar/concluir serviços, editar perfil profissional       |
| `admin`    | Tudo + verificar prestadores, alterar qualquer status, gerir usuários |

---

## 🚀 Deploy para produção

### Frontend + Backend
- [Vercel](https://vercel.com) (recomendado para Next.js)

### Banco de dados
- [Supabase](https://supabase.com) (PostgreSQL gerenciado, plano grátis)
- [Railway](https://railway.app) (alternativa)
- [PlanetScale](https://planetscale.com) (requer mudar provider para `mysql`)

### Variáveis no Vercel
```
DATABASE_URL=postgresql://...
NEXTAUTH_SECRET=chave-segura-gerada
NEXTAUTH_URL=https://seu-dominio.vercel.app
```

---

## 📦 Comandos úteis

```bash
npm run dev          # Servidor de desenvolvimento
npm run build        # Build de produção
npm run start        # Servir build de produção
npm run db:push      # Aplicar schema ao banco
npm run db:seed      # Popular banco com dados de teste
npm run db:generate  # Regenerar Prisma Client
npx prisma studio    # GUI visual do banco de dados
```

---

## 🔮 Próximos passos sugeridos

- [ ] Chat em tempo real entre cliente e prestador (Socket.io / Pusher)
- [ ] Notificações push (Web Push API)
- [ ] Geolocalização e mapa de prestadores
- [ ] Sistema de agendamento com calendário
- [ ] Integração real de pagamentos (Mercado Pago / Stripe)
- [ ] Upload de fotos de perfil e portfólio
- [ ] Painel de análises para prestadores
- [ ] App mobile (React Native / Expo)
- [ ] Multi-tenancy para outras cidades
- [ ] Testes automatizados (Jest + Testing Library)
- [ ] Monitoramento de erros (Sentry)
