# Yangi loyiha uchun backend: o'rnatish tartibi

1. **Supabase:** yangi loyiha (har bir sayt uchun alohida, alohida parol).
   Storage -> New bucket -> `media` -> **Public**.
2. **.env:** `.env.example` ni `.env` deb nusxalang va to'ldiring.
   Kalit (`service_role`) 219 belgi, bitta qatorda bo'lishi kerak.
3. **Lokal tekshirish** (Windows'da `python -m` bilan yozing):
   ```
   pip install -r requirements.txt
   python test_storage.py        # HAMMASI ISHLAYAPTI chiqishi kerak
   python create_tables.py       # jadvallarni yaratadi (alembic upgrade head EMAS)
   python create_admin.py        # admin hisob
   python -m uvicorn app.main:app --reload
   ```
   http://localhost:8000/api/health va http://localhost:8000/api/docs
4. **GitHub:** yangi repo, `.env` ni yuklamang.
5. **Render:** `render.yaml` dagi `name` ni o'zgartiring, repoga qo'shing,
   Render -> New -> Blueprint. Til **Python** bo'lishi shart (Go emas).
   So'ralgan o'zgaruvchilarni qo'lda kiriting (`.env` Render'ga o'tmaydi).
6. **Vercel (frontend):** `NEXT_PUBLIC_API_URL=https://<servis>.onrender.com/api/v1`,
   backend `BACKEND_CORS_ORIGINS` ga frontend domenini qo'shing.

Tez-tez uchraydigan xatolar:
- `.env` o'qilmayapti -> fayl nomi `.env.txt` bo'lib qolgan yoki boshqa papkada.
- `Invalid Compact JWS` -> kalit qatorida ortiqcha matn (uzunligi 219 emas).
- `signature verification failed` -> Render'dagi kalit/URL boshqa loyihaniki.
- `uvicorn: command not found` -> Render servisi Python emas, qayta yarating.
