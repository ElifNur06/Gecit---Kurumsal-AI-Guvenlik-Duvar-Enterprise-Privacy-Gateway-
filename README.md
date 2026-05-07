# 🛡️ Geçit - Kurumsal AI Güvenlik Duvarı (Enterprise Privacy Gateway)

Geçit, kurumsal firmaların hassas verilerini (PII - Kişisel Tanımlanabilir Bilgiler) genel yapay zeka modellerine (Gemini, ChatGPT vb.) sızdırmadan LLM entegrasyonu yapabilmelerini sağlayan **çift yönlü bir güvenlik katmanıdır (De-anonymization Gateway).**

Yapay zeka modellerine giden veriyi maskeler, LLM'in maskeli cevaplarını yakalar ve son kullanıcıya orijinal verilerle restore edilmiş kusursuz bir metin sunar.

![Geçit Banner](https://via.placeholder.com/1000x300.png?text=Ge%C3%A7it+-+Enterprise+AI+Privacy+Gateway) *(Buraya kendi aldığın arayüz ekran görüntüsünü ekleyebilirsin)*

## ✨ Temel Özellikler

* **🔄 Çift Yönlü Restorasyon (De-anonymization):** Veriler (İsim, TC, IBAN, Kredi Kartı, Telefon) LLM'e gitmeden önce `[TC_NO_1]`, `[KİŞİ_ADI_1]` gibi etiketlerle maskelenir. LLM'den cevap döndüğünde, proxy bu etiketleri anlık bellekteki orijinal verilerle tekrar değiştirir.
* **📄 PDF Sanitization (Doküman Analizi):** Sisteme yüklenen kurumsal PDF belgelerindeki bozuk satırları ve görünmez karakterleri temizleyerek metni düzleştirir, ardından maskeleme işlemine sokar.
* **🧠 LLM Router (Çoklu Model):** Promptları içeriğine ve kullanıcı seçimine göre Google Gemini 2.5 Flash veya OpenAI GPT-4o modellerine yönlendirir.
* **📊 MongoDB Denetim Logları (Audit):** Hangi veriden kaç adet maskelendiği, API kullanım istatistikleri ve logları MongoDB üzerinde tutulur (Kişisel verilerin *kendisi* asla veritabanına kaydedilmez).
* **🇹🇷 Yerel Dil Desteği:** Türkçe spesifik kelimelerin (Örn: Özgeçmiş, iletişim) İngilizce NLP modelleri tarafından yanlışlıkla maskelenmesini önleyen özel filtreleme sistemi.

## 🏗️ Sistem Mimarisi

1. **Kullanıcı Girişi:** Kullanıcı metin veya PDF girer.
2. **Geçit Katmanı (Presidio NLP + Regex):** FastAPI arka ucu metni tarar, PII verilerini tespit eder ve geçici bir Hash/Sözlük (Mapping) oluşturur.
3. **LLM İletişimi:** İzole edilmiş, maskeli metin LLM'e (Gemini/OpenAI) "Sistem Komutları" ile birlikte gönderilir.
4. **Restorasyon:** LLM'den dönen maskeli cevap, Geçit proxy'sinde orijinal verilerle tekrar birleştirilir.
5. **Kullanıcı Çıktısı:** Kullanıcı, yapay zekanın orijinal verileri kullanarak yazdığını sandığı, son derece doğal bir cevap alır.

## Görseller
<img width="958" height="536" alt="image" src="https://github.com/user-attachments/assets/66e6a979-9477-4c40-a62b-f85cb862f82e" />
<img width="960" height="542" alt="image" src="https://github.com/user-attachments/assets/e3ae00c1-268c-4a91-8ec3-2033f381beb3" />
<img width="959" height="541" alt="image" src="https://github.com/user-attachments/assets/5a462066-97a2-442f-8ff0-a684b6415703" />
<img width="960" height="541" alt="image" src="https://github.com/user-attachments/assets/eff69631-0b46-4ea9-a935-9f8a3ea4eb37" />
<img width="963" height="544" alt="image" src="https://github.com/user-attachments/assets/06b3fb5d-1822-4111-90fc-715fcd97d435" />

## 🛠️ Kullanılan Teknolojiler
Backend: FastAPI, Python, Uvicorn

Frontend: Streamlit

Veritabanı: MongoDB, Motor (Async)

NLP & Maskeleme: Microsoft Presidio, Spacy, Regular Expressions (Regex)

LLM Entegrasyonu: Google Gemini API, OpenAI API

Doküman İşleme: PyPDF2

Geliştirici: Elif Nur Ayhan
