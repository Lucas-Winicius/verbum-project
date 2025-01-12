# Verbum

**Verbum** is a library management API that allows users to create new libraries and manage books individually.

With **Verbum**, we aim to provide a comprehensive solution for managing libraries of all sizes. Our API enables adding books with detailed information, creating libraries with administrators, and performing efficient searches within the collection.

# Project Structure

First, let’s clarify some project standards, including essential elements like the database and routes. These are merely recommendations—you are free to design your own structure.

### Library Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id  | int | - |
| public_id | string | URL-like pattern (e.g., my-cool-library) |
| private | boolean | - |
| name | string | - |
| about | string | - |
| owner | User(id) | References the owner |
| location | string | - |
| moderators | User[](id) | References helpers |
| books | Books[](id) | References multiple books |
| created_at | Date | - |

### User Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | int | - |
| name | string | - |
| nick | string | - |
| email | string | - |
| password | string | - |
| about | string | - |
| libraries | Library[](id) | - |
| created_at | Date | - |

### Book Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | - |
| name | string | - |
| category | string | - |
| author | string | - |
| amount | string | - |
| synopsis | string | - |
| comments | Comments[] | References comments |
| library | Library(id) | References the library |
| created_at | Date | - |

### Lending Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | - |
| book_id | Book(id) | References the book |
| collected_at | Date | - |
| returned | boolean | - |
| returned_at | Date | nullable | - |
| user_name | string | - |
| user_email | string | - |
| user_tel | string | - |
| notes | string | - |

### Comments Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | - |
| author_id | User(id) | References the user |
| book_id | Book(id) | References the book |
| content | string | - |
| rating | number | Book rating |
| created_at | Date | - |

### Library Statistics Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | - |
| library_id | int | References the library |
| month_year | string | Month and year representation (MM-YYYY) |
| books_added | int | Number of books added during the month/year |
| total_books | int | Total books in the collection after the month/year |
| average_borrow_time | int[] | Average borrowing time in hours |
| total_borrows | int | Total borrowings completed |
| total_returns | int | Total returns completed |
| created_at | Date | - |

### Search Patterns Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | Unique search record identifier |
| search_term | string | Search term |
| user_id | id | References the user who performed the search |
| search_date | Date | Search date |
| results_count | int | Number of returned results |
| your_results | int | Results featuring your entries |

### Events Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | Unique event identifier |
| library_id | int | nullable | References the library |
| title | string | Event title |
| description | string | Event description |
| event_date | Date | Event date and time |
| ends_at | Date | End date |
| organizer_id | int | References the organizer (User) |
| status | Planned Cancelled Postponed Completed | Event status |
| link | string | nullable | - |
| created_at | Date | - |

### Notifications Table

| **Column Name** | **Type** | **Notes** |
| --- | --- | --- |
| id | string | Identifier |
| library_id | int | nullable | References the library |
| title | string | - |
| content | string | - |
| hide_at | Date | Expiration date |
| created_at | Date | - |

For optimal functionality, every user should be able to access any library and, if desired, create their own. Below are suggested routes and functionalities.

## User

- Create User - `PUT /user`
- View a User - `GET /user/{nick}`
- Edit Profile - `PATCH /user/{nick}`

## Library

- Create a new library - `PUT /library`
- View a single library - `GET /library/{library_id}`
- Edit library - `PATCH /library/{library_id}`
- Add moderators - `PUT /library/{library_id}/moderator`
- Remove moderator - `DELETE /library/{library_id}/moderator`
- View moderators - `GET /library/{library_id}/moderator`
- Add books - `PUT /library/{library_id}/book`
- Remove books - `DELETE /library/{library_id}/book`
- View books - `GET /library/{library_id}/book`
- View a single book - `GET /book/{book_id}`
- Search libraries - `GET /library?q=`
- Borrow books - `PUT /library/{library_id}/lending`
- Return books - `DELETE /library/{library_id}/lending`
- View all borrowings - `GET /library/{library_id}/lending`
- Create a comment - `PUT /library/{library_id}/comment`
- Delete a comment - `DELETE /library/{library_id}/comment`
- Create a notification - `PUT /library/{library_id}/notification`
- Edit a notification - `PATCH /library/{library_id}/notification`

## Events

- Create a new event - `PUT /events`
- View a single event - `GET /events/{event_id}`
- Edit an event - `PATCH /events/{event_id}`
- Cancel an event - `DELETE /events/{event_id}`

# Design

If you’d like, we also have a frontend template saved in Figma.

- [Figma](https://www.figma.com/design/xwYF27qE2els9kG9M4yPGu/Verbum?node-id=0-1&t=P73fi4PmTxu0OA1b-1)

# Final Considerations

Thank you for reading this far! I hope you enjoyed it. I encourage you to create your version of the project, whether following my guidelines or using a more creative approach. To view my version, check the links below. Feel free to share your version with me via my social media links below, and don’t forget to follow me!

## Follow me on Social Media!

- [GitHub/@Lucas-Winicius](https://github.com/Lucas-Winicius/)
- [LinkedIn/Lucas-Winicius-Souza](https://www.linkedin.com/in/lucas-winicius-souza/)
- [Instagram/@Luk.Winicius](https://www.instagram.com/luc.winicius/)
- [Notion Project Page](https://mountain-parka-6b1.notion.site/Verbum-11018dcd61ef807d84f8f34011570300)
