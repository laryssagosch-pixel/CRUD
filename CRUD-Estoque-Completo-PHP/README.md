# Estoque Didático MVC — PHP 8.1+ + PDO + MySQL

Aplicação educacional completa, organizada em **Model–View–Controller (MVC)**. Apenas `public/` deve ser publicada pelo Apache.

## Funcionalidades
Login, logout, troca de senha (`password_hash`), usuários admin/operador, dashboard, CRUD de produtos, entradas e saídas com transação, histórico, validação Bootstrap + JavaScript, CSRF, prepared statements e escape HTML.

## Instalação com XAMPP
1. PHP 8.1+ com `pdo_mysql` e `mbstring`. Inicie Apache e MySQL.
2. Copie o projeto para `htdocs/CRUD-Estoque-Completo-PHP`.
3. Importe `sql/banco.sql` no phpMyAdmin (cria o banco `estoque_didatico`). **Importe uma única vez.**
4. Variáveis opcionais: `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASS` (padrão: 127.0.0.1 / estoque_didatico / root / vazia).
5. Abra `http://localhost/CRUD-Estoque-Completo-PHP/public/index.php?r=login`
6. Admin inicial: `admin@escola.local` / `Admin@12345!` — **troque a senha em "Minha senha".**

## Rotas (todas via `public/index.php?r=...`)
| GET | POST |
| --- | --- |
| `login` | `login.submit` |
| `dashboard` | `logout` |
| `products`, `products.create`, `products.edit&id=1` | `products.save`, `products.delete` |
| `movements`, `movements.create&produto_id=1` | `movements.save` |
| `users` | `users.save`, `users.toggle` |
| `password` | `password.save` |

## Permissões
- **Admin:** produtos (CRUD), usuários, movimentações, histórico, própria senha.
- **Operador:** consulta de produtos, entradas/saídas, histórico, dashboard, própria senha.

## Roteiro de testes
1. Senha errada não autentica; entre com o admin e troque a senha.
2. Cadastre um produto: saldo inicial 0.
3. Entrada 10 + saída 3 → saldo 7, dois eventos no histórico.
4. Saída 99 deve ser recusada.
5. Excluir produto com movimentação é bloqueado.
6. Operador recebe 403 nas rotas de admin.
7. POST sem CSRF retorna 419.
8. Nome `<script>alert(1)</script>` aparece como texto.

Projeto de ensino, não pronto para produção (faltam HTTPS, rate limiting, auditoria e backups).
