# Book Notes

Book Notes is a personal reading journal built with Node.js, Express, EJS, and PostgreSQL. Record books you've read, rate and review them, keep notes, and revisit your reading history. Book cover images are requested from the Open Library Covers API using each book's ISBN.

## Features

- Add, edit, and delete book entries
- Save an ISBN, rating, review, notes, and date read for each book
- Browse entries sorted by rating, date read, or title
- View reading statistics and a page of all reviews and notes

## Requirements

- Node.js 18 or later
- PostgreSQL database

## Setup

1. Install the dependencies:

   ```sh
   npm install
   ```

2. Create a PostgreSQL database and set the connection string in a `.env` file in the project root:

   ```env
   DATABASE_URL=postgresql://USERNAME:PASSWORD@HOST:5432/DATABASE
   PORT=3000
   ```

   `PORT` is optional; the app defaults to `3000`. The PostgreSQL client is configured to use SSL, so use a database provider that supports SSL.

3. Create the table expected by the app:

   ```sql
   CREATE TABLE bookstore (
       id SERIAL PRIMARY KEY,
       title TEXT NOT NULL,
       author TEXT NOT NULL,
       isbn TEXT NOT NULL,
       rating INTEGER NOT NULL CHECK (rating BETWEEN 1 AND 5),
       review TEXT NOT NULL,
       notes TEXT NOT NULL,
       date_read DATE NOT NULL,
       cover_url TEXT,
       created_at TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP
   );
   ```

4. Start the server:

   ```sh
   npm start
   ```

5. Open [http://localhost:3000](http://localhost:3000) (or the port configured in `PORT`).

## Routes

| Method | Path | Description |
| --- | --- | --- |
| `GET` | `/` | View books and reading statistics; optionally sort with `?sort=rating`, `?sort=recent`, or `?sort=title` |
| `GET` | `/add` | Open the add-book form |
| `POST` | `/add` | Save a new book |
| `GET` | `/edit/:id` | Open a book for editing |
| `POST` | `/edit/:id` | Save edits to a book |
| `POST` | `/delete/:id` | Delete a book |
| `GET` | `/reviews` | View saved reviews and notes |
| `GET` | `/about` | View information about the project |

## Scripts

- `npm start` starts the application with Node.js.
- `npm run dev` is configured to run Nodemon, but Nodemon is not currently declared as a project dependency.
- `npm test` is a placeholder and currently exits with an error because no tests are configured.
