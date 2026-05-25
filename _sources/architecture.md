# NoteFlow — Teknik Mimari

## Tech Stack

| Katman | Teknoloji | Neden |
|--------|-----------|-------|
| Framework | React 18 + TypeScript + Vite | Hızlı, tip güvenli, modern |
| Styling | Tailwind CSS + shadcn/ui | Tutarlı UI, kolay özelleştirme |
| Rich Text | TipTap 2 | Tam özellikli, uzantılar, markdown |
| Canvas | Konva.js + React-Konva | 2D canvas, React entegrasyonu |
| Freehand | perfect-freehand | Yumuşak el çizimi |
| Ses | MediaRecorder API (native) | Tarayıcı built-in, hiç bağımlılık yok |
| Storage | Dexie.js (IndexedDB) | Offline, hızlı, async |
| State | Zustand | Hafif, basit, slice pattern |
| Routing | React Router v6 | Standart |
| Drag & Drop | dnd-kit | Erişilebilir, esnek |
| İkonlar | Lucide React | Tutarlı, hafif |
| Animasyon | Framer Motion | Smooth geçişler |
| Tarih | date-fns | Hafif tarih manipülasyonu |
| ID | nanoid | Kısa benzersiz ID |

---

## Klasör Yapısı

```
new_pro/
├── docs/                        # Proje belgeleri
│   ├── FEATURES.md
│   ├── ARCHITECTURE.md
│   └── DATA_MODEL.md
├── src/
│   ├── main.tsx                 # Entry point
│   ├── App.tsx                  # Router & layout
│   ├── index.css                # Tailwind imports
│   │
│   ├── types/                   # TypeScript tip tanımları
│   │   ├── note.ts
│   │   ├── project.ts
│   │   ├── canvas.ts
│   │   └── index.ts
│   │
│   ├── lib/                     # Yardımcı fonksiyonlar
│   │   ├── db/
│   │   │   ├── index.ts         # Dexie DB tanımı
│   │   │   ├── notes.ts         # Not CRUD
│   │   │   ├── projects.ts      # Proje CRUD
│   │   │   └── folders.ts       # Klasör CRUD
│   │   ├── utils.ts             # Genel yardımcılar
│   │   └── keyboard.ts          # Kısayol yönetimi
│   │
│   ├── store/                   # Zustand store'lar
│   │   ├── useAppStore.ts       # Global UI state
│   │   ├── useNotesStore.ts     # Not state
│   │   ├── useProjectsStore.ts  # Proje state
│   │   └── useCanvasStore.ts    # Canvas araç state
│   │
│   ├── hooks/                   # Özel hook'lar
│   │   ├── useNotes.ts          # Not CRUD hook'ları
│   │   ├── useProjects.ts       # Proje CRUD hook'ları
│   │   ├── useVoiceRecorder.ts  # Ses kayıt hook'u
│   │   ├── useCanvas.ts         # Canvas hook'u
│   │   └── useSearch.ts         # Arama hook'u
│   │
│   ├── components/
│   │   ├── layout/
│   │   │   ├── AppLayout.tsx        # Ana düzen (sidebar + içerik)
│   │   │   ├── Sidebar.tsx          # Sol kenar çubuğu
│   │   │   ├── SidebarNav.tsx       # Navigasyon linkleri
│   │   │   ├── SidebarProjects.tsx  # Proje listesi
│   │   │   ├── SidebarFolders.tsx   # Klasör ağacı
│   │   │   └── Header.tsx           # Üst bar (arama, ayarlar)
│   │   │
│   │   ├── notes/
│   │   │   ├── NoteCard.tsx         # Not kartı (grid/liste görünümü)
│   │   │   ├── NoteList.tsx         # Not listesi
│   │   │   ├── NoteGrid.tsx         # Not ızgarası
│   │   │   ├── NoteEditor.tsx       # Genel not editör wrapper
│   │   │   ├── TextNoteEditor.tsx   # TipTap zengin metin editörü
│   │   │   ├── NoteToolbar.tsx      # Editör araç çubuğu
│   │   │   └── NoteHeader.tsx       # Not başlığı & meta
│   │   │
│   │   ├── canvas/
│   │   │   ├── InfiniteCanvas.tsx   # Ana canvas bileşeni
│   │   │   ├── CanvasToolbar.tsx    # Araç seçici (kalem, şekil vs.)
│   │   │   ├── CanvasColorPicker.tsx
│   │   │   ├── CanvasMinimap.tsx    # Mini harita
│   │   │   ├── CanvasZoomControl.tsx
│   │   │   ├── tools/
│   │   │   │   ├── PenTool.tsx
│   │   │   │   ├── ShapeTool.tsx
│   │   │   │   ├── SelectTool.tsx
│   │   │   │   ├── EraserTool.tsx
│   │   │   │   └── TextTool.tsx
│   │   │   └── shapes/
│   │   │       ├── DrawingShape.tsx  # Serbest çizim
│   │   │       ├── RectShape.tsx
│   │   │       ├── CircleShape.tsx
│   │   │       ├── ArrowShape.tsx
│   │   │       └── StickyNote.tsx
│   │   │
│   │   ├── voice/
│   │   │   ├── VoiceRecorder.tsx    # Kayıt arayüzü
│   │   │   ├── VoicePlayer.tsx      # Oynatıcı
│   │   │   ├── Waveform.tsx         # Dalga görselleştirme
│   │   │   └── RecordButton.tsx
│   │   │
│   │   ├── presentation/
│   │   │   ├── PresentationEditor.tsx
│   │   │   ├── SlideList.tsx        # Sol panel slayt listesi
│   │   │   ├── SlideEditor.tsx      # Slayt düzenleme alanı
│   │   │   ├── SlideViewer.tsx      # Sunum modu
│   │   │   └── SlideToolbar.tsx
│   │   │
│   │   ├── projects/
│   │   │   ├── ProjectCard.tsx
│   │   │   ├── ProjectGrid.tsx
│   │   │   ├── ProjectHeader.tsx
│   │   │   ├── NewProjectModal.tsx
│   │   │   └── ProjectViewSwitcher.tsx  # Liste/ızgara/kanban
│   │   │
│   │   └── ui/                    # shadcn/ui bileşenleri + özel
│   │       ├── Button.tsx
│   │       ├── Input.tsx
│   │       ├── Modal.tsx
│   │       ├── Dropdown.tsx
│   │       ├── Tooltip.tsx
│   │       ├── Badge.tsx
│   │       ├── ColorPicker.tsx
│   │       ├── EmojiPicker.tsx
│   │       ├── CommandPalette.tsx   # Ctrl+K hızlı arama
│   │       ├── ContextMenu.tsx
│   │       └── Toast.tsx
│   │
│   └── pages/
│       ├── HomePage.tsx             # Dashboard / ana sayfa
│       ├── AllNotesPage.tsx         # Tüm notlar
│       ├── StarredPage.tsx          # Yıldızlı notlar
│       ├── RecentPage.tsx           # Son notlar
│       ├── TrashPage.tsx            # Çöp kutusu
│       ├── SearchPage.tsx           # Arama sonuçları
│       ├── SettingsPage.tsx         # Ayarlar
│       ├── ProjectsPage.tsx         # Projeler listesi
│       ├── ProjectDetailPage.tsx    # Proje içi
│       └── NoteDetailPage.tsx       # Not detay/editör
│
├── public/
│   ├── favicon.svg
│   └── manifest.json              # PWA manifest
├── index.html
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## State Mimarisi

### Zustand Stores

```
useAppStore
├── theme: 'light' | 'dark' | 'system'
├── accentColor: string
├── sidebarOpen: boolean
├── sidebarWidth: number
├── currentView: 'list' | 'grid' | 'kanban'
├── commandPaletteOpen: boolean
└── activeModal: string | null

