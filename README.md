# P2_Probstat_D_5025201106
Repository untuk pengerjaan Praktikum 2 mata kuliah Probabilitas dan Statistik 2022.


| Nama                      | NRP        |
|---------------------------|------------|
| Ahmad Hafizh Assa'ad      | 5025201106 |

## Soal 1
> Seorang peneliti melakukan penelitian mengenai pengaruh aktivitas 𝐴 terhadap
kadar saturasi oksigen pada manusia. Peneliti tersebut mengambil sampel
sebanyak 9 responden. Pertama, sebelum melakukan aktivitas 𝐴, peneliti mencatat
kadar saturasi oksigen dari 9 responden tersebut. Kemudian, 9 responden tersebut
diminta melakukan aktivitas 𝐴. Setelah 15 menit, peneliti tersebut mencatat kembali
kadar saturasi oksigen dari 9 responden tersebut. Berikut data dari 9 responden
mengenai kadar saturasi oksigen sebelum dan sesudah melakukan aktivitas 𝐴
![image](https://user-images.githubusercontent.com/96507651/170881581-39a25bd3-348f-4461-b55d-578d9cbd28c2.png)

Berdasarkan data pada tabel diatas, diketahui kadar saturasi oksigen dari
responden ke-3 ketika belum melakukan aktivitas 𝐴 sebanyak 67, dan setelah
melakukan aktivitas 𝐴 sebanyak 70.

### 1.a
- Carilah Standar Deviasi dari data selisih pasangan pengamatan tabel
diatas_

- kita akan mengekstrak data dari tabel tersebut dengan fungsi `c()` yang akan melakukan kombinasi menjadi vector pada data tabel kemudian disimpan pada variabel `x` dan `y`

```
x <- c(78,75,67,77,70,72,28,74,77)
y <- c(100,95,70,90,90,90,89,90,100)
```

- Visualisasi variabel `x` dan `y` akan disimpan kedalam `data`, hasilnya adalah sebagai berikut
![image](https://user-images.githubusercontent.com/96507651/170881646-b04d3478-d62f-4fe8-8b3b-18e37df0e0e0.png)

- Kemudian dihitung standar deviasinya denggan fungsi `sd()`

```
cat(sprintf("No 1.a Standar Deviasi data X -> %f", sd(x)))
cat(sprintf("No 1.a Standar Deviasi data X -> %f", sd(y)))
```

![image](https://user-images.githubusercontent.com/96507651/170881670-3c62cedd-302f-48c9-9083-f98fe793b06a.png)
 
 ### 1.b
- carilah nilai t (p-value)

`t-value` merupakan cara untuk mengukur perbedaan antara rata-rata populasi dan `p-value` adalah probabilitas untuk memperoleh `t-value` dengan nilai absolut setidaknya sebesar yang sebenarnya kita amati dalam data sampel jika nol hipotesis sebenarnya benar

disini hipotesa kita adalah `greater`

```
alt <- "greater"
t.test(x, y, alternative = alt, var.equal = FALSE)
```

![image](https://user-images.githubusercontent.com/96507651/170881698-5f881b1c-69c2-4595-8324-20276de24699.png)

 ### 1.c
- tentukanlah apakah terdapat pengaruh yang signifikan secara statistika
dalam hal kadar saturasi oksigen , sebelum dan sesudah melakukan
aktivitas 𝐴 jika diketahui tingkat signifikansi 𝛼 = 5% serta H0 : “tidak ada
pengaruh yang signifikan secara statistika dalam hal kadar saturasi
oksigen , sebelum dan sesudah melakukan aktivitas 𝐴”_

- `tidak ada pengaruh yang signifikan` oleh karena itu, disini kita akan terlebih dahulu membandingkan data pada kolom `x` dan `y` dengan

```
var.test(x, y)
```

![image](https://user-images.githubusercontent.com/96507651/170881759-b718d886-6210-48f0-9be3-c897918547e3.png)

- kemudian diikuti dengan percobaan dengan `t.test()` untuk mengetahui apakah terdapat pengaruh yang signifikan secara statistika dalam hal kadar saturasi oksigen , sebelum dan sesudah melakukan aktivitas 𝐴

```
t.test(x, y, mu = 0, var.equal = TRUE)
```

sebelum :

![image](https://user-images.githubusercontent.com/96507651/170881791-5c2f227d-6142-4507-8477-2bd447a30ae3.png)

setelah :

![image](https://user-images.githubusercontent.com/96507651/170881827-79858db4-d311-4150-aac7-0b99a8784bfe.png)

dapat dilihat bahwa jika dibandingkan dengan nilai sebelumnya, tidak terjadi perbedaan nilai yang signifikan setelah aktivitas 𝐴
  
## Soal 2
> Diketahui bahwa mobil dikemudikan rata-rata lebih dari 20.000 kilometer per tahun.
Untuk menguji klaim ini, 100 pemilik mobil yang dipilih secara acak diminta untuk
mencatat jarak yang mereka tempuh. Jika sampel acak menunjukkan rata-rata
23.500 kilometer dan standar deviasi 3900 kilometer.
 ### 2.a
 - Apakah Anda setuju dengan klaim tersebut?

```
Setuju
```
  
 ### 2.b
 - Jelaskan maksud dari output yang dihasilkan!

```
library(BSDA)
## diketahui
rata_rata <- 23500
standar_deviasi <- 3900
pemilik_mobil <- 100
## hasil
tsum.test(
  mean.x = rata_rata,
  sd(standar_deviasi),
  n.x = pemilik_mobil,
  var.equal = FALSE)
```

![image](https://user-images.githubusercontent.com/96507651/170881877-cbf34283-1543-43f6-b035-f0eafe2461e9.png)

Dari hasil tersebut, maka
Hipotesa nol :

`H0 : μ = 20000`

Hipotesa Alternatif :

`H1 : μ > 20000`
  
 ### 2.c
 - Buatlah kesimpulan berdasarkan P-Value yang dihasilkan!

- Kita pertama akan menghitung nilai dari `p-value` dari data diatas

```
data.mean <- 235000
data.a <- 20000
data.sd <- 3900
data.n <- 100
z <- (data.mean-data.a)/(data.sd/sqrt(data.n))
2*pnorm(-abs(z))
```

![image](https://user-images.githubusercontent.com/96507651/170881902-6cd348c0-f242-4be4-a005-585bf2ad6db4.png)

- dari nilai `p-value = 0` maka diketahui hipotesis nol ditolak dan pengujian kita signifikan secara statistik. Oleh karena itu, dapat kita tarik kesimpulan bahwa

```
Mobil dikemudikan rata-rata lebih dari 20.000 kilometer/tahun
```
  
  
  ## Soal 3
> Diketahui perusahaan memiliki seorang data analyst ingin memecahkan
permasalahan pengambilan keputusan dalam perusahaan tersebut. Selanjutnya
didapatkanlah data berikut dari perusahaan saham tersebut.
![img10](https://user-images.githubusercontent.com/96507651/170881945-5b41d1c8-7084-48cd-af17-224d094141ee.png)

Dari data diatas berilah keputusan serta kesimpulan yang didapatkan dari hasil
diatas. Asumsikan nilai variancenya sama, apakah ada perbedaan pada
rata-ratanya (α= 0.05)? Buatlah :

 ### 3.a
 - H0 dan H1

H0 : (Tidak ada perbedaan antara nilai rata rata Bandung dan nilai rata rata Bali)

H1 : (Terdapat perbedaan antara nilai rata rata Bandung dan nilai rata rata Bali)

```
## diketahui
bandung.n <- 19
bandung.mean <- 3.64
bandung.sd <- 1.67
bali.n <- 27
bali.mean <- 2.79
bali.sd <- 1.32
a <- 0
## hasil
bandung.z <- (bandung.mean-a)/(bandung.sd/sqrt(bandung.n))
bali.z <- (bali.mean-a)/(bali.sd/sqrt(bali.n))
cat(sprintf("No 3.a Nilai H0  -> %f", bandung.z))
cat(sprintf("No 3.a Nilai H1 -> %f", bali.z))
```

dari potongan kode diatas, maka didapatkan nilai `h1` dan `h0` yaitu sebagai berikut

![image](https://user-images.githubusercontent.com/96507651/170881975-954abaaf-cd3c-4964-871e-24b4cb4fe9ae.png)

```
h0 : 9.500834
h1 : 10.982777
```
  
### 3.b
- Hitung Sampel Statistik

```
## diketahui
alt <- "greater"
## hasil
tsum.test(
  mean.x = bandung.mean_,
  s.x = bandung.sd,
  n.x = bandung.n
  mean.y = bali.mean,
  s.y = bali.sd,
  n.y = bali.n
  alternative = alt,
  var.equal = TRUE
)
```

maka hasil dari pengujian kedua data tersebut adalah :
![image](https://user-images.githubusercontent.com/96507651/170882004-80f9fac5-90b0-4511-882d-d644b5703cbf.png)

 
### 3.c
- Lakukan Uji Statistik (df =2)

```
library(mosaic)
## diketahui
df <- 2
## hasil
plotDist(dist = 't', df = df)
```

![image](https://user-images.githubusercontent.com/96507651/170882045-2f62c1a0-526f-4d8c-943e-051e3078459c.png)

### 3.d
- Nilai Kritikal

```
alpha <- 0.05
df <- 2
## hasil
result <- qchisq(p = alpha, df = df, lower.tail = FALSE)
cat(sprintf("No 3.d Nilai Kritikal -> %f", result))
```

![image](https://user-images.githubusercontent.com/96507651/170882062-61a3f607-d3f6-4fc9-be8d-afd665876172.png)
                                                             
### 3.e
- Keputusan

- dapat dilihat dari data perhitungan diatas bahwa

```
nilai kritikal = 5.991465
nilai test statistik = 3.64 + 2.79 = 6.43
6.43 > 5.991465
```

kita akan menolak h0 karena 6.43 > 5.991465

### 3.f
- Kesimpulan

```
Terdapat perbedaan antara nilai rata rata Bandung dan nilai rata rata Bali
```

## Soal 4
> Seorang Peneliti sedang meneliti spesies dari kucing di ITS . Dalam penelitiannya
ia mengumpulkan data tiga spesies kucing yaitu kucing oren, kucing hitam dan
kucing putih dengan panjangnya masing-masing.
Jika :
diketahui dataset https://intip.in/datasetprobstat1
H0 : Tidak ada perbedaan panjang antara ketiga spesies atau rata-rata panjangnya
sama
Maka Kerjakan atau Carilah:
### 4.a
 - Buatlah masing masing jenis spesies menjadi 3 subjek "Grup" (grup 1,grup
2,grup 3). Lalu Gambarkan plot kuantil normal untuk setiap kelompok dan
lihat apakah ada outlier utama dalam homogenitas varians

- Pertama, kita akan melakukan import data yang telah disimpan di _cloud_, kita menggunakan fungsi 1attach()1 untuk mengakses data variabel tanpa memanggil ulang `data_frame`

```
library(ggplot2)
oneWayData  <- read.table(url("https://rstatisticsandresearch.weebly.com/uploads/1/0/2/6/1026585/onewayanova.txt"))
dim(oneWayData)
head(oneWayData)
attach(oneWayData)
```

- Kemudian dilakukan pengelompokan berdasarkan `Group` yang terdiri atas 3 jenis yaitu
  "Kucing Oren","Kucing Hitam","Kucing Putih","Kucing Oren"

```
oneWayData$Length <- as.factor(oneWayData$V2)
oneWayData$Group <- as.factor(oneWayData$V1)
oneWayData$Group = factor(oneWayData$Group,labels = c("Kucing Oren","Kucing Hitam","Kucing Putih","Kucing Oren"))
class(oneWayData$Group)
```

- Pengelompokan data tersebut, kemudian kita simpan dalam 3 variabel berbeda, `grup1`, `grup2`, dan `grup3`,

```
grup1 <- subset(oneWayData, Group == "Kucing Oren")
grup2 <- subset(oneWayData, Group == "Kucing Hitam")
grup3 <- subset(oneWayData, Group == "Kucing Putih")
```

- Terakhir kita melakukan penggambaran plot kuantil normal untuk setiap kelompok

```
ggplot(
  data = grup1,
  aes(sample = Length)
  ) + geom_qq()
ggplot(
  data = grup2,
  aes(sample = Length)
  ) + geom_qq()
ggplot(
  data = grup3,
  aes(sample = Length)
  ) + geom_qq()
```
  
### 4.b
 - carilah atau periksalah Homogeneity of variances nya , Berapa nilai p yang
didapatkan? , Apa hipotesis dan kesimpulan yang dapat diambil ?

```
bartlett.test(oneWayData$Group, oneWayData$Length)
```

dari pengujian diatas, didapatkan

```
bartlett = 0.43292
p-value = 0.8054
```
  
### 4.c
- Untuk uji ANOVA (satu arah), buatlah model linier dengan Panjang versus
Grup dan beri nama model tersebut model 1.

```
qqnorm(grup1$Length)
qqline(grup1$Length)
```

![image](https://user-images.githubusercontent.com/96507651/170882129-80df1400-290f-4af9-acf3-7c9bd3f7daef.png)
 
### 4.d
  - Dari Hasil Poin C, Berapakah nilai-p ? , Apa yang dapat Anda simpulkan
dari H0?

```
p-value = 0.8054
```

maka Probabilitas (p-value) > 0,05 maka h0 diterima

### 4.e
  - Verifikasilah jawaban model 1 dengan Post-hoc test Tukey HSD, dari nilai p
yang didapatkan apakah satu jenis kucing lebih panjang dari yang lain?

```
model <- lm(Length~Group, data = oneWayData)
anova(model)
TukeyHSD(aov(model))
```
  <p align="right">(<a href="#top">back to top</a>)</p>
### 4.f
  _Visualisasikan data dengan ggplot2_

```
ggplot(
  oneWayData,
  aes(x = Group, y = Length)) + geom_boxplot(colour = "black") + scale_x_discrete() + xlab("Species") + ylab("Length")
```

![image](https://user-images.githubusercontent.com/96507651/170882166-a9fa9bba-2dd6-4ba3-8492-2cb29202c5b2.png)

## Soal 5
> Data yang digunakan merupakan hasil eksperimen yang dilakukan untuk
mengetahui pengaruh suhu operasi (100˚C, 125˚C dan 150˚C) dan tiga jenis kaca
pelat muka (A, B dan C) pada keluaran cahaya tabung osiloskop. Percobaan
dilakukan sebanyak 27 kali dan didapat data sebagai berikut: Data Hasil
Eksperimen. Dengan data tersebut
### 5.a
 - Buatlah plot sederhana untuk visualisasi data
- Kita akan melakukan import data `GTL.csv` dari google drive

```
id <- "1aLUOdw_LVJq6VQrQEkuQhZ8FW43FemTJ"
GTLData <- read.csv(sprintf("https://docs.google.com/uc?id=%s&export=download", id))
head(GTLData)
str(GTLData)
```

![image](https://user-images.githubusercontent.com/96507651/170882191-11fe92d0-5598-4f32-83e2-34f15f7f065e.png)

- Kemudian akan dilakukan plot sederhana

```
qplot(
  x = Temp,
  y = Light,
  geom = "point",
  data = GTLData) + facet_grid(.~Glass, labeller = label_both)
```

![image](https://user-images.githubusercontent.com/96507651/170882210-610207fb-539a-4e80-9068-98b4ae13617c.png)
  
### 5.b
 - Lakukan uji ANOVA dua arah

- disini kita akan melakukan klasifikasi dari data yang sudah diimport sebelumnya untuk dilakukan pengujian dua arah

```
GTLData$Glass <- as.factor(GTLData$Glass)
GTLData$Temp_Factor <- as.factor(GTLData$Temp)
str(GTLData)
```

![image](https://user-images.githubusercontent.com/96507651/170882234-de6ef1c1-b308-40b8-bf6a-11d96c75e520.png)

- kemudian dilakukan pengujian denggan `aov`

```
anova <- aov(Light ~ Glass*Temp_Factor, data = GTLData)
summary(anova)
```

![image](https://user-images.githubusercontent.com/96507651/170882248-74e27c20-cf02-4af4-ae03-f8dd7fef9ed1.png)
  
### 5.c
 - Tampilkan tabel dengan mean dan standar deviasi keluaran cahaya untuk
setiap perlakuan (kombinasi kaca pelat muka dan suhu operasi)

```
summary_table <- group_by(GTLData, Glass, Temp)
  %>%
  summarise(
    mean = mean(Light),
    sd = sd(Light))
  %>%
  arrange(desc(mean))
print(summary_table)
```

![image](https://user-images.githubusercontent.com/96507651/170882266-dc2968eb-e042-41c3-abe0-a28b9926d530.png)

### 5.d
  Lakukan uji Tukey

```
anova <- aov(Light ~ Glass*Temp_Factor, data = GTLData)
print(TukeyHSD(anova))
```

![image](https://user-images.githubusercontent.com/96507651/170882294-feba057e-aee2-4924-8498-1d94c95600e1.png)

     
  ### 5.e
  Gunakan compact letter display untuk menunjukkan perbedaan signifikan
antara uji Anova dan uji Tukey

```
anova <- aov(Light ~ Glass*Temp_Factor, data = GTLData)
tukey <- TukeyHSD(anova)
compare_data <- multcompLetters4(anova, tukey)
print(compare_data)
cld <- as.data.frame.list(compare_data$`Glass:Temp_Factor`)
compare_data$Tukey <- cld$Letters
print(compare_data)
```

![image](https://user-images.githubusercontent.com/96507651/170882310-24ca4319-20ee-442d-a2b2-bbd5766fe734.png)
