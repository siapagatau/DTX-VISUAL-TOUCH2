# APK PROJECT CHECKPOINT (Skin Engine)
Status: Stage 05 — kode Skin Engine ditulis dan diintegrasikan; BELUM dikompilasi (sandbox tanpa Android SDK/kotlinc/jaringan).
Detail arsitektur: docs/skin-engine.md. Root CHECKPOINT.md = checkpoint proyek keseluruhan.
Default skin (fallback offline): app/src/main/assets/skins/default/{skin.svg,skin.json} = salinan skins/skin-01 v1.1.
Dependency baru: com.caverock:androidsvg-aar:1.4 (app/build.gradle.kts).
Cek pertama oleh user: build lewat GitHub Actions (.github/workflows/build-apk.yml), salin log error kompilasi ke AI berikutnya bila ada.

Update Stage 08: tambah skin/SkinRepository.kt + integrasi SkinManager (unduh/cache offline), assets/config/skin-repo.json, docs/skin-repo.md. Belum dikompilasi. Lihat root CHECKPOINT.md.

Update Stage 09: validator diperluas + rantai fallback di SkinManager; docs/validation.md. Belum dikompilasi.

Update Stage 10: PROMPT_SKIN.md lengkap di skins-repo/. Tidak ada perubahan kode APK.

Update Stage 11: README + docs dirapikan (architecture, mapping-table, unsupported-elements); default skin tanpa c2pa.

Update Stage 12-13: validasi final (validation/stage12-final.md di arsip proyek). Proyek siap dibuild; lihat root CHECKPOINT.md di arsip.

Update Stage 14: pemilih skin (SkinPickerDialog, menu melayang baris SKIN). Belum dibuild.

Update Stage 15 (Skin v2): renderer ditulis ulang (skala via Canvas, root SVG dinormalisasi), SkinHost ditulis ulang (sentuhan tidak restart, tanpa inset ganda, tanpa menu melayang), NativeFloatingMenu DIHAPUS, 8 tombol skin-01 yang dulu dekoratif jadi kontrol (skin v1.2), FunctionRegistry + dispatcher diperluas, MusicPanelDialog baru. Lihat docs/skin-v2.md. BELUM dikompilasi.

Update Stage 16 (Skin v3): default = UI klasik (bukan skin), dialog buatan dihapus (pakai panel asli APK), layout 2 zona (pad melar, panel skin bisa disembunyikan), tab kanan 3 tombol, skin.json v1.3 (layout). Lihat docs/skin-v3.md. BELUM dikompilasi.

Update Stage 17 (Skin v3.1): latar panel melar + isi seragam (tinggi maks 150dp), render tidak lagi bergantung status panel (bug panel hilang), render bertahap + cache disk, skin.json v1.4. Lihat docs/skin-v3.1.md. BELUM dikompilasi.

Update Stage 18 (Skin v3.2): SELURUH skin di-stretch (satu gambar, tanpa pemisahan zona/latar panel), knob diputar lalu di-stretch, skin.json v1.5. Lihat docs/skin-v3.2.md. BELUM dikompilasi.

Update Skin v3.2.1: pengaturan lebar skin (slider Asli..Penuh di pemilih skin; SkinManager.widthPercent, SkinLayout.widthFraction). Lihat docs/scaling.md. BELUM dikompilasi.

Update Skin v3.2.2: pemilih skin tidak lagi berkedip (daftar awal dari index tersimpan, baris bawaan tidak muncul-lalu-diganti, status dipindah ke bawah, ikon refresh ukuran tetap), isi dialog bisa di-scroll (pesan/slider tidak terpotong); dialog preset/suara online langsung tampil dari cache tanpa spinner sesaat. BELUM dikompilasi.

Update Skin v3.2.3: tombol preset.prev/preset.next (DEC/INC) kini berputar (terakhir -> 1, 1 -> terakhir; versi FREE berputar di preset yang tidak terkunci). BELUM dikompilasi.

Update Skin v3.3 (lampu indikator pad): skin.json bisa punya "indicators" (id, pad, on) -> elemen SVG `led-pad-N-on` (display="none") digambar sebagai state menyala di atas dasar saat pad N dipukul. Dipakai keypad 12 tombol skin DTX-Multi 12 (skin-01/03/04/05/06 v+1). SkinModel.SkinIndicator, SkinParser, SkinRenderer.buildDetails (kunci layer "ind:<id>"), SkinHost (loop frame `lamp`, padam 240 ms, sumber = padFlash sehingga sentuh/MIDI/keyboard sama-sama menyalakan lampu), SkinValidator (peringatan saja), SkinRenderCache RENDER_VERSION 33. Default skin asset = salinan skin-01 v1.6. Lihat docs/skin-indicators.md. BELUM dikompilasi.

Update v1.5 (versionCode 6): tombol sembunyikan menu bawah kini juga ada di UI klasik (tema default). Tab kanan klasik = ClassicToggleTab (atas: panel samping, bawah: strip tombol utama), state classicBarVisible (uiFlag "classic_bar_visible", default tampil, disimpan). Strip bawah klasik tidak lagi ikut tersembunyi saat panel samping disembunyikan; target tutorial LOAD klasik hanya bila strip tampil. BELUM dikompilasi.

Update v1.6 (versionCode 7): VISUAL SENTUHAN global (dialog Tema -> bagian "Visual Sentuhan"). Gambar kustom (PNG transparan didukung) tampil di tiap titik jari: multi touch, ditahan tetap tampil, digeser ikut jari, memudar 220 ms setelah dilepas (tap cepat tampil min 90 ms), ukuran 16-240dp (slider). File baru TouchFx.kt (TouchFxState + TouchFxOverlay). Overlay = View biasa di atas konten (addContentView), input hanya DIBACA di MainActivity.dispatchTouchEvent SETELAH super -> jalur pad/audio tidak berubah & tidak ada delay; tanpa recomposition; frame loop hanya saat ada efek memudar. Catatan: sentuhan di dalam jendela dialog (AlertDialog dll) tidak tertangkap karena dialog = window terpisah. BELUM dikompilasi.

Update v1.6.1 (versionCode 8): Visual Sentuhan -> (1) slider "Kedip" (kecepatan memudar 0-1000 ms, 0 = Instan/langsung hilang saat jari lepas, berlaku live, disimpan; TouchFxState.fadeMs); (2) efek kini juga tampil DI DALAM dialog: TouchFxDialogHook() dipasang di title/content 9 dialog (membungkus Window.Callback dialog = hanya baca event, plus overlay di PopupWindow layar-penuh non-touchable; ketukan di luar window dialog = kedip singkat via ACTION_OUTSIDE). Tap lebih singkat dari 1 frame tetap tergambar 1x. BELUM dikompilasi.