useNotesStore
├── notes: Note[]
├── activeNoteId: string | null
├── searchQuery: string
├── filters: FilterState
├── selectedNotes: string[]
└── actions: CRUD + filter + search

useProjectsStore
├── projects: Project[]
├── activeProjectId: string | null
├── folders: Folder[]
└── actions: CRUD

useCanvasStore
├── activeTool: CanvasTool
├── strokeColor: string
├── fillColor: string
├── strokeWidth: number
├── zoom: number
├── panOffset: { x, y }
└── history: CanvasAction[]
```

---

## Veri Akışı

```
Kullanıcı Eylemi
     │
     ▼
React Component
     │
     ▼
Zustand Store Action
     │
     ├─► UI State güncelle (anında)
     │
     └─► Dexie.js (IndexedDB)
              │
              └─► Persist (async, arka planda)
```

---

## Routing

```
/                          → HomePage (Dashboard)
/notes                     → AllNotesPage
/notes/:id                 → NoteDetailPage
/notes/new/:type           → Yeni not (type: text|canvas|voice|image|drawing)
/starred                   → StarredPage
/recent                    → RecentPage
/trash                     → TrashPage
/search                    → SearchPage
/projects                  → ProjectsPage
/projects/:id              → ProjectDetailPage
/projects/:id/notes/:noteId → Proje içi not detay
/settings                  → SettingsPage
```

---

## Performans Stratejileri

- Canvas: requestAnimationFrame tabanlı render
- Büyük not listeleri: virtual scroll (react-virtual)
- Resimler: lazy loading + thumbnail önbelleği
- Arama: debounce (300ms) + IndexedDB full-text index
- Otomatik kayıt: debounce (2000ms)
- Canvas nesneleri: kademeli render (görünür alan)
