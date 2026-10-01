# Текстова специфікація домену та критерії прийняття (Acceptance Criteria)

## 1. Сутності та їх атрибути

### User (Користувач)
- `id`: UUID (Primary Key)
- `email`: string (Unique)
- `full_name`: string
- `created_at`: timestamp

### Author (Автор)
- `id`: UUID (Primary Key)
- `name`: string
- `bio`: text

### Book (Книга)
- `id`: UUID (Primary Key)
- `title`: string
- `isbn`: string (Unique)
- `published_year`: integer

### Loan (Видача книги — Асоціативна сутність)
*Примітка: Логічний зв'язок між User та Book з власними атрибутами.*
- `id`: UUID (Primary Key)
- `user_id`: UUID (Foreign Key -> User.id)
- `book_id`: UUID (Foreign Key -> Book.id)
- `borrowed_at`: timestamp
- `due_date`: timestamp
- `returned_at`: timestamp (optional)

---

## 2. Зв'язки між сутностями
1. **User 1 : N Loan**: Один користувач може мати декілька видач.
2. **Book 1 : N Loan**: Одна книга може видаватися декілька разів у різний час.
3. **Author M : N Book**: Один автор може написати декілька книг, і книга може мати декількох авторів. *(Оформлено як чистий зв'язок M:N без проміжної таблиці на ER-рівні)*.

---

## 3. Критерії прийняття (Prompting Criteria for AI)
- [AC-1] Усі ідентифікатори (`id`) мають уніфікований тип `UUID`.
- [AC-2] Модель відповідає вимогам 3-ї нормальної форми (3NF): відсутні транзитивні залежності.
- [AC-3] Чисті зв'язки M:N (наприклад, Author-Book) моделюються без проміжних сутностей-таблиць.
- [AC-4] Асоціативні сутності використовуються тільки тоді, коли зв'язок містить власні бізнес-атрибути (наприклад, `borrowed_at` у `Loan`).
