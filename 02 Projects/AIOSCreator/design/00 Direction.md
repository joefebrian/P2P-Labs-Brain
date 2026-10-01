# CreatorOS — design direction

#idea #project

Bukan Figma-first. Bukan dashboard. Ini **studio malam di LAN**: operator, character, SKU, kamera, take.

Chrome & tokens tetap [[02 Projects/AIOSCreator/Design-lock]]. Folder ini = imajinasi + keputusan per fitur, supaya Grok tidak nge-code dari vibe session.

## Gambar yang kita kejar

Kamu buka Tailscale jam 11 malam. Kiri: Character library, wajah yang sudah kamu kenal. Tengah: canvas atau workspace — **satu shot yang sedang dikerjakan**, bukan 40 panel settings. Kanan: identity lock, plate, job. Generate terasa seperti **take**, bukan “run inference”.

Merek kamera (Leica, iPhone 17 Pro Max) dan framing (3/4, full body) adalah **departemen kamera**. Baju dan SKU adalah **wardrobe**. Character adalah **talent yang sudah di-cast**. Jangan campur tiga itu di satu accordion.

Download adalah satu-satunya momen “keluar studio”. Di dalam app, file boleh masih berjejak AI. Yang kamu simpan ke HP / Drive harus bersih dari label *AI content*.

## Tiga hukum (kalau bentrok, hukum menang)

1. **Talent dulu.** Image 1 = orang yang lagi kamu buka. Wajah, rambut, kulit tidak boleh ikut prompt orang lain. Orang baru hanya lewat Image 2/3/4 atau Generate baru.
2. **Satu pekerjaan per tool.** Generate = photoshoot baru. Edit still = ubah still ini (tempat, orang tambahan, objek). Clone = pose/baju dari look, Muse. Try-on = SKU ke plate. Jangan taruh Complete set di Edit.
3. **3060 jujur.** Lokal untuk identity + edit + draft. Cloud untuk clip yang 3060 tidak sanggup. Jangan janji 4K native. Jangan suruh user pilih Klein ketika yang gagal itu Seedance.

## Suasana UI

- **Workspace character** = meja rias. Preset boleh di Generate. Edit still = kertas kosong + extra stills. Freestyle di situ.
- **AI Studio** = floor. Node = orang, barang, kamera, compose, I2V. Wire = kalimat. Character + SKU ke video = satu clip, bukan dua modal.
- **Present** = clapper. Aspect, Camera, Scene, Light, Style — urutan yang sama dengan prompt. Kalau kamera belum di-wire, tulis `—`, jangan ngarang.
- Warna: navy / purple / lime dari Labs. Merah rose hanya untuk Edit still (zona berbahaya: bisa merusak still). Canvas `#F3F4F8`. Jangan Ant blue.

## Imajinasi 90 hari (bukan backlog dust)

- Character bible yang terasa seperti *contact sheet* majalah, bukan grid file explorer. 3/4 selalu ada kalau headshot + full ada — Complete set tidak boleh “lupa” slot tengah.
- Studio I2V: `@Image1` talent, `@Image2` wardrobe, Seedance reference-to-video. Wan hanya first frame. Grok Video key terpisah dari Grok stills.
- Takes strip = rol film. Download dari situ selalu lewat `?download=1` (strip C2PA + pill AI).
- Satu “look” = framing + camera body + place + light + art, tersusun, bisa di-recall tanpa dump markdown.

## Anti-imajinasi (yang bikin jelek)

- Chip preset di setiap kolom “supaya lengkap”
- Label `Theme` / `Title` / `Subject Description` di Adult
- Pesan error stills (“pakai Klein”) waktu yang gagal itu video
- Pack SKU sebagai first frame I2V
- Design.md satu file untuk seluruh OS

## Cara pakai folder ini

1. Fitur baru yang sentuh >1 permukaan → note dari [[_template]]
2. “Brainstorm ya” → Grok **tidak** code. Opsi dulu. Pilihanmu masuk **Keputusan** di note
3. “Gas” → implement. Sesudah lolos, 3 baris *yang jadi* di note yang sama
4. `/design` hanya kalau arsitektur (engine router, spend, multi-ref I2V spek penuh)

## Links

- [[02 Projects/AIOSCreator]]
- [[02 Projects/AIOSCreator/Design-lock]]
- [[02 Projects/AIOSCreator/Logic-lock]]
- [[02 Projects/AIOSCreator/GROK]]
- Code: `C:\Users\USER\Grok\apps\AIOSCreator`
