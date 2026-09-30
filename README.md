# Gündəlik plan — Notion embed vidceti

Tək faylda (`index.html`) işləyən gündəlik iş paneli: bu günün irəliləyişi, geri sayım,
gün-gün qrafik, gecikən işlər, təxirə salma, tarix/saat seçimi. Xarici kitabxana yoxdur.

## Notion-a necə qoyulur

1. `notion-plan/` qovluğunu (index.html + .htaccess) hostinqə yükləyin, məs.
   `public_html/notion-plan/` → ünvan: `https://aimedia.az/notion-plan/`
2. Yoxlayın ki, cavabda `X-Frame-Options` YOXDUR (əks halda Notion boş göstərəcək):
   `curl -sI https://aimedia.az/notion-plan/ | grep -i frame`
3. Notion səhifəsində `/embed` yazın → ünvanı yapışdırın → **Embed link**.
4. Embed-in hündürlüyünü aşağı kənarından dartıb ~650–700 px edin
   (≥ 640 px enində iki sütun, dar olanda tək sütun olur).

Tema: `?theme=dark` və ya `?theme=light` parametri ilə (məs.
`https://aimedia.az/notion-plan/?theme=dark`), ya da vidcetin sağ-üst `⋯` menyusundan.
Notion-un tünd rejimi sistem rejimindən fərqli ola bilər — o halda menyudan seçin.

## Məlumat harada saxlanılır

Brauzerin `localStorage`-ında (açar `gp_tasks_v1`). Yəni hər cihaz/brauzer öz siyahısını
saxlayır, sinxronizasiya yoxdur. Yedək: `⋯` → **Yedək çıxar (JSON)** / **Yedəkdən bərpa et**.

## Qaydalar (kodda belədir)

- **Gecikən** = tarixi keçmiş edilməmiş iş, ya da bu gün saatı keçmiş iş → siyahının
  başında qırmızı. Köhnə edilmişlər bu günün siyahısında görünmür.
- **Təxirə** = tarix (və ya eyni gündə saat) irəli çəkiləndə `moves`-a yazılır → nişan
  «N× təxirə salınıb · əvvəl <ilk tarix>». İlk tarixə (və ya ondan əvvələ) qaytarsan nişan silinir.
- **Edilib** işin *edildiyi günə* yazılır (gecikmiş iş bu gün edilsə, bu günə sayılır);
  edilməmiş iş öz planlanan gününə sayılır. Qrafik/cədvəl bu qaydaya görədir.
- Başlıqda `15:30 Görüş` və ya `Görüş 15:30` yazsan saat avtomatik ayrılır.
