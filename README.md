# Toadformatter

A clean, compact formatter for AIOStreams. See the title, video quality, original-language and English audio, and source at a glance.

Uses probed-track features documented for **AIOStreams v2.35**. Your version needs to support the variables and modifiers in the [current formatter reference](https://docs.aiostreams.viren070.me/reference/custom-formatter/).

## The layout

Title first, details underneath. For shows, season and episode follow the resolution.

[Download formatter JSON](https://raw.githubusercontent.com/thetoadsage/toadformatter/main/formatter.json)

```text
🎬 Example Show (2026)
🔥4K UHD 🍂 S02 · E03 🎚️ Web T1
🎥 WEB-DL 📺 DV · HDR10+ 🎞️ HEVC
🎧 JA TrueHD 7.1 · EN TrueHD 5.1
💬 EN Subs · Forced
📦 20 GiB 📊 25 Mbps
🏷️ GROUP 🎭 Prime Video
⚡ (AIO) 🔍Example addon
```

This is a sample preview. Available details, spacing, and wrapping depend on the release and your player, which may add its own size line.

## How to use

1. In AIOStreams, open **Formatter** and select **Custom**.
2. Click **Import → Import from URL**, then paste:

   ```text
   https://raw.githubusercontent.com/thetoadsage/toadformatter/main/formatter.json
   ```

3. Preview it, then save your configuration.

You can also download the JSON and import the file. Use the formatter's Import button; this is a formatter definition, not a full configuration template.

To update, import it again. An already-imported copy won't pick up repository changes automatically.

## Reading the details

| Symbol | Meaning |
| --- | --- |
| 🎬 | Movie or show title and year |
| 🔥 / ✨ / 🚀 / 💿 | 4K UHD / QHD / FHD / HD |
| 💩 | Low or unknown resolution |
| 🍂 | Season and episode |
| 🎚️ | Release ranking or SeaDex Best/Alternative |
| 🎥 | Release quality, such as WEB-DL or BluRay REMUX |
| 📺 | Video format, such as DV or HDR10+ |
| 🎞️ | Video codec; also used for edition labels on the release row |
| 🎧 | Audio format and channels when available |
| 🌐 | Language hints when detailed audio tracks are unavailable |
| 💬 | English subtitles for a known non-English original |
| 📦 / 📊 | File or folder size / average overall bitrate |
| 🌱 / 📅 | Seeders / Usenet release age |
| 🏷️ / 🎭 | Release group / streaming service or network |
| ⚡ / ⏳ | Cached / uncached |
| 📌 | In your library |
| 🔒 / 🔑 | Proxied / private stream |
| 🔍 | Source addon |
| ℹ️ | Additional status message |

- **EN, JA, etc.** are language codes. Detailed audio shows at most one original-language track and one English track. English originals appear once.
- **T1, T2, etc.** come from your AIOStreams ranking rules.
- **EN Subs**, **Forced**, and **SDH/CC** describe reported English subtitle availability. This row is hidden for English originals and when the original language is unknown.
- Sizes use binary units, such as **GiB**. When folder size is available, it follows the file size: `📦 6.95 GiB / 211 GiB`.
- Missing optional details are left out. A missing subtitle row doesn't necessarily mean there are no subtitles.

Moon scores, container labels, chapters, and runtime are omitted to keep cards concise. Library and uncached status appear once on the service/addon row.

<details>
<summary>More about titles, audio, and status handling</summary>

Titles and years prefer the requested movie/show's catalog metadata, falling back to filename-derived values. Punctuation and capitalization are preserved. Titles are limited to 45 characters; a matching year already at the end of the displayed title is not repeated.

Audio selection prefers an eligible default track, then the first matching track in source order. This is not a quality ranking. Commentary and audio-description tracks are excluded using flags and specific track-title phrases. Explicit original-track flags resolve ties after default-track preference.

Original audio is identified using original-language metadata or an explicit original-track flag. If both are missing, the formatter does not guess. When detailed tracks are unavailable, a short aggregate audio/language summary is used. Filename-derived language hints can include subtitle-only languages.

Stream-wide Atmos/DTS:X badges are omitted from detailed track summaries because they cannot identify which displayed track carries the feature. Other mixes and codecs are intentionally omitted without an ellipsis.

SDH/CC detection recognizes flags, SDH and Closed Caption title phrases, and exact CC titles. Empty optional rows are removed. Other status messages, including Download messages, are preserved.

</details>

## Files and verification

- [`formatter.json`](formatter.json): importable name and description templates.
- [`description.txt`](description.txt): description template for manual paste.

Both templates passed the upstream formatter validator. Regression checks cover title/year fallback, season/episode placement, audio selection and large track lists, subtitle labels, empty rows, and status messages. Preview on your installed AIOStreams version before saving.

## Credits

Built for [AIOStreams](https://docs.aiostreams.viren070.me/). README structure and presentation adapted from [Jeor's formatter](https://github.com/Jeor/formatter), with permission.

Formatter behavior follows the [official custom formatter reference](https://docs.aiostreams.viren070.me/reference/custom-formatter/). Import instructions follow AIOStreams' [formatter selection](https://github.com/Viren070/AIOStreams/blob/main/packages/frontend/src/components/menu/formatter/formatter-selection.tsx) and [URL import](https://github.com/Viren070/AIOStreams/blob/main/packages/frontend/src/components/shared/import-modal.tsx) implementations.
