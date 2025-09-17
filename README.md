# 🍽️ PROJETO DE EXTRAÇÃO DE DADOS DE RECEITAS E CHEFS

Este projeto tem como objetivo **extrair dados de receitas e chefs/confeiteiros** de páginas públicas,  
utilizando **Java + Spring Boot + Jsoup**.  

> ⚠️ **Atenção:** Usar URLS da wikipedia ou panelinha.com. 

--------------------------

## 1️⃣ EXTRAÇÃO DE RECEITAS

- **URL de exemplo:**  
  `https://panelinha.com.br/receita/salada-de-folhas-com-carambola`  

- **O que é extraído:**  
  - Nome da receita  
  - Ingredientes  
  - Modo de preparo  


**Requisição no Postman:**  
`` 
POST http://localhost:8081/receita/importar
``


Body (JSON):
```json
{
   "url": "https://panelinha.com.br/receita/salada-de-folhas-com-carambola"
}
```


**Resposta esperada (JSON):**

```json
{
  "titulo": "Salada de folhas com carambola",
  "ingredientes": [
    "1 maço de alface",
    "1 unidade de carambola",
    "Sal a gosto"
  ],
  "descricao": "Misture as folhas e a carambola em uma tigela e tempere com sal."
}

````
### Endpoints CRUD PADRÃO

| Operação | Endpoint | Método | Descrição |
|-----------|---------|-------|-----------|
| Criar receita manual | `/receita` | POST | Salva uma nova receita fornecida no corpo da requisição. |
| Importar receita via URL | `/receita/importar` | POST | Faz scraping da página e salva os dados extraídos. |
| Listar todas | `/receita` | GET | Retorna todas as receitas cadastradas. |
| Buscar por ID | `/receita/{id}` | GET | Retorna a receita com o ID especificado. |
| Buscar por título | `/receita/buscar?titulo={titulo}` | GET | Retorna todas as receitas que correspondem ao título (ignore case). |
| Atualizar | `/receita/{id}` | PUT | Atualiza os campos da receita com o ID especificado. |
| Deletar | `/receita/{id}` | DELETE | Remove a receita do banco de dados. |


-----------------------------------------------------------------

## 2️⃣ EXTRAÇÃO DE CHEFS / CONFEITEIROS
URL de exemplo:
https://pt.wikipedia.org/wiki/Henrique_Foga%C3%A7a

O que é extraído:

-Nome completo

-Nacionalidade

-Data de nascimento

-Email (gerado automaticamente concatenando chefe + "gmail.com")

-Senha (Nome do chefe em minusculo + data de nascimento // exemplo:henriquefogaça1974)

Requisição no Postman:
POST http://localhost:8081/confeiteiro/importar
Body (JSON):
```
{
  "url": "https://pt.wikipedia.org/wiki/Henrique_Foga%C3%A7a"
}
```
## Resposta esperada (JSON):

```json
{
  "nome": "Henrique Fogaça",
  "nacionalidade": "Brasileiro",
  "dataNascimento": "1974-11-07",
  "email": "henriquefogaca@gmail.com",
  "senha": "henriquefogaca1974"
}
```

### Endpoints CRUD PADRÃO

| Operação | Endpoint | Método | Descrição |
|-----------|---------|-------|-----------|
| Criar confeiteiro manual | `/confeiteiro` | POST | Salva um novo confeiteiro fornecido no corpo da requisição. |
| Importar confeiteiro via URL | `/confeiteiro/importar` | POST | Faz scraping da página e salva os dados extraídos. |
| Listar todos | `/confeiteiro` | GET | Retorna todos os confeiteiros cadastrados. |
| Buscar por ID | `/confeiteiro/{id}` | GET | Retorna o confeiteiro com o ID especificado. |
| Atualizar | `/confeiteiro/{id}` | PUT | Atualiza os campos do confeiteiro com o ID especificado. |
| Deletar | `/confeiteiro/{id}` | DELETE | Remove o confeiteiro do banco de dados. |


⚠️ Observações importantes
✅ As URLs devem ser válidas e acessíveis (wikipedia ou panelinha.com)

✅ O scraping respeita a estrutura atual das páginas; mudanças nos sites podem exigir ajustes nos selectors CSS

✅ Os e-mails e senhas dos chefs são gerados automaticamente a partir do nome e data de nascimento, removendo espaços e acentos

✅ Para testar, use Postman ou qualquer cliente HTTP enviando JSON no corpo da requisição (raw → JSON)

✅ Banco H2 rodando na porta 8081
