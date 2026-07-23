# Crawler-Scraping-News-Site
Program ini merupakan web crawler yang menggunakan Bahasa Pemrograman Python untuk mengumpulkan artikel berita dari website "bisnis.com".
- Backtrack : Mengekstrak artikel berdasarkan rentang tanggal publikasi yang sudah ditentukan.
- Standard : Mengekstrak artikel secara berkala untuk mengambil artikel dari yang terbaru.

Untuk setiap artikel, crawler mengekstrak informasi berikut:

1. URL artikel
2. Judul artikel
3. Tanggal publikasi
4. Isi artikel

Seluruh hasil ekstraksi disimpan dalam format JSON.

</> Arsitektur Proyek

Notebook dibagi menjadi tiga bagian utama:

Shared Functions

├── Library
├── Global Config
├── URL Validation
├── Article Url Crawler
├── Global Scraping Config
└── Import as JSON

├── Backtrack Crawler
│   └── Mengekstrak artikel berdasarkan rentang tanggal publikasi
│
└── Mode Standard
    └── Mengekstrak artikel dari yang terbaru

Struktur ini mengurangi duplikasi kode karena kedua mode menggunakan function/prosedur yang sama.

</> Shared Functions
Shared Functions berisi function/prosedur yang digunakan oleh kedua mode crawler.

1. Global Config
	- get_soup()
		Mengambil halaman web dan mengubahnya menjadi objek BeautifulSoup.

2. URL Validation
	- normalize_url()
		Mengubah URL relatif menjadi URL absolut serta menghapus parameter atau fragment yang tidak diperlukan.
	- is_bisnis_url()
		Memeriksa apakah URL berasal dari domain Bisnis.com.
	- is_article_url()
		Memastikan apakah URL mengarah ke halaman artikel.
	- parse_date(), parse_input_date(), is_date_in_range()
		Fungsi-fungsi ini digunakan untuk mengonversi tanggal publikasi menjadi datetime serta memeriksa apakah artikel berada dalam rentang tanggal yang telah ditentukan.

3. Article Url Crawler
	- crawl_article_urls()
		Melakukan crawling pada halaman daftar berita dan mengumpulkan URL artikel yang valid.

4. Parsing Artikel
	- get_meta(), find_article_json(), get_json_ld(), get_article_text(), scrape_article()
		Fungsi-fungsi ini digunakan untuk mengekstrak informasi artikel, meliputi:
			1. Judul
			2. Tanggal publikasi
			3. Isi artikel

5. Penyimpanan Data
	- save_articles()
		Menyimpan hasil crawling ke dalam file berformat JSON.


</> Note 
- Crawler menggunakan jeda antar session (REQUEST_DELAY) yang dapat dikonfigurasi untuk menghindari pengiriman request secara berlebihan ke server.
- Mode Standard menggunakan variable seen_links untuk mencegah pemrosesan artikel yang sama selama notebook masih berjalan.
- Jika notebook atau runtime di-restart, maka seen_links akan dikosongkan sehingga artikel yang sama bisa diekstrak kembali.
