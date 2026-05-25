# NoteFlow — Veri Modeli

## IndexedDB Tabloları (Dexie.js)

---

### notes

```typescript
interface Note {
  id: string               // nanoid()
  type: NoteType           // 'text' | 'canvas' | 'voice' | 'image' | 'drawing' | 'presentation' | 'page'
  title: string
  content: NoteContent     // type'a göre değişen içerik (JSON)
  projectId: string | null // null = "Notlarım"
  folderId: string | null
  tags: string[]
  color: string            // hex arka plan rengi
  icon: string             // emoji ikon
  starred: boolean
  archived: boolean
  deleted: boolean
  deletedAt: Date | null
  createdAt: Date
  updatedAt: Date
  wordCount: number        // text notlar için
  duration: number         // ses notlar için (saniye)
  thumbnail: string | null // base64 küçük resim (canvas/image)
}

type NoteType = 'text' | 'canvas' | 'voice' | 'image' | 'drawing' | 'presentation' | 'page'
```

### NoteContent tipleri

```typescript
// Metin notu
interface TextNoteContent {
  html: string             // TipTap HTML çıktısı
  plainText: string        // Arama için
}

// Canvas notu
interface CanvasNoteContent {
  objects: KonvaObject[]   // Konva sahne nesneleri (JSON)
  background: string       // 'blank' | 'dots' | 'grid' | 'lines'
  viewportX: number
  viewportY: number
  zoom: number
}

// Ses notu
interface VoiceNoteContent {
  audioData: string        // base64 WebM/audio
  duration: number         // saniye
  waveformData: number[]   // dalga görselleştirme için amplitüd dizisi
  transcriptText: string   // isteğe bağlı transkript
  textNote: string         // ses yanındaki metin
}

// Görsel notu
interface ImageNoteContent {
  images: {
    id: string
    data: string           // base64
    caption: string
    width: number
    height: number
  }[]
  textNote: string
}

// Sunum
interface PresentationContent {
  slides: Slide[]
  theme: PresentationTheme
}

interface Slide {
  id: string
  elements: SlideElement[]
  background: SlideBackground
  presenterNotes: string
  transition: string
}

// Çok sayfalı doküman
interface PageDocContent {
  pages: {
    id: string
    html: string           // TipTap HTML
    pageSize: 'A4' | 'A3' | 'Letter'
    orientation: 'portrait' | 'landscape'
  }[]
  header: string
  footer: string
}
```

---

### projects

```typescript
interface Project {
  id: string
  name: string
  description: string
  color: string            // hex
  icon: string             // emoji
  coverImage: string | null // base64
  archived: boolean
  createdAt: Date
  updatedAt: Date
  noteCount: number        // cache (performans)
}
```

---

### folders

```typescript
interface Folder {
  id: string
  name: string
  projectId: string | null // null = "Notlarım" altında
  parentId: string | null  // null = root klasör
  color: string
  icon: string
  createdAt: Date
  updatedAt: Date
  order: number            // sıralama
}
```

---

### tags

```typescript
interface Tag {
  id: string
  name: string
  color: string
  noteCount: number        // cache
  createdAt: Date
}
```

---

### noteVersions (versiyon geçmişi)

```typescript
interface NoteVersion {
  id: string
  noteId: string
  content: NoteContent
  savedAt: Date
  label: string | null     // isteğe bağlı kullanıcı etiketi
}
```

---

### settings

```typescript
interface AppSettings {
  id: 'singleton'          // tek kayıt
  theme: 'light' | 'dark' | 'system'
  accentColor: string
  fontSize: 'sm' | 'md' | 'lg'
  fontFamily: string
  sidebarWidth: number
  defaultView: 'list' | 'grid'
  autoSaveDelay: number    // ms, varsayılan 2000
  compactMode: boolean
}
```

---

## Dexie Şema Tanımı

```typescript
class NoteFlowDB extends Dexie {
  notes!: Table<Note>
  projects!: Table<Project>
  folders!: Table<Folder>
  tags!: Table<Tag>
  noteVersions!: Table<NoteVersion>
  settings!: Table<AppSettings>

  constructor() {
    super('NoteFlowDB')
    this.version(1).stores({
      notes: 'id, type, projectId, folderId, starred, archived, deleted, createdAt, updatedAt, *tags',
      projects: 'id, archived, createdAt',
      folders: 'id, projectId, parentId',
      tags: 'id, name',
      noteVersions: 'id, noteId, savedAt',
      settings: 'id',
    })
  }
}
```

---

## Örnek Veri

```json
{
  "note": {
    "id": "abc123",
    "type": "text",
    "title": "Proje Toplantı Notları",
    "content": {
      "html": "<h1>Toplantı</h1><p>Bugün şunları konuştuk...</p>",
      "plainText": "Toplantı\nBugün şunları konuştuk..."
    },
    "projectId": "proj456",
    "folderId": null,
    "tags": ["toplantı", "önemli"],
    "color": "#fef3c7",
    "icon": "📝",
    "starred": true,
    "archived": false,
    "deleted": false,
    "deletedAt": null,
    "createdAt": "2026-05-12T10:00:00Z",
    "updatedAt": "2026-05-12T10:30:00Z",
    "wordCount": 245,
    "duration": 0,
    "thumbnail": null
  }
}
```
