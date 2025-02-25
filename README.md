# API RESTful de E-commerce com PHP Puro

## 📌 Visão Geral

API RESTful desenvolvida em **PHP puro**, seguindo os princípios do **REST** e utilizando **HATEOAS** para tornar as respostas mais dinâmicas e autodescritivas. A API permite que **usuários administrem suas lojas** e **clientes façam compras**, garantindo segurança e escalabilidade.

---

## 📌 Arquitetura

A API segue a arquitetura **MVC (Model-View-Controller)** para manter uma separação clara de responsabilidades:

### 🔹 **1. Model (DAO - Data Access Object)**

- Responsável pela comunicação com o banco de dados.
- Cada entidade tem seu próprio DAO.

### 🔹 **2. Service (Regra de Negócio)**

- Intermedia os Controllers e os Models.
- Garante que as regras de negócio sejam aplicadas corretamente.

### 🔹 **3. Controller**

- Recebe requisições HTTP.
- Valida os dados e aciona os serviços adequados.
- Retorna as respostas no formato JSON.

### 🔹 **4. Core (Infraestrutura e Utilitários)**

- Inclui classes auxiliares como roteador, autenticação JWT, e resposta padronizada.

---

## 📌 Estrutura de Diretórios

```
/ecommerce-api
 ├── /app
 │   ├── /controllers
 │   │   ├── ProductController.php
 │   │   ├── UserController.php
 │   │   ├── OrderController.php
 │   │   ├── AuthController.php
 │   ├── /models
 │   │   ├── Product.php
 │   │   ├── User.php
 │   │   ├── Order.php
 │   ├── /services
 │   │   ├── ProductService.php
 │   │   ├── UserService.php
 │   ├── /dao
 │   │   ├── ProductDAO.php
 │   │   ├── UserDAO.php
 │   ├── /core
 │   │   ├── Database.php
 │   │   ├── Router.php
 │   │   ├── Response.php
 │   │   ├── JWT.php
 ├── /public
 │   ├── index.php
 │   ├── .htaccess
 ├── /config
 │   ├── database.php
 ├── composer.json
 ├── README.md
```

---

## 📌 HATEOAS: Navegação RESTful

Para tornar a API realmente RESTful, cada resposta contém **links** indicando possíveis ações futuras, evitando que o cliente precise conhecer todas as rotas.

**Exemplo de resposta:**

```json
{
    "id": 1,
    "name": "Camisa Preta",
    "price": 49.90,
    "_links": {
        "self": { "href": "/products/1" },
        "buy": { "href": "/orders", "method": "POST" },
        "reviews": { "href": "/products/1/reviews" }
    }
}
```

Os links são gerados dinamicamente pela API, dentro dos **Controllers ou Services**.

---

## 📌 Autenticação com JWT

A API utiliza **JSON Web Token (JWT)** para autenticação segura.

### 🔹 **Fluxo de Autenticação**

1. O usuário faz login enviando `POST /login` com suas credenciais.
2. A API valida as credenciais e gera um token JWT.
3. Em cada requisição protegida, o cliente envia o token no cabeçalho `Authorization`.
4. O backend valida o token antes de processar a requisição.

### 🔹 **Exemplo de Token JWT**

```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

## 📌 Configuração do Servidor

1. **Requisitos:**

   - PHP 8+
   - MySQL ou MariaDB
   - Apache/Nginx

2. **Configuração do **``** para URL amigáveis:**

   ```apache
   RewriteEngine On
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule ^(.*)$ /public/index.php?request=$1 [QSA, L]
   ```

   Isso redireciona todas as requisições para `index.php`, permitindo um roteamento limpo.

---

## 📌 Como Rodar o Projeto

1. Clone o repositório:

   ```sh
   git clone https://github.com/seu-usuario/ecommerce-api.git
   ```

2. Configure o banco de dados em `/config/database.php`.

3. Inicie um servidor embutido PHP:

   ```sh
   php -S localhost:8000 -t public/
   ```

4. Teste a API:

   ```sh
   curl -X GET http://localhost:8000/products
   ```
  A api pode ser testada em outros programas com postman ou insomnia (;
---

## 📌 Próximos Passos

- **Criar testes automatizados para a API** 
- **Melhorar o sistema de permissões para administradores e clientes** (prioridade)
- **Criar um painel administrativo em um frontend separado**

