# Catálogo de Produtos | React + API

## Estrutura do repositório

```
.
├── api/                  # API REST (Express),
└── catalogo-produtos/    # Front-end (React + Vite)
```

## Pré-requisitos e como executar
- Node.js 20 ou superior
- Como são dois terminais tem que rodar um para a API e outro para o front-end

### 1. API (terminal 1)

```bash
abra o terminal integrado da pasta api
npm install
npm start
```

Deve aparecer `Servidor rodando em http://localhost:3000`. Teste em <http://localhost:3000/produtos>.

### 2. Front-end (terminal 2)

```bash
abra o terminal integrado da pasta catalogo-produtos
npm install
npm run dev
```

Abra o endereço mostrado pelo Vite (normalmente <http://localhost:5173>).

### Estrutura da API

| Método | Rota | Descrição |
|--------|------|-----------|
| GET | `/produtos` | Lista de produtos |
| GET | `/produtos/:id` | Um produto (404 se não existir) |
| POST | `/produtos` | Cria produto |
| PUT | `/produtos/:id` | Atualiza produto |
| DELETE | `/produtos/:id` | Remove produto |

Campos de um produto: `id`, `descricao`, `preco`, `categoria`, `estoque`. O front-end usa `descricao` como nome do produto.

A API habilita CORS (`cors()`), porque o front-end roda em outra porta e o navegador bloquearia as requisições.

## Fluxo de dados
Todo o estado fica em App, o pai de todos os componentes. Os filhos só recebem dados por props e avisam o pai por funções de callback
Ao abrir a página, App chama a API (GET /produtos) num useEffect e guarda a lista em products. O texto digitado em ProductSearch sobe pelo callback onSearchChange, e App filtra a lista e a passa para ProductList, que cria um ProductCard para cada produto.
Ao clicar em “Ver detalhes”, ProductCard chama onViewDetails(id), que é o setSelectedId de App. Isso dispara outro useEffect, que chama GET /produtos/:id, e App entrega o resultado ao ProductDetails por props. “Fechar detalhes” chama onClose e limpa esses estados.

## Evidências
### Sem erros no console e com os cards carregados:
<img width="1865" height="1121" alt="image" src="https://github.com/user-attachments/assets/63ca1e5c-4503-4e47-a04d-6cf4c5357862" />

### Pesquisa funcionando:
<img width="1865" height="1117" alt="image" src="https://github.com/user-attachments/assets/010f70e3-711d-4a21-a527-74ec2679df9d" />

### Sem a API rodando:
<img width="1863" height="1115" alt="image" src="https://github.com/user-attachments/assets/1d9da5bf-27cf-40bd-8798-af26d38fd3f5" />

### Botão "Ver detalhes" e botão "Fechar detalhes":
<img width="1866" height="1118" alt="image" src="https://github.com/user-attachments/assets/bee1fd8f-c9d0-41d8-b108-083127813675" />
