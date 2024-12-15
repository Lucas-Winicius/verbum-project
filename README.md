# Verbum

O "**Verbum**" é uma API de gerenciamento de bibliotecas que permite criar novas **Verbum** e gerenciar livros individualmente.

Com o "Verbum", buscamos oferecer uma solução abrangente para o gerenciamento de bibliotecas de todos os portes. Nossa API permite adicionar livros com seus respectivos dados, criar bibliotecas com seus administradores e realizar buscas eficientes no acervo.

# Estrutura do projeto

Primeiramente, quero esclarecer alguns padrões do projeto, incluindo elementos essenciais como banco de dados e rotas. É importante lembrar que estas são apenas recomendações – você está livre para desenvolver sua própria estrutura.

### Tabela da Biblioteca

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id  | int | - |
| public_id | string | Ter padrão de url (biblioteca-legal) |
| private | boolean |  |
| name | string | - |
| about | string | - |
| owner | User(id) | Referencia o dono |
| location | string | - |
| moderators | User[](id) | Referencia os ajudantes |
| books | Books[](id) | Referencia vários livros |
| created_at | Date | - |

### Tabela do Usuário

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | int | - |
| name | string | - |
| nick | string | - |
| email | string | - |
| password | string | - |
| about | string | - |
| libraries | Library[](id) | - |
| created_at | Date | - |

### Tabela de Livros

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | - |
| name | string | - |
| category | string | - |
| author | string | - |
| amount | string | - |
| synopsis | string | - |
| comments | Comments[] | Refencia o comentario |
| library | Library(id) | Refencia a biblioteca |
| created_at | Date | - |

### Tabela de Empréstimos

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | - |
| book_id | Book(id) | Refencia o Livro |
| collected_at | Date | - |
| returned | boolean | - |
| returned_at | Date | null | - |
| user_name | string | - |
| user_email | string | - |
| user_tel | string | - |
| notes | string | - |

### Tabela de comentarios

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | - |
| author_id | User(id) | Refencia ao usuário |
| book_id | Book(id) | Referencia o livro |
| content | string | - |
| rating | number | Nota do livro |
| created_at | Date | - |

### Tabela de estatísticas da biblioteca

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | - |
| library_id | int | Referência à biblioteca |
| month_year | string | Representação do mês e ano (MM-AAAA) |
| books_added | int | Número de livros adicionados no mês/ano |
| total_books | int | Total de livros no acervo após o mês/ano |
| average_borrow_time | int[] | Tempo médio de empréstimo em horas |
| total_borrows | int | Total de empréstimos realizados |
| total_returns | int | Total de devoluções realizadas |
| created_at | Date | Data do registro |

### Tabela de padrões de Busca

| **Nome da coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | Identificador único do registro de busca |
| search_term | string | Termo buscado |
| user_id | id | Referência ao usuário que realizou a busca |
| search_date | Date | Data da busca |
| results_count | int | Número de resultados retornados |
| your_results | int | Número de resultados retornados que apareciam você |

### Tabela de Eventos

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | Identificador único do evento |
| library_id | int | null | Referência à biblioteca (Library) |
| title | string | Título do evento |
| description | string | Descrição do evento |
| event_date | Date | Data e horário do evento |
| ends_at | Date | Data de encerramento |
| organizer_id | int | Referência ao organizador (User) |
| status | Planned Cancelled Postponed Completed | Status do evento (planejado, concluído, cancelado) |
| link | string | null |  |
| created_at | Date | Data de criação do evento |

### Tabela de Notificações

| **Nome da Coluna** | **Tipo** | **Observações** |
| --- | --- | --- |
| id | string | Identificador |
| library_id | int | null | Referência à biblioteca (Library) |
| title | string | - |
| content | string | - |
| hide_at | Date | Quando a notificação desaparecerá |
| created_at | Date | - |

Para um melhor funcionamento, é importante que todo usuário possa acessar qualquer biblioteca e, caso queira, possa criar a sua própria. Quanto às rotas, listarei abaixo sugestões de rotas e funcionalidades.

## Usuário

- Criar Usuário - `PUT /user`
- Ver um usuario - `GET /user/{nick}`
- Editar Perfil - `PATCH /user/{nick}`

## Biblioteca

- Criar uma nova biblioteca - `PUT /library`
- Ver uma unica biblioteca - `GET /library/{library_id}`
- Editar a biblioteca - `PATCH /library/{library_id}`
- Adicionar moderadores - `PUT /library/{library_id}/moderator`
- Remover moderador - `DELETE /library/{library_id}/moderator`
- Ver moderadores - `GET /library/{library_id}/moderator`
- Adicionar livros - `PUT /library/{library_id}/book`
- Remover livros - `DELETE /library/{library_id}/book`
- Ver livros - `GET /library/{library_id}/book`
- Ver um unico livro - `GET /book/{book_id}`
- Buscar bibliotecas - `GET /library?q=`
- Emprestar livros - `PUT /library/{library_id}/lending`
- Devolver livros - `DELETE /library/{library_id}/lending`
- Ver todos os emprestimos `GET /library/{library_id}/lending`
- Criar um comentario - `PUT /library/{library_id}/comment`
- Deletar um comentario - `DELETE /library/{library_id}/comment`
- Criar uma notificação - `PUT /library/{library_id}/notification`
- Editar uma notificação - `PATCH /library/{library_id}/notification`

## Eventos

- Criar um novo evento - `PUT /events`
- Ver um uníco evento - `GET /events/{event_id}`
- Editar um evento existente - `PATCH /events/{event_id}`
- Cancelar um evento - `DELETE /events/{event_id}`

# Desing

Caso deseje, também temos um template de frontend, o qual esta salvo no figma.

- [Figma](https://www.figma.com/design/xwYF27qE2els9kG9M4yPGu/Verbum?node-id=0-1&t=P73fi4PmTxu0OA1b-1)

# Considerações Finais

Caso tenha chegado até aqui, agradeço e espero que tenha gostado. Além disso, convido você a criar sua própria versão do projeto, seja seguindo minhas diretrizes ou de uma forma mais livre. Se quiser ver a minha versão, basta acessar os links abaixo. Caso deseje me mostrar a sua versão, envie-a através de uma das minhas redes sociais listadas abaixo. Não se esqueça de me seguir lá também!

## Me siga nas redes!

- [GitHub/@Lucas-Winicius](https://github.com/Lucas-Winicius/)
- [Linkedin/Lucas-Winicius-Souza](https://www.linkedin.com/in/lucas-winicius-souza/)
- [Instagram/@Luk.Winicius](https://www.instagram.com/luc.winicius/)
- [Notion Project Page](https://mountain-parka-6b1.notion.site/Verbum-11018dcd61ef807d84f8f34011570300)
