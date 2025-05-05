# 📚Megapik 'Genisleme' Chatbot

🔗 **Repo:** [Megapik-Genisleme](https://github.com/GunalHincal/Megapik-Genisleme)

🚀 **Canlı Demo:** [https://megapikgenislemechatbot-production.up.railway.app/](https://megapik-yeniden-chatbot.onrender.com/) 🔗

Megapik Chatbot, Meltem Hınçal’ın bilim kurgu serisi **Megapik 'Genişleme'** kitabı için özel olarak geliştirilmiş bir **Retrieval-Augmented Generation (RAG)** projesidir. Kitap dünyasını keşfetmek, karakterleri tanımak ve öyküyü derinlemesine anlamak için sorularınızı sorun; chatbot size merak ettiklerinizi içeriği göre cevaplasın. ✨

---

## 📖 İçindekiler

1. [Özellikler](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-%C3%B6zellikler)
2. [Teknolojiler](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-teknolojiler)
3. [Proje Yapısı](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-proje-yap%C4%B1s%C4%B1)
4. [Kurulum &amp; Çalıştırma](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-kurulum--%C3%A7al%C4%B1%C5%9Ft%C4%B1rma)
5. [Kullanım Örneği](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-kullan%C4%B1m-%C3%B6rne%C4%9Fi)
6. [API Endpoint’leri](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-api-endpointleri)
7. [Ortam Değişkenleri](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-ortam-de%C4%9Fi%C5%9Fkenleri)
8. [Katkıda Bulunma](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-katk%C4%B1da-bulunma)
9. [Lisans](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-lisans)
10. [Roadmap](https://chatgpt.com/c/6813c188-e610-8000-829a-bde0d5ccad45#-roadmap)

---

## 🔍 Özellikler

* 🤖 **Embedding**: Kullanıcı sorusu, **Google Gemini Embedding** kullanılarak dönüştürülür.
* 📦  **Depolama** : Oluşan embedding’ler **ChromaDB**’de saklanır ve en alakalı  **chunk** ’lar seçilir.
* 🌐  **RAG** : Seçilen içerik,  **Google Gemini API** ’ye gönderilerek doğal, akıcı yanıtlar üretilir.
* 🎨  **Dinamik Arayüz** : Her mesajdan sonra arka plan görseli otomatik değişir.
* 🛠️  **Test & Dokümantasyon** : Swagger UI ile endpoint’ler interaktif test edilebilir.

---

## 🛠️ Teknolojiler

| Kategori        | Teknoloji / Kütüphane                       |
| --------------- | --------------------------------------------- |
| Backend         | FastAPI, Uvicorn                              |
| Embedding & RAG | HuggingFace Transformers, ChromaDB, LangChain |
| LLM API         | Google Gemini API                             |
| Frontend        | HTML, CSS, JavaScript                         |
| Veri Depolama   | ChromaDB (DuckDB + Parquet)                   |
| Ortam Yönetimi | Python Dotenv, venv                           |

---

## 📂 Proje Yapısı

```
📂 MEGAPIK_GENISLEME/
├── 📂 data/                 # Kitap PDF verisi
│   └── megapik_yeniden.pdf
├── 📂 chroma_db/            # Vektör veritabanı
├── 📂 static/               # CSS, JS ve medya dosyaları
│   ├── 📂 backgrounds/               # Arka plan görselleri (background1.jpeg ... background20.jpeg)
│   ├── megapik_yeniden_cover2*.jpeg   # Kitap kapağı görselleri
│   ├── style.css
│   └── script.js
├── 📂 templates/            # HTML dosyaları
│   └── index.html
├── 📄 main.py               # FastAPI uygulaması
├── 📄 vector_store_api.py   # ChromaDB vektör işlemleri
├── 🔧.env
├── 📄 .gitignore            # Git için gereksiz dosyaları dışarıda tutar
├── 📄 README.md             # Proje dokümantasyonu
├── 📄 requirements.txt      # Gerekli Python kütüphaneleri
```

---

## ⚙️ Kurulum & Çalıştırma

### 1️⃣ Gereksinimler

* Python ≥ 3.9
* Git, curl, ngrok (opsiyonel)

### 2️⃣ Hızlı Başlangıç

```bash
# Depoyu klonlayın
git clone https://github.com/GunalHincal/Megapik-Yeniden.git
cd Megapik-Yeniden

# Sanal ortam oluştur ve aktif et
python -m venv venv
# Windows
.\venv\Scripts\activate
# macOS/Linux
source venv/bin/activate

# Bağımlılıkları yükle
pip install -r requirements.txt

# ChromaDB’yi oluştur (ilk defa)
python vector_store_api.py

# Uygulamayı başlat
uvicorn main:app --reload --port 8001

# Tarayıcıda aç
open http://127.0.0.1:8001
```

---

## 💡 Kullanım Örneği

```bash
curl -X POST http://127.0.0.1:8001/chat \
  -H "Content-Type: application/json" \
  -d '{"history": [], "message": "Kitabın ana teması nedir?"}'
```

---

## 🚏 API Endpoint’leri

| Metot | Yol                     | Açıklama                         |
| ----- | ----------------------- | ---------------------------------- |
| GET   | `/`                   | Arayüzü yükler                  |
| HEAD  | `/`                   | Sağlık kontrolü (UptimeRobot)   |
| GET   | `/vector_store_info`  | Vektör sayısını döner         |
| GET   | `/vector_store_debug` | Debug info                         |
| POST  | `/build_vector_store` | DB oluşturma görevini başlatır |
| POST  | `/chat`               | Soruyu işleyip yanıt üretir     |
| GET   | `/api/backgrounds`    | Arka plan görsellerini listeler   |

Swagger UI: [http://127.0.0.1:8001/docs](http://127.0.0.1:8001/docs)

---

## 🔒 Ortam Değişkenleri

`.env.example` dosyasını kopyala:

```ini
GEMINI_API_KEY=your_gemini_api_key_here
```

---

## 🤝 Katkıda Bulunma

1. Repoyu fork’la
2. Yeni branch aç (`git checkout -b feature/x`)
3. Commit’le (`git commit -m "feat: yeni özellik"`)
4. Push’la (`git push origin feature/x`)
5. Pull request oluştur 🎉

---

## 🛣️ Roadmap

* [ ] Parquet tabanlı embedding indeksi
* [ ] Çoklu dil desteği
* [ ] Mobil tasarım
* [ ] Tema seçimi
* [ ] CI/CD entegrasyonu

---

## 🎯 Sonuç ve Gelecek Çalışmalar

Bu proje, **kitap içeriğine dayalı chatbot geliştirme** sürecini detaylandırarak **bilgiye dayalı yapay zeka asistanlarının nasıl inşa edilebileceğini** gösteren bir çalışma olmuştur. Gelecekte **farklı veri kaynakları** ile genişletilerek akademik ve ticari kullanım alanları artırılabilir.

👩‍💻 **Geliştirici:** Günal Hınçal

📆 **Tarih:** Mayıs 2025

Her türlü geri bildiriminiz için ulaşabilirsiniz. Projeyi beğenip desteklemeyi unutmayın! 😊

**✨ Teşekkürler! 😊**

---


## 🚀 Follow Me for More Updates

Stay connected and follow me for updates on my projects, insights, and tutorials:

* **LinkedIn:** **[Connect with me professionally to learn more about my work and collaborations](https://www.linkedin.com/in/gunalhincal)**
* **Medium:** **[Check out my blog for articles on technology, data science, and more!](https://medium.com/@hincalgunal)**

Feel free to reach out or follow for more updates! 😊 Have Fun!
