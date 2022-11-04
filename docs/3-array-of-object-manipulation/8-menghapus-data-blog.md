---
sidebar_position: 8
---

# 8. Delete blog data

import useBaseUrl from '@docusaurus/useBaseUrl';

Kita perlu membuat sebuah route untuk menangani proses menghapus data blog.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-7-delete-blog-data/main.go">
Contoh code
</a>

<br />
<br />

```go {16,25-33} title="main.go"
// continuation this code same like before
// this code below var Blogs = []Blog{
func main() {
	route := mux.NewRouter()

	// static folder
	route.PathPrefix("/public/").Handler(http.StripPrefix("/public/", http.FileServer(http.Dir("./public/"))))

	// routing
	route.HandleFunc("/", helloWorld).Methods("GET")
	route.HandleFunc("/home", home).Methods("GET").Name("home")
	route.HandleFunc("/blog", blogs).Methods("GET")
	route.HandleFunc("/blog/{id}", blogDetail).Methods("GET")
	route.HandleFunc("/add-blog", formBlog).Methods("GET")
	route.HandleFunc("/blog", addBlog).Methods("POST")
	route.HandleFunc("/delete-blog/{id}", deleteBlog).Methods("GET")
	route.HandleFunc("/contact-me", contactMe).Methods("GET")

	fmt.Println("Server running on port 5000")
	http.ListenAndServe("localhost:5000", route)
}

// continuation this code same like before
// this code below func addBlog(w http.ResponseWriter, r *http.Request) {
func deleteBlog(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")

	id, _ := strconv.Atoi(mux.Vars(r)["id"])

	Blogs = append(Blogs[:id], Blogs[id+1:]...)

	http.Redirect(w, r, "/blog", http.StatusMovedPermanently)
}

func contactMe(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")

	var tmpl, err = template.ParseFiles("views/contact.html")
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte("message : " + err.Error()))
		return
	}

	w.WriteHeader(http.StatusOK)
	tmpl.Execute(w, Data)
}
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

Nama route yang kita gunakan untuk menghandle proses menghapus data blog yaitu `/delete-blog`, kemudian diikuti `/{index}` agar kita dapat menangkap `index` yang dikirim melalui route/url. Untuk mengambil `index` yang dikirim, kita gunakan `mux.Vars(r)["id"]`, jadi index tersebut tersimpan didalam `request`.

Setelah mendapatkan value `index`, kita tampung dalam sebuah variable `id`. Menghapus data kita menggunakan cara dengan mereplace seluruh data yang ada dalam `slice Blogs` dengan data selain data yang dihapus. Kemudian kita gunakan perintah `redirect` agar pengguna dapat diarahkan ke route yang telah diatur, contoh: kembali ke halaman blog `http.Redirect(w, r, "/blog", http.StatusMovedPermanently)`
