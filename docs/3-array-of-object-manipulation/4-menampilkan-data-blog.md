---
sidebar_position: 4
---

# 4. Showing data blog

import useBaseUrl from '@docusaurus/useBaseUrl';

Menampilkan data pada **Handlebars** kita menggunakan **double curly brackets**, contoh `{{blogs}}`. Karena data yang dikirim adalah semua data blog, maka kita menggunakan `{{each}}` untuk menampilkan semua data blog tersebut. Dan kita menggunakan perintah `this` kemudian diikuti `property name` yang ingin ditampilkan.

**Each** sama halnya seperti looping for yang telah kita pelajari pada chapter satu. Fungsinya sama yakni untuk melakukan eksekusi code secara berulang sejumlah kondisi yang ditentukan.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day3-3.display-data">
Contoh code
</a>

<br />
<br />

```html {44-63} title=blog.hbs
<html>

<head>
  <title>Creating Blog Page</title>
  <link rel="stylesheet" href="/public/style.css" />
  <!-- linking boostrap css cdn  -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
</head>

<body>
  <!-- NavBar -->
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

  <!-- Blog list -->
  <div id="contents" class="blog-list">
    <!-- conditional post blog -->
    {{#if isLogin}}
    <div class="button-group w-100">
      <a href="/add-blog" class="btn-post">Add New Blog</a>
    </div>
    {{/if}}
    <!-- dynamic content would be here -->
    <!-- using each expression to iterate blogs data sent -->
    {{#each blogs}}
    <div class="blog-list-item">
      <div class="blog-image">
        <img src="/public/assets/blog-img.png" alt="Pasar Coding di Indonesia Dinilai Masih Menjanjikan" />
      </div>
      <div class="blog-content">
        <div class="button-group">
          <a class="btn-edit">Edit Post</a>
          <a class="btn-post">Delete Blog</a>
        </div>
        <h1>
          <a href="/blog/{{this.id}}" target="_blank">{{this.title}}</a>
        </h1>
        <div class="detail-blog-content">
          {{this.post_date}} | {{this.author}}
        </div>
        <p>{{this.content}}</p>
      </div>
    </div>
    {{/each}}
  </div>
</body>
</html>
```

<img alt="image1" src={useBaseUrl('img/docs/image-3-2.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://ebook-code-result-chapter-2-git-day3-3disp-677d78-demo-dumbways.vercel.app/blog">
Demo
</a>
</div>
<br />

Kita akan coba juga untuk menampilkan data blog pada halaman **detail blog**, karena data yang dikirim hanya satu atau bertipe **object** maka kita langsung panggil `property name` yang ingin ditampilkan.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day3-3.display-data">
Contoh code
</a>

<br />
<br />

```js {35-42} title=blog-detail.hbs
<html>

<head>
  <title>Creating Blog Page - detail</title>
  <link rel="stylesheet" href="/public/style.css" />
  <!-- linking boostrap css cdn  -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
</head>

<body>
  <!-- NavBar -->
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

  <!-- Blog -->
  <div class="blog-detail">
    <div class="blog-detail-container">
      <h1>{{blog.title}}</h1>
      <div class="author">{{blog.post_date}} | {{blog.author}}</div>
      <img src="/public/assets/blog-img-detail.png" alt="detail" />
      <p>{{blog.content}}</p>
    </div>
  </div>
</body>

</html>
```

<img alt="image1" src={useBaseUrl('img/docs/image-3-3.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://ebook-code-result-chapter-2-git-day3-3disp-677d78-demo-dumbways.vercel.app/blog/1">
Demo
</a>
</div>

