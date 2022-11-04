---
sidebar_position: 2
---

# 2. Struct Declaration

Untuk menyimpan data blog kita perlu membuat atau deklarasi sebuah `variable struct` yang akan menyimpan data blog. Didalam `variable struct` tersebut kita akan menyisipkan sebuah data blog didalam `slice`.

Go tidak memiliki class yang ada di bahasa-bahasa strict OOP lain. Tapi Go memiliki tipe data struktur yang disebut dengan Struct.

**Struct** adalah kumpulan definisi variabel (atau property) dan atau fungsi (atau method), yang dibungkus sebagai tipe data baru dengan nama tertentu. **Property** dalam struct, tipe datanya bisa bervariasi. Mirip seperti map, hanya saja key-nya sudah didefinisikan di awal, dan tipe data tiap itemnya bisa berbeda.

Dari sebuah struct, kita bisa buat variabel baru, yang memiliki atribut sesuai skema struct tersebut. Kita sepakati dalam buku ini, variabel tersebut dipanggil dengan istilah object atau object struct.

:::info
Konsep struct di golang mirip dengan konsep class pada OOP, meski sebenarnya berbeda. Di sini penulis menggunakan konsep OOP sebagai analogi, dengan tujuan untuk mempermudah dalam mencerna isi chapter ini.
:::

Dengan memanfaatkan struct, grouping data akan lebih mudah, selain itu dan rapi dan gampang untuk di-maintain.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2-golang/blob/day3-1-struct-declaration/main.go">
Contoh code
</a>

<br />
<br />

```go {7-27} title="main.go"
// this code same like before
var Data = map[string]interface{}{
	"Title": "Personal Web",
	"IsLogin": false,
}

type Blog struct {
	Title     string
	Post_date string
	Author    string
	Content   string
}

var Blogs = []Blog{
	{
		Title:     "Pasar Coding di Indonesia Dinilai Masih Menjanjikan",
		Post_date: "12 Jul 2021 22:30 WIB",
		Author:    "Ilham Fathullah",
		Content:   "Ketimpangan sumber daya manusia (SDM) di sektor digital masih
                    menjadi isu yang belum terpecahkan. Berdasarkan penelitian
                    ManpowerGroup, ketimpangan SDM global, termasuk Indonesia,
                    meningkat dua kali lipat dalam satu dekade terakhir. Lorem ipsum,
                    dolor sit amet consectetur adipisicing elit. Quam, molestiae
                    numquam! Deleniti maiores expedita eaque deserunt quaerat! Dicta,
                    eligendi debitis?",
	},
}

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
```

Data Blog akan bertipe struct dimana memiliki beberapa property antara lain `Title`, `Post_date`, `Author`, dan `Content`.
