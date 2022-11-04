---
sidebar_position: 4
---

# 4. Showing data blog

import useBaseUrl from '@docusaurus/useBaseUrl';

Menampilkan data pada **Template HTML** kita menggunakan **double curly brackets**, contoh `{{.Blogs}}`. Karena data yang dikirim adalah semua data blog, maka kita harus melakukan `looping/perulangan` menggunakan `{{range}}` untuk menampilkan semua data blog tersebut.

**range** sama halnya seperti looping for yang telah kita pelajari pada chapter satu. Fungsinya sama yakni untuk melakukan eksekusi code secara berulang sejumlah kondisi yang ditentukan.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-3-showing-data-blog/views/blog.html">
Contoh code
</a>

<br />
<br />

```html {43-68} title="blog.html"
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
        {{if $.Data.IsLogin}}
        <div class="button-group">
          <a class="btn-edit">Edit Post</a>
          <a class="btn-post">Delete Blog</a>
        </div>
        {{end}}
        <h1>
          <a href="/blog/1" target="_blank">
            {{$data.Title}}
          </a>
        </h1>
        <div class="detail-blog-content">
          {{$data.Post_date}} | {{$data.Author}}
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

<img alt="image1" src={useBaseUrl('img/docs/image-3-2.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="">
Demo
</a>
</div>
<br />

Kita akan coba juga untuk menampilkan data blog pada halaman **detail blog**, pertama kita harus menentukan data yang akan ditampilkan. Hal ini bisa kita tentukan berdasarkan index yang kita dapatkan dari proses looping, sehingga pada file `main.go` bisa kita terima dan kita lakukan filter.


<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-3-showing-data-blog/main.go">
Contoh code
</a>

<br />
<br />

```go {15-31} title="main.go"
// this code same like before
// this code below func blogs(w http.ResponseWriter, r *http.Request) {
func blogDetail(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "text/html; charset=utf-8")

    id, _ := strconv.Atoi(mux.Vars(r)["id"])

    var tmpl, err = template.ParseFiles("views/blog-detail.html")
    if err != nil {
        w.WriteHeader(http.StatusInternalServerError)
        w.Write([]byte("message : " + err.Error()))
        return
    }

    BlogDetail := Blog{}

    for i, data := range Blogs {
      if i == id {
        BlogDetail = Blog{
          Title:     data.Title,
          Post_date: data.Post_date,
          Author:    data.Author,
          Content:   data.Content,
        }
      }
    }

    resp := map[string]interface{}{
      "Data": Data,
      "Blog": BlogDetail,
    }

    w.WriteHeader(http.StatusOK)
    tmpl.Execute(w, resp)
}

func formBlog(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")

	var tmpl, err = template.ParseFiles("views/form-blog.html")
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte("message : " + err.Error()))
		return
	}

	w.WriteHeader(http.StatusOK)
	tmpl.Execute(w, Data)
}
// continuation this code same like before
```


Maka untuk mengakses data blog detail yang dikirimkan pada halaman `blog-detail.html` sebagai berikut.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-3-showing-data-blog/views/blog-detail.html">
Contoh code
</a>

<br />
<br />

```html {35-44} title="blog-detail.html"
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

  <!-- Blog -->
  <div class="blog-detail">
    <div class="blog-detail-container">
      <h1>{{.Blog.Title}}</h1>
      <div class="author"> {{.Blog.Post_date}} | {{.Blog.Author}}</div>
      <img src="/public/assets/blog-img-detail.png" alt="detail" />
      <p>
        {{.Blog.Content}}
      </p>
    </div>
  </div>
</body>

</html>
```

<img alt="image1" src={useBaseUrl('img/docs/image-3-3.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="">
Demo
</a>
</div>

