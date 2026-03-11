# Personal Website Architecture

## Stack

| Layer      | Choice                      |
| ---------- | --------------------------- |
| Framework  | Next.js (App Router)        |
| Hosting    | Vercel                      |
| Source     | GitHub                      |
| Styling    | Tailwind CSS + shadcn/ui    |
| Content    | MDX                         |
| Images     | next/image + `/public`      |
| Language   | TypeScript                  |
| Linting    | ESLint + Prettier           |

---

## Storage Split

| Asset Type                        | Stored In                   | Why                                          |
| --------------------------------- | --------------------------- | -------------------------------------------- |
| Photos, video, audio, art files   | S3 / Vercel Blob / R2       | Binary files, too large for GitHub           |
| Metadata (titles, URLs, tags)     | GitHub (`content/data/`)    | Text, version controlled, easy to edit       |
| Short stories                     | GitHub (`content/stories/`) | Plain text, MDX pipeline works perfectly     |
| About me                          | GitHub (`Md.tsx`)           | Single static section, no pipeline needed    |
| OG image                          | GitHub (`public/`)          | Small static asset, fine in repo             |

---

## Repo Structure

```
my-site/
├── public/
│   └── og-image.png
│
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   └── page.tsx                    # home page, all sections assembled
│   │
│   ├── components/
│   │   ├── sections/
│   │   │   ├── Py.tsx                  # coding projects
│   │   │   ├── Wav.tsx                 # music
│   │   │   ├── Mov.tsx                 # videos
│   │   │   ├── Jpeg.tsx                # photography
│   │   │   ├── Svg.tsx                 # art
│   │   │   ├── Doc.tsx                 # short stories (renders MDX)
│   │   │   └── Md.tsx                  # about me (static, written directly)
│   │   ├── ui/                         # shadcn/ui components
│   │   └── layout/
│   │       └── Nav.tsx                 # .py .wav .mov .jpeg .svg .doc .md
│   │
│   ├── content/
│   │   ├── stories/                    # .mdx files, stored in GitHub (text only)
│   │   │   └── my-first-story.mdx
│   │   └── data/                       # metadata only, S3 URLs as strings
│   │       ├── projects.ts             # coding projects
│   │       ├── music.ts                # links to .wav files in S3
│   │       ├── videos.ts               # links to .mov files in S3
│   │       ├── photography.ts          # links to .jpeg files in S3
│   │       └── art.ts                  # links to .svg/.png files in S3
│   │
│   └── lib/
│       └── mdx.ts                      # MDX parsing helpers
│
├── next.config.ts
├── tailwind.config.ts
└── tsconfig.json
```

---

## Color Palette

### Backgrounds

| Color Name    | Hex       | Usage                           |
| ------------- | --------- | ------------------------------- |
| White         | `#FFFFFF` | Main website background         |
| Soft Off White | `#FDF5F1` | Cards or subtle section backgrounds |

### Brand Accents

| Color Name     | Hex       | Usage                        |
| -------------- | --------- | ---------------------------- |
| Primary Orange | `#F1A45A` | Buttons, links, highlights   |
| Warm Orange    | `#F2AC6B` | Supporting orange tone       |
| Peach          | `#F4BD97` | Soft highlights              |
| Accent Purple  | `#D6A4D8` | Icons, secondary accents     |

### Gradient Palette

| Gradient Name    | Colors                    | Direction    | Usage                        |
| ---------------- | ------------------------- | ------------ | ---------------------------- |
| Primary          | Orange → Purple           | Left → Right | Main CTAs, hero elements     |
| Accent           | Lavender → Periwinkle     | Left → Right | Secondary highlights         |
| Heading          | Orange → Violet           | Left → Right | Section titles, display text |

Individual gradient stops available: Lavender `#C39BF8`, Soft Violet `#AD98F6`, Periwinkle Blue `#9BABF4`

### Text

| Color Name    | Hex       | Usage               |
| ------------- | --------- | ------------------- |
| Primary Black | `#111111` | Main body text      |
| Dark Grey     | `#3A3A3A` | Secondary text      |

### UI Neutrals

| Color Name  | Hex       | Usage                   |
| ----------- | --------- | ----------------------- |
| Light Grey  | `#CFCFCF` | Borders and separators  |
