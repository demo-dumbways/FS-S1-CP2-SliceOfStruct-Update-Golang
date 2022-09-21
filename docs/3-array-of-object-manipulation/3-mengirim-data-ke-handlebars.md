---
sidebar_position: 3
---

# 3. Send data to Template

Kita akan mengirim data yang ada didalam variable **Blogs** ke halaman `blog` dan `detail blog` agar pengguna dapat melihat data blog.

<br />

<a class="btn-example-code" href="">
Contoh code
</a>

<br />
<br />

```go {26-29,32} title="main.go"
// this code same like before
func home(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "text/html; charset=utf-8")

    var tmpl, err = template.ParseFiles("views/index.html")
    if err != nil {
        w.WriteHeader(http.StatusInternalServerError)
        w.Write([]byte("message : " + err.Error()))
        return
    }

    w.WriteHeader(http.StatusOK)
    tmpl.Execute(w, Data)
}

func blogs(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "text/html; charset=utf-8")

    var tmpl, err = template.ParseFiles("views/blog.html")
    if err != nil {
        w.WriteHeader(http.StatusInternalServerError)
        w.Write([]byte("message : " + err.Error()))
        return
    }

    respData := map[string]interface{}{
        "Data":  Data,
        "Blogs": Blogs,
    }

    w.WriteHeader(http.StatusOK)
    tmpl.Execute(w, respData)
}

func blogDetail(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "text/html; charset=utf-8")

    id, _ := strconv.Atoi(mux.Vars(r)["id"])

    var tmpl, err = template.ParseFiles("views/blog-detail.html")
    if err != nil {
        w.WriteHeader(http.StatusInternalServerError)
        w.Write([]byte("message : " + err.Error()))
        return
    }

    resp := map[string]interface{}{
        "Data": Data,
        "Id":   id,
    }

    w.WriteHeader(http.StatusOK)
    tmpl.Execute(w, resp)
}
// continuation this code same like before
```

Untuk mengirim data ke **template html**, kita menambahkan `struct` pada parameter kedua **function execute**. Kita tambahkan property sesuai dengan data yang dikirim dan valuenya adalah variable yang menyimpan data tersebut.
