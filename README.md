# Book Club 📚

A shared monthly reading list with book details and ratings from club members.

[Open Book Club](https://teal-cheesecake-c8ccf0.netlify.app/)

## Features

- Add a book for a month and year, with its author and genre.
- Sort the list by month, genre, or average rating.
- Submit named ratings from 1 to 10 and view individual scores.
- Delete individual ratings, clear a book's ratings, or remove a book.
- Search Google for more information about a book.

## How it works

`index.html` contains the HTML, CSS, and JavaScript. The browser loads Supabase JS v2 from jsDelivr and reads and writes books and ratings in Supabase. Netlify hosts the page and is connected to this repository.

There is no package installation or build step.

## Run locally

With Python 3 installed, run this from the repository folder:

```sh
python3 -m http.server 8000
```

Open [localhost:8000](http://localhost:8000). Internet access is required for Supabase and the JavaScript CDN.

The checked-in page points to the live database. For a separate copy or development environment, change `SUPABASE_URL` and `SUPABASE_KEY` in `index.html` to your own project before adding or deleting data.

## Database setup

The code expects these tables and columns:

| Table | Columns used by the app |
| --- | --- |
| `books` | `id`, `month`, `year`, `name`, `author`, `genre` |
| `ratings` | `id`, `book_id`, `rating`, `rater_name` |

Months use JavaScript's zero-based numbering: January is `0`, December is `11`. Ratings refer to books through `book_id`. The interface allows one book per month/year; database constraints should enforce this for a new setup. Decide how related ratings are handled when deleting a book.

Database schema migrations and access policies are not included in this repository. Configure these in your own Supabase project. The app has no sign-in flow; access is controlled by the database's permissions and row-level security policies. Use a browser-safe publishable key, never a secret or service-role key.

## Deploy and edit

Edit `index.html`, commit, and push to `main`. The connected Netlify project can deploy changes automatically. For a new static Netlify site, publish the repository root and leave the build command empty.

Book and rating records live in Supabase, not in Git. Changing database structure requires a separate database update.
