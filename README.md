# Max Made Products

This repo holds the source files for [maxmadeproducts.com](https://maxmadeproducts.com/) — the website showcasing things Max has made. You don't need to be a programmer to add a product here; this guide walks through it step by step.

## Clone the repo

"Cloning" just means downloading a copy of this project onto your computer.

1. Install [Git](https://git-scm.com/downloads) if you don't already have it.
2. Open a terminal and run:

   ```
   git clone https://github.com/lviss/maxmadeproducts.com.git
   ```

3. This creates a `maxmadeproducts.com` folder with everything in it.

If you'd rather not touch the terminal at all, [GitHub Desktop](https://desktop.github.com) does the same thing with buttons and windows instead of typed commands — it's a friendlier way to clone the repo, make changes, and open pull requests (see [Submit a PR](#submit-a-pr) below).

## Install Hugo

This site is built with [Hugo](https://gohugo.io), a tool that turns simple text files into the actual website. To preview your changes before they go live, you'll need it installed locally.

1. Go to the [official Hugo install instructions](https://gohugo.io/installation/) and follow the steps for your operating system.
2. **Important:** install the **extended** version — the site's theme needs it to work correctly. The install docs make it clear which download or command gives you the extended edition.
3. Try to match version **0.166.0**, since that's the version used to build the live site (check `.github/workflows/hugo.yml` if it's ever updated) — this keeps your local preview looking the same as what actually gets published.

On a Mac, the quickest way is:

```
brew install hugo
```

On Windows or Linux, follow the [official docs](https://gohugo.io/installation/) for the option that matches your system.

## Add a new product

1. Create a new folder for your product under `content/`, e.g. `content/my_new_product/`. Use lowercase words separated by underscores for the folder name.
2. Inside your new product folder, create a file named `index.md` with this format at the top (this is called "front matter" — it's metadata Hugo reads before the product description):

   ```
   +++
   date = '2026-09-10T08:01:51-07:00'
   draft = false
   title = 'My new product'
   +++
   A description of the product goes here!
   ```

   - `date` — when the product was added (any reasonable date/time works).
   - `draft` — set to `false` so the product actually appears on the live site. (If you leave it as `true`, it stays hidden from everyone except you previewing locally.)
   - `title` — the product's name, shown on the site.

3. To add a photo, drop the image file (e.g. `product.jpg`) into the same product folder as `index.md`, then reference it in the description like this:

   ```
   ![A short description of the photo](product.jpg "A short description of the photo")
   ```

## Preview locally

Before sharing your changes, you can see exactly how they'll look on the real site:

1. Open a terminal in the repo folder.
2. Run:

   ```
   hugo server -D
   ```

   The `-D` flag also shows any products still marked `draft = true`, so you can preview your work before you're ready to make it public.
3. Hugo will print a local address, usually `http://localhost:1313/` — open that in your browser to see the site.
4. Leave the command running while you edit; the preview updates automatically as you save changes. Press `Ctrl+C` in the terminal to stop it when you're done.

## Submit a PR

Once your product entry looks good, it needs to be reviewed before it goes live. This happens through a "pull request" (or "PR") — a request to merge your changes into the live site, which the repo owner (Lane) reviews and approves before anything is published.

**Easiest way — no terminal needed:**

1. On GitHub, navigate to the file or folder you want to add or change (or use "Add file" to create a new one).
2. Click the pencil (✏️) icon to edit, or use "Add file" to upload a new product entry and its photo.
3. Make your changes, then scroll down and save. GitHub will automatically offer to open a pull request for you (usually labeled "Propose changes") — just follow the prompts.

This is the quickest option for a small text fix or a straightforward new product entry.

**Local way — if you're previewing your product entry first (per the steps above):**

1. Create a new branch — think of this as a separate workspace for your changes so you don't affect the live site directly:

   ```
   git checkout -b my-product-branch
   ```

2. Add and commit your changes:

   ```
   git add .
   git commit -m "Add my product"
   ```

3. Push your branch and open a pull request:

   ```
   git push -u origin my-product-branch
   ```

   Then go to GitHub, and it will offer to open a pull request from your new branch.

If you're using GitHub Desktop instead of the terminal, it has the same steps as clickable buttons: create a branch, commit your changes, push, and click "Create Pull Request."

Either way, once your pull request is open, Lane will review it and merge it — and your product entry will go live on the site.
