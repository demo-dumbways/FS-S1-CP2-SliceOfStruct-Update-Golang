---
sidebar_position: 2
---

# 2. Variable Declaration

Untuk menyimpan data blog kita perlu membuat atau deklarasi sebuah `variable` yang akan menyimpan data blog. Didalam `variable` tersebut kita akan menyisipkan sebuah data blog didalam `Array`.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day3-1.variable-declaration">
Contoh code
</a>

<br />
<br />

```js {4-18} title=index.js
// this code below app.use("/public", express.static(path.join(__dirname, "../public")));
app.use(express.urlencoded({ extended: false }))

const blogs = [
  {
    id: 1,
    title: 'Pasar Coding di Indonesia Dinilai Masih Menjanjikan',
    post_date: '12 Jul 2021 22:30 WIB',
    author: 'Ichsan Emrald Alamsyah',
    content: `Ketimpangan sumber daya manusia (SDM) di sektor digital masih
    menjadi isu yang belum terpecahkan. Berdasarkan penelitian
    ManpowerGroup, ketimpangan SDM global, termasuk Indonesia,
    meningkat dua kali lipat dalam satu dekade terakhir. Lorem ipsum,
    dolor sit amet consectetur adipisicing elit. Quam, molestiae
    numquam! Deleniti maiores expedita eaque deserunt quaerat! Dicta,
    eligendi debitis?`,
  },
];

app.get('/', function (req, res) {
    res.send("Hello World")
})
```

Data blog akan bertipe object dimana memiliki beberapa property antara lain `id`, `title`, `post_data`, `author`, dan `content`.
