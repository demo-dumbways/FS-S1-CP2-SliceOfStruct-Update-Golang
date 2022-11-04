---
sidebar_position: 5
---

# 5. Adding form blog method

import useBaseUrl from '@docusaurus/useBaseUrl';

Untuk menambahkan data blog kita perlu mempersiapkan form yang digunakan untuk mengisi data.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-4-adding-form-blog-method/views/form-blog.html">
Contoh code
</a>

<br />
<br />

```html {33,37,41,45,48} title="form-blog.html"
<!DOCTYPE html>
<html>

<head>
  <title>Blog Form With Bootstrap</title>
  <link rel="stylesheet" href="/public/style.css">
  <!-- linking boostrap css cdn  -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
</head>

<body>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-lg">
      <a class="navbar-brand me-5" href="/home">
        <img src="/public/assets/logo.png" alt="logo" />
      </a>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" href="/home">Home</a>
          </li>
          <li class="nav-item">
            <a href="/blog" class="nav-link list-active">Blog</a>
          </li>
        </ul>
      </div>
      <div class="d-flex contact-me">
        <a href="/contact-me"> Contact Me </a>
      </div>
    </div>
  </nav>
  <form class="form-container" action="/blog" method="POST">
    <h1>Create Post Blog</h1>
    <div>
      <label for="input-title" class="form-label">Title</label>
      <input id="input-title" name="title" class="form-control" />
    </div>
    <div>
      <label for="input-content" class="form-label">Content</label>
      <textarea id="input-content" name="content" class="form-control"></textarea>
    </div>
    <div>
      <label for="input-image" class="form-label">Upload Image</label>
      <input class="form-control" type="file" id="input-image">
    </div>
    <div class="d-flex justify-content-end">
      <button type="submit" class="btn">Post Blog</button>
    </div>
  </form>
</body>

</html>
```
<img alt="image1" src={useBaseUrl('img/docs/image-3-4.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://ebook-code-result-chapter-2-git-day3-4prep-4d00d7-demo-dumbways.vercel.app/add-blog ">
Demo
</a>
</div>
<br />

Yang perlu disiapkan sebagai berikut:

- Pada tag `form`, tambahkan attribute `action` dan ketiklah `route` yang akan menghandle data yang diisi, tambahkan attribute `method` dan ketikkan `POST`.
- Pada tag `input`, tambahkan attribute `name` dan ketiklah sesuai dengan data yang ingin diisi pada tag tersebut.
- Pada tag `button`, tambahkan attribute `type` dengan `value submit`