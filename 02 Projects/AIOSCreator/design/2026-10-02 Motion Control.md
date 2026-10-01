# Motion Control

#decision

Status: 🟢 knowledge · 2026-10-02

Sumber: [Kling Motion Control user guide](https://kling.ai/quickstart/motion-control-user-guide). Ini aturan untuk halaman kita `/create/motion`, bukan salinan halaman Kling.

## Apa halaman ini

MotionControl menempelkan gerak dari **drive clip** ke **character still**. Muka, badan, dan baju datang dari still. Drive clip hanya gerakannya.

Still → video tanpa drive clip tetap di AI Studio (`/create/studio`). Orang dikunci dulu di Characters (`/create/characters`).

Picker di halaman ini: **Kling Motion Control 2.6**, **Kling Motion Control 3.0**, **DreamActor V2**. DreamActor bukan bagian panduan Kling. Muka fotorealnya lebih lemah. Untuk orang katalog, pakai Kling 3.0.

## Nama di layar kita

| Panduan Kling | Layar kita |
| --- | --- |
| Character image | **1 · Character Lock** |
| Action video / motion reference | **2 · Motion reference** (drive clip) |
| Character Orientation Matches Image | **Still orientation**. Drive clip max 10 detik. |
| Character Orientation Matches Video | **Drive orientation**. Drive clip max 30 detik. |
| Prompt untuk latar dan detail lain | **Notes** |
| Audio dari video acuan | **Keep audio from the drive clip** |
| Motion Library | **Use a clip** |

Default di situs Kling adalah orientation mengikuti video. Default kita adalah **Still orientation**.

## Kling 2.6 dan 3.0

2.6 meniru gerak badan, tangan, dan one-shot sampai 30 detik. 3.0 menambah muka yang lebih stabil di sudut sulit, emosi, muka yang tertutup, dan framing yang bergerak.

Cara pakai 2.6 di Kling: video gerak, lalu foto karakter dengan proporsi yang sama, lalu pilih orientation, lalu prompt.

3.0 menambah **Bind Facial Element**. Element itu hanya data muka (bukan baju, rambut, makeup, atau prop). Binding hanya jalan kalau orientation karakter sama dengan orientation video. Kita **belum** mengirim element binding. Yang terkirim: still, drive clip, prompt, `character_orientation`, 1080p, dan audio original atau off.

## Supaya hasilnya tidak rusak

- Samakan framing. Half-body dengan half-body. Full-body dengan full-body. Kepala dan badan kelihatan, tidak tertutup.
- Gerak lebar, kecepatan sedang, perpindahan kecil. Gerak besar butuh ruang kosong di still.
- Satu orang. Kalau ada dua, Kling memakai yang paling besar di frame. Di 3.0, kalau ukurannya mirip, element bisa tidak terpilih.
- Orang sungguhan paling aman. Beberapa proporsi humanoid tetap dikenali.
- Satu take terus. Jangan ada cut, pindah shot, atau gerak kamera di drive clip, atau hasilnya bisa terpotong.
- Jangan terlalu cepat. Gerak rumit atau cepat bisa kembali lebih pendek dari upload. Minimal gerak kontinu yang kepakai 3 detik. Kredit Kling untuk kasus ini tidak di-refund.
- Sisi pendek minimal 340px. Sisi panjang maksimal 3850px. Durasi upload 3–30 detik. Panjang output mengikuti drive clip.
- Untuk putar kepala: depan plus samping. Untuk ekspresi: depan netral plus ekspresi yang diinginkan. Emosi rumit lebih aman dari video muka, bukan satu foto.

## Batas yang kode kita sudah jaga

- Drive di bawah 2.8 detik ditolak. Kling minta minimal 3 detik.
- Still orientation di atas 10.05 detik otomatis pindah ke drive orientation.
- Di luar 340–3850px, drive di-scale dulu.
- Still maksimal 50MB. Drive maksimal 100MB. Output Kling 1080p.

## Harga di panduan Kling

Durasi dibulatkan ke detik terdekat. Kita tidak punya tombol Standard / Professional di halaman.

| Model | Standard | Professional |
| --- | --- | --- |
| 2.6 | 5 kredit/detik | 8 kredit/detik |
| 3.0 | 9 kredit/detik | 12 kredit/detik |

Contoh mereka: 3.4 detik dihitung 3 detik, 3.6 detik dihitung 4 detik.

## Belum di halaman kita

- Element binding 3.0 (set foto atau video muka).
- Pilih Standard vs Professional.
- Default orientation kita masih still, bukan default Kling yang mengikuti video.

## Links

- [[02 Projects/AIOSCreator]]
- [[02 Projects/AIOSCreator/design/00 Direction]]
