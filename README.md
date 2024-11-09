| Nama          | NRP        | 
| ---            | ---        | 
| Christoforus Indra Bagus Pratama | 5025231124 |

# 🌵 Soal
Untuk menjadi raja Codeforces, Kuroni harus menyelesaikan soal berikut.<br>
Dia diberikan _n_ angka _a1, a2, a3, ... , an._ <br>
Bantu Kuroni untuk menghitung _**∏1 ≤ i ≤ j ≤ n |a1 - aj|**_. <br>
Karena hasilnya bisa sangat besar, keluarkan hasilnya dalam bentuk modulo _m_.<br>
<br>
Jika Anda tidak familiar dengan notasi pendek, <br>
_**∏1 ≤ i ≤ j ≤ n |a1 - aj|**_ sama dengan <br>
_**|a1 - a2| . |a1 - a3| . ... . |a1 - an| . |a2 - a3| . |a2 - a4| . ... . |a2 - an| . ... . |an-1 - an|**_ <br>
Dengan kata lain, ini adalah hasil kali dari |ai - aj| unutk semua 1 ≤ i ≤ j ≤ n <br>

**Input :** <br>
Baris pertama berisi dua bilanngan bulat n,m (2 ≤ n ≤ 2.10^5, 1 ≤ m ≤ 1000) - jumlah bilangan dan nilai modulo.<br>
Baris kedua berisi n bilangan bulat a1, a2, a3, ... , an (0 ≤ ai ≤ 10^9).<br>
<br>
**Output :** <br>
Keluarkan satu bilangan, yaitu hasil dari _∏1 ≤ i ≤ j ≤ n |a1 - aj|_ <br>
<br>
**Contoh :** <br>
Input 1 :<br>
2 10<br>
8 5<br>
Output 1 :<br>
3 <br>
<br>
Input 2 :<br>
3 12<br>
1 4 5<br>
Output 2 :<br> 
0<br>
<br>
Input 3 :<br>
3 7  <br>
1 4 9 <br>
Output 3 :<br>
1<br>
<br>
_**Note :**_ <br>
Contoh 1 : |8-5| = 3 ≡ 3 mod 10<br>
Contoh 2 : |1-4| . |1-5| . |4-5| = 3 . 4 . 1 ≡ 0 mod 12<br>
Contoh 3 : |1-4| . |1-9| . |4-9| = 3 . 9 . 5 ≡ 1 mod 7<br>
<br>

# 🌴 Source Code
Klik [Google Colab](https://colab.research.google.com/drive/10A6OgRu6u7_o8HMK1UzQSR03GuwYoUbW?usp=sharing) untuk menjalankan program ini.
```
def impossible_calculation(n, m, arr):
    # jika n > m, hasil pasti 0 berdasarkan pigeonhole principle
    if n > m:
        print(0)
        return
    
    result = 1
    
    # hitung hasil perkalian semua |a[i] - a[j]|
    for i in range(n):
        for j in range(i + 1, n):
            diff = abs(arr[i] - arr[j])
            result = (result * diff) % m
            # jika hasil sudah 0, langsung output dan hentikan program
            if result == 0:
                print(0)
                return
    
    # output hasil
    print(result)

# mengambil input dan menjalankan fungsi
if __name__ == "__main__":
    n, m = map(int, input().split())
    arr = list(map(int, input().split()))
    impossible_calculation(n, m, arr)
```
# 🌳 Penjelasan
1. **Fungsi impossible_calculation(n, m, arr):**
   Fungsi ini menerima tiga parameter :<br>
   n : jumlah elemen dalam array arr.<br>
   m : sebuah bilangan yang digunakan untuk menghitung hasil modulo.<br>
   arr : array berisi bilangan-bilangan bulat.
2. **Pengecekan Awal :** <br>
   Fungsi memeriksa apakah n lebih besar dari m. Jika n > m, fungsi langsung mencetak 0 dan berhenti.<br>
   Alasan pengecekan ini adalah Prinsip Pigeonhole, yang menyatakan bahwa jika ada lebih banyak elemen dalam arr (yaitu n > m), maka ada jaminan bahwa hasil akhir dari perkalian selisih nilai yang diambil modulo m akan menjadi 0.<br>
3. **Inisialisasi Variabel result :** <br>
   Variabel result diinisialisasi dengan nilai 1. Variabel ini akan digunakan untuk menyimpan hasil perkalian dari semua nilai selisih absolut antar-elemen arr (yakni, | arr[i] - arr[j]| ).
4. **Perhitungan Selisih Absolut Antar-Elemen :** <br>
   Dua loop for bersarang digunakan untuk menghitung selisih absolut antara setiap pasangan elemen dalam arr, yaitu | arr[i] - arr[j] | untuk setiap i < j.<br>
   Selisih absolut tersebut kemudian dikalikan dengan result, dan hasilnya diambil modulo m untuk menjaga hasil tetap dalam rentang angka yang relatif kecil.<br>
   Jika result menjadi 0 selama proses ini, fungsi langsung mencetak 0 dan berhenti, karena hasil akhir perkalian dengan 0 akan tetap 0.
5. **Cetak Hasil Akhir :** <br>
   Jika perhitungan selesai tanpa menemukan result = 0, maka fungsi mencetak nilai akhir dari result.

# 🌻 Hasil
Contoh 1 : <br>
![image](https://github.com/user-attachments/assets/19aee16b-e71d-4fab-baf1-b07e5c1ad141)<br>
Contoh 2 : <br>
![image](https://github.com/user-attachments/assets/5d292208-0f04-4449-b4d9-d3b4d47c8144)<br>
Contoh 3 : <br>
![image](https://github.com/user-attachments/assets/2a574c18-8e76-497b-bb91-63a46ec411e9)<br>

# :bird: Analisis Pigeonhole
1. **Konsep** <br>
   - Jika jumlah elemen n lebih besar dari nilai modulo m, maka setidaknya  ada 2 elemen dalam array yang memiliki nilai yang sama dalam modulo m.
   - Akibatnya, |ai - aj| % m = 0 untuk beberapa pasangan i dan j, yang membuat hasil perkalian menjadi 0.
2. **Implementasi** <br>
   - Jika n > m , program langsung mengeluarkan hasil 0 tanpa melakukan perhitungan lebih lanjut<br>
   ```
   if n > m
        print(0)
        return
   ```
   - Hal ini dapat menghemat waktu karena tidak perlu menghitung semua pasangan |ai - aj|.
3. **Efisiensi** <br
   - Menghindari Komputasi Besar : <br>
     Ketika n > m, menghitung semua pasangan akan memakan waktu O(n^2). Dengan menghentikan program lebih awal, waktu eksekusi dapat menjadi O(1).
4. **Kesimpulan** <br>
   Prinsip pigeonhole dalam program ini digunakan untuk mengeluarkan hasil 0 ketika n > m, menghemat waktu dan meningkatkan efisiensi program.
   




