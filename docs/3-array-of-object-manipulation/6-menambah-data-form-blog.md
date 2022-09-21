---
sidebar_position: 6
---

# 6. Store data form blog

import useBaseUrl from '@docusaurus/useBaseUrl';

Setelah pengguna mengirim data dari form blog, kita mengumpulkan semua data tersebut menjadi sebuah `struct` dan disimpan dalam sebuah `variable`. Kemudian kita `append` atau masukkan data yang berupa object tersebut kedalam variable `Blogs`.

<br />

<a class="btn-example-code" href="">
Contoh code
</a>

<br />
<br />

```go {22-32} title="main.go"
// this code below func blogDetail(w http.ResponseWriter, r *http.Request) {
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

func addBlog(w http.ResponseWriter, r *http.Request) {
	err := r.ParseForm()
	if err != nil {
		log.Fatal(err)
	}

	title := r.PostForm.Get("title")
	content := r.PostForm.Get("content")

	var newBlog = Blog{
		Title:     title,
		Post_date: time.Now().String(),
		Author:    "Ilham Fathullah",
		Content:   content,
	}

	Blogs = append(Blogs, newBlog)

	http.Redirect(w, r, "/blog", http.StatusMovedPermanently)
}

// continuation this code same like before
```
<img alt="image1" src={useBaseUrl('img/docs/image-3-5.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://ebook-code-result-chapter-2-git-day3-5add-a5efea-demo-dumbways.vercel.app//blog">
Demo
</a>
</div>
<br />

Data yang kita kumpulkan didalam sebuah object antara lain `Title`, `Post_date`, `Author`, dan `Content`. Dimana data yang kita dapatkan dari inputan pengguna adalah data `Title` dan `Content`. Kemudian kita menggunakan function `append` untuk memasukkan value ke sebuah `slice` dan disimpan di paling akhir / paling kanan.
