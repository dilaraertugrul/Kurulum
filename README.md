# Wine Üzerinden Proteus Kurma ve Çalıştırma (MacBook) (Apple Silicon[M1/M2/M3])

Bu rehber, MacBook'ta Wine üzerinden Windows uygulamalarının nasıl kurulabileceğini ve çalıştırılabileceğini gösterir.

## Gereksinimler
- Homebrew (macOS paket yöneticisi)
- Wine
- Windows uygulama dosyası (.exe veya .msi)

---

## 1. Homebrew Kurulumu
Homebrew'ü henüz kurmadıysanız, Terminal'i açın ve aşağıdaki komutu çalıştırarak kurun:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Homebrew'ün kurulu olup olmadigini bilmiyorsaniz aşağıdaki komutun hata verip vermemesinden anlayabilirsiniz:

```bash
brew --version
```

## 2. Wine Kurulumu

### Apple Silicon MacBook'lar İçin (M1/M2/M3)
Apple Silicon cihazlarda, uyumluluk sorunları olabilmektedir. Bu yuzden Rosetta 2 ile Wine'ı kullanmak daha stabil olmasını saglayacaktır.

#### Rosetta 2 ile Wine Kurulumu

1. Terminal'de aşağıdaki komutu çalıştırarak Rosetta 2'yi yükleyin:

   ```bash
   /usr/sbin/softwareupdate --install-rosetta --agree-to-license
   ```
2. Terminal'de aşağıdaki komutu çalıştırarak Wine'i yükleyin.

   ```bash
   arch -x86_64 brew install --cask xquartz
   arch -x86_64 brew install --cask --no-quarantine wine@staging
   ```

## 3. Proteus Kurulumu
   - Proteus kurulum dosyasini rar'dan disari aktarin
   - Aşağıdaki komutu çalıştırarak kurun, (dosya yolunu duzeltmeyi unutmayin)
     ```bash
     arch -x86_64 wine "/Users/dilara/Downloads/Proteus 8.17 SP2 Pro.exe"
     ```
   - Kurulumun baslangicinda Windows'a özel birkaç ek yazilim da kuracak. Gerekli oldukça "Next", "Install", "Agree" butonlarina basarak kurulumu tamamlayin.

## 4. Proteus'u Çalıştırma
- Asagidaki komutu calistirarak Proteus'u acabilirsiniz:
  ```bash
  arch -x86_64 wine "$HOME/.wine/drive_c/Program Files (x86)/Labcenter Electronics/Proteus 8 Professional/BIN/PDS.EXE"
  ```
- Masaüstünde yeni bir dosya olusturup, bu komutu shell script olarak kaydedebiliriz, boylece her seferinde bu uzun komutu yazmak zorunda kalmayiz.
  - Masaustunde "proteus" isimli bir dosya olusturup icerigine sunu koyun ve kaydedip dosyayi kapatin
    ```bash
    #!/bin/bash
    arch -x86_64 wine "$HOME/.wine/drive_c/Program Files (x86)/Labcenter Electronics/Proteus 8 Professional/BIN/PDS.EXE"
    ```
  - Aşağıdaki komutu yazarak bu dosyayı "çalıştırılabilir (executable)" hale getirin
    ```bash
    chmod +x $HOME/Desktop/proteus
    ```
  - Artık uzun komutu yazmadan terminalden uygulamayı çalıştırabilirsiniz
    ```bash
    cd ~/Desktop # Masaüstüne git
    ./proteus    # Çalıştır
    ```
