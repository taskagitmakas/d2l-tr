# Kurulum
:label:`chap_installation`

Sizi uygulamalı öğrenme deneyimine hazır hale getirmek ve Python'u,
Jupyter not defterlerini, ilgili kütüphaneleri ve kitabın kendisini çalıştırmaya
gereken kodu koşturmak için bir ortam kurmanıza ihtiyacımız var.


## Miniconda'yı Yükleme

Başlamanın en basit yolu yüklemektir.
[Miniconda] (https://conda.io/en/latest/miniconda.html).
Python 3.x sürümü gereklidir. Conda önceden yüklenmişse, aşağıdaki adımları
atlayabilirsiniz. Sisteminize karşılık gelen Miniconda sh dosyasını web
sitesinden indirin ve ardından yükleme işlemini komut satırından
`sh <FILENAME> -b` komutunu kullanarak yürütün. MacOS kullanıcıları için:

```bash
# The file name is subject to changes
sh Miniconda3-latest-MacOSX-x86_64.sh -b
```


Linux kullanıcıları için:

```bash
# The file name is subject to changes
sh Miniconda3-latest-Linux-x86_64.sh -b
```

Ardından, doğrudan `conda` çalıştırabilmemiz için kabuğu sıfırlayın.
Next, initialize the shell so we can run `conda` directly.

```bash
~/miniconda3/bin/conda init
```

Şimdi mevcut kabuğunuzu kapatıp yeniden açın. Artık aşağıdaki gibi yeni bir
ortam oluşturabilmelisiniz:

```bash
conda create --name d2l -y
```


## D2L Not Defterlerini İndirme

Sonra, bu kitabın kodunu indirmemiz gerekiyor. Kodu indirmek ve açmak için
herhangi bir HTML sayfasının üst kısmındaki "Tüm Not Defterleri" sekmesini
tıklayabilirsiniz. Alternatif olarak, "unzip" varsa
(yoksa "sudo apt install unzip") komutunu çalıştırın:

```bash
mkdir d2l-en && cd d2l-en
curl https://d2l.ai/d2l-en.zip -o d2l-en.zip
unzip d2l-en.zip && rm d2l-en.zip
```

Şimdi `d2l` ortamını etkinleştirmek ve `pip` i kurmak isteyeceğiz.
Bu komutu izleyen sorgular için `y` girin.

```bash
conda activate d2l
conda install python=3.7 pip -y
```


## Çerçeveyi ve `d2l` Paketini Yükleme

:begin_tab:`mxnet,pytorch`
Derin öğrenme çerçevesini kurmadan önce, lütfen önce makinenizde uygun GPU'ların
olup olmadığını kontrol edin (standart bir dizüstü bilgisayarda ekranı
destekleyen GPU'lar bizim amacımıza uygun için sayılmaz). GPU sunucusuna kurulum
yapıyorsanız, GPU destekli bir sürüm kurma talimatları için şu adrese ilerleyin
:ref:`subsec_gpu`.

Aksi takdirde, CPU sürümünü yükleyebilirsiniz.
Bu, ilk birkaç bölümü geçmeniz için yeterli beygir gücü olacak, ancak daha
büyük modelleri çalıştırmadan önce GPU'lara erişmek isteyeceksiniz.
:end_tab:


:begin_tab:`mxnet`

```bash
pip install mxnet==1.6.0
```


:end_tab:

:begin_tab:`pytorch`

```bash
pip install torch==1.5.1 torchvision
```


:end_tab:

:begin_tab:`tensorflow`
TensorFlow'u hem CPU hem de GPU desteğiyle aşağıdakileri kullanarak
yükleyebilirsiniz:

```bash
pip install tensorflow==2.2.0 tensorflow-probability==0.10.0
```


:end_tab:

Ayrıca, bu kitapta sık kullanılan işlevleri ve sınıfları içeren `d2l` paketini
de yüklüyoruz.

```bash
pip install -U d2l
```

Yüklendikten sonra, Jupyter not defterini şu şekilde çalıştırarak açıyoruz:

```bash
jupyter notebook
```

Bu noktada, http://localhost:8888 (genellikle otomatik olarak açılır) adresini
web tarayıcınızda açabilirsiniz. Sonra kitabın her bölümü için kodu çalıştırabiliriz.
Lütfen kitabın kodunu çalıştırmadan veya derin öğrenme çerçevesini veya `d2l`
paketini güncellemeden önce çalışma zamanı ortamını etkinleştirmek için daima
`conda enable d2l` yi yürütün. Ortamdan çıkmak için `conda deactivate` komutunu
çalıştırın.



## GPU Desteği
:label:`subsec_gpu`

:begin_tab:`mxnet, pytorch`
Varsayılan olarak, derin öğrenme çerçevesi, herhangi bir bilgisayarda
(çoğu dizüstü bilgisayar dahil) çalışmasını sağlamak için GPU desteği olmadan
yüklenir.
Bu kitabın bir kısmı GPU ile çalışmayı gerektirir veya önerir.
Bilgisayarınızda NVIDIA grafik kartları varsa ve
[CUDA](https://developer.nvidia.com/cuda-downloads) yüklüyse, GPU-etkin bir
sürüm yüklemeniz gerekir.
Yalnızca CPU sürümünü yüklediyseniz, önce bunu çalıştırarak
kaldırmanız gerekebilir:
:end_tab:

:begin_tab:`tensorflow`
Varsayılan olarak, TensorFlow GPU desteği ile yüklenir.
Bilgisayarınızda NVIDIA grafik kartları varsa ve
[CUDA](https://developer.nvidia.com/cuda-downloads) yüklüyse, tamamen hazırsınız
demektir.
:end_tab:

:begin_tab:`mxnet`

```bash
pip uninstall mxnet
```


:end_tab:

:begin_tab:`pytorch`

```bash
pip uninstall torch
```


:end_tab:

:begin_tab:`mxnet,pytorch`
Sonrasında yüklü CUDA sürümünüzü bulmamız gerekiyor.
`nvcc --version` veya `cat /usr/local/cuda/version.txt` ile kontrol edebilirsiniz.
CUDA 10.1'i yüklediğinizi varsayalım, o zaman aşağıdaki komutla kurabilirsiniz:
:end_tab:

:begin_tab:`mxnet`

```bash
# For Windows users
pip install mxnet-cu101==1.6.0b20190926

# For Linux and macOS users
pip install mxnet-cu101==1.6.0
```


:end_tab:

:begin_tab:`pytorch`

```bash
pip install torch==1.5.1+cu101 -f https://download.pytorch.org/whl/torch_stable.html
```


:end_tab:

:begin_tab:`mxnet,pytorch`
Son rakamları CUDA sürümünüze göre değiştirebilirsiniz; örneğin,
CUDA 10.0 için `cu100` ve CUDA 9.0 için `cu90`.
:end_tab:

## Alıştırmalar

1. Kitabın kodunu indirin ve koşma zamanı ortamını yükleyin.

:begin_tab:`mxnet`
[Tartışmalar](https://discuss.d2l.ai/t/23)
:end_tab:

:begin_tab:`pytorch`
[Tartışmalar](https://discuss.d2l.ai/t/24)
:end_tab:

:begin_tab:`tensorflow`
[Tartışmalar](https://discuss.d2l.ai/t/436)
:end_tab:
