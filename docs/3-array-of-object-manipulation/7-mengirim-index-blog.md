---
sidebar_position: 7
---

# 7. Query String Index

Pada tag `anchor` yang kita gunakan untuk menghapus blog, kita tambahkan attribute `href` kemudian tambahkan route yang menghandle proses menghapus data blog. Tambahkan juga `index` blog tersebut setelah route untuk menghapus data.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-6-query-string-index/views/blog.html">
Contoh code
</a>

<br />
<br />

```html {51,54} title="blog.html"
<html>

<head>
  <title>{{.Data.Title}}</title>
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
    {{if .Data.IsLogin}}
    <div class="button-group w-100">
      <a href="/add-blog" class="btn-post">Add New Blog</a>
    </div>
    {{end}}
    <!-- dynamic content would be here -->
    {{range $index, $data := .Blogs}}
    <div class="blog-list-item">
      <div class="blog-image">
        <img src="/public/assets/blog-img.png" alt="Pasar Coding di Indonesia Dinilai Masih Menjanjikan" />
      </div>
      <div class="blog-content">
        <div class="button-group">
          <a class="btn-edit">Edit Post</a>
          <a class="btn-post" href="/delete-blog/{{$index}}">Delete Blog</a>
        </div>
        <h1>
          <a href="/blog/{{$index}}" target="_blank">
            {{$data.Title}}
          </a>
        </h1>
        <div class="detail-blog-content">
          {{$data.Format_date}} | {{$data.Author}}
        </div>
        <p>
          {{$data.Content}}
        </p>
      </div>
    </div>
    {{end}}
  </div>
</body>

</html>
```

