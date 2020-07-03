# README

## API's

### Cadastro de empresas

#### Descrição

<p align="justify"> A API de cadastro de empresas tem a funcionalidade de ao receber os dados de uma empresa, cadastra-los no nosso sistema e gerar o token para identificações dessa empresa no futuro. Assim que cadastrado os dados são devolvidos adicionando o token gerado.</p>

#### Parametros necessarios

- Model [company]
- Nome da empresa [name]
- Razão social [corporate_name]
- Endereço [address]
- CNPJ [cnpj]
- **Todos os dados devem ser enviados como um JSON**
- **Exemplo:**
  - **{ company: { name: 'TreinaDev', corporate_name: 'CampusCode', address: 'Av. Ṕaulista, 123', cnpj: ' 00.000.000/0000-00' } }**

#### Parametros devolvidos

- Nome da empresa [name]
- Razão social [corporate_name]
- Endereço [address]
- CNPJ [cnpj]
- Código gerado para identificação da empresa [token]
- ID [id]
- **Todos os dados serão enviados como um JSON**

#### Verbo HTTP

- **POST**
- Os dados devem ser enviados para seguinte rota:
  - **/api/v1/companies**

#### Possiveis erros

- Parametros obrigatorios:
  - Nome, Razão social, Endereço, CNPJ. Caso algum parametro estivem em branco a resposta será:
    - [atributo] não pode ficar em branco
  - Erros exclusivos do CNPJ:
    - **já está em uso** - Motivo: CNPJ já cadastrado
    - **não é válido** - Motivo: CNPJ incorreto, ou, fora de formatação
- Company vazio:
  - Mensagem: **param is missing or the value is empty: company**
  - Motivo: **chave company faltando no json { company: { } }**

### Cancelamento de Compra

#### Descrição

<p align="justify">A API de cancelamento permite que o cliente solicite o cancelamento de uma compra informando o token e o motivo de cancelamento (opcional). Após o sistema receber a solicitação do cliente, é necessario que um usuario do sistema autorize essa solicitação. Cada compra poderá haver somente uma solicitação de cancelamento em aberto, caso já exista, o sistema retonará um erro.</p>

#### Parametros necessarios

- Model [purchase]
- Token [token]
- Motivo do cancelamento **(OPCIONAL)** [reason]
- **Todos os dados devem ser enviados como um JSON**
- **Exemplo:**
  - **{ purchase: { token: 'ABC123'}, reason: 'String' }**

#### Parametros devolvidos

- Status da comunicação 200
- **Todos os dados serão enviados como um JSON**

#### Verbo HTTP

- **POST**
- Os dados devem ser enviados para seguinte rota:
  - **/api/v1/purchase_cancellations**

#### Possiveis erros

- Token não encontrado:
  - Status de comunicação devolvido será: **404**
- Compra já possui solicitação de cancelamento em aberto:
  - Status de comunicação devolvido será: **400**
