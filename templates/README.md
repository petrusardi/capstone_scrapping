# Web-Scrapping using Beautifulsoup

Projek ini dikembangkan sebagai salah satu capstone project dari Algoritma Academy Data Analytics Specialization.
Hasil yang diharapkan dari projek ini adalah melakukan simple webscrapping untuk mendapatkan informasi data kurs Japan Yen ke Rupiah.
Saya juga akan memanfaatkan flask dashboard sederhana untuk menampilkan hasil scrap dan visualisasi kita.

## Dependencies

- beautifulSoup4
- pandas
- flask
- matplotlib

* Membuat variabel dengan mengambil data dari web yang ditentukan.
```python
url_get = requests.get('https://news.mifx.com/kurs-valuta-asing?kurs=JPY')
```

* Beautifulsoap digunakan untuk mengubah dokumen HTML yang sulit dibaca menjadi sebuah python object.
```python
from bs4 import BeautifulSoup 
soup = BeautifulSoup(url_get.content,"html.parser")
print(type(soup))
```

* Dua code dibawah digunakan untuk mengambil data yang kita inginkan, untuk paramater-parameter didalamnya didapatkan saat
kita melakukan inspect pada web pengambilan data. 
```python
table = soup.find('table',attrs={'class':'centerText newsTable2'})
print(table.prettify()[1:500])
tr = table.find_all('tr')
```

*Kemudian saya melakukan wrangling data untuk mengambil data dan dijadikan sebuah dataframe.
```python
temp = [] #initiating a tuple

for i in range(1, len(tr)):
    row = table.find_all('tr')[i]

    tanggal = row.find_all('td')[0].text
    tanggal = tanggal.strip()

    ask = row.find_all('td')[1].text
    ask = ask.strip()

    bid = row.find_all('td')[2].text
    bid = bid.strip()
    #scrapping process
    temp.append((tanggal,ask,bid))
```

* Isi bagian ini untuk menyimpan hasil scrap menjadi sebuah dataframe.
```python
import pandas as pd

df = pd.DataFrame(temp, columns=('Tanggal','Kurs_Jual','Kurs_Beli'))
df.head()
```

* Terakhir kita dapat menggunakan fungsi `scrap` dengan cara mengisi bagian berikut dengan link web yang kita scrap.
```python
df = scrap(___) #insert url here
```

* Kita juga dapat bermain dengan UI nya pada `index.html` yang dimana dapat mengikuti comment yang ada untuk mengetahui bagian mana yang dapat diubah. 

