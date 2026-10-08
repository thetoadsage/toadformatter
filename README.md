# Toadformatter

A compact custom formatter for AIOStreams, with original-language and English audio summaries.

## Import from GitHub

In AIOStreams, open **Formatter**, select **Custom**, click **Import**, then **Import from URL**. Paste:

```text
https://raw.githubusercontent.com/thetoadsage/toadformatter/main/formatter.json
```

Check the preview, then save your configuration. Import this file through the formatter's Import button. It is a formatter definition, not a full configuration template.

To pick up later changes, import the same URL again.

## What it shows

- Resolution and score in the stream name.
- Title, year, release quality, video format and container.
- One original-language audio track and one English audio track, with codec and channels when available.
- English subtitle availability, forced subtitles, and SDH/CC when known.
- Size, bitrate, release group, service/addon, and relevant release/status information.

Example audio summary:

```text
🎧 JA TrueHD 7.1 · EN TrueHD 5.1
```

Audio entries use the first matching track in source order, not a quality ranking. Commentary tracks are excluded. English originals appear once. Other mixes and codecs are intentionally omitted, without an ellipsis.

Original audio is identified using the title's original-language metadata or an explicit original-track flag. If both are missing, the formatter does not guess. When track details are absent, a short aggregate audio/language summary is used instead. Filename-derived language hints can include subtitle-only languages.

Chapters and runtime are omitted to keep stream cards concise. Stream-wide Atmos/DTS:X badges are omitted from detailed audio summaries because they cannot identify which displayed track carries the feature.

## Files

- `formatter.json`: importable name and description templates.
- `description.txt`: description template for manual paste.

This formatter uses probed-track features documented for AIOStreams v2.35. Use a version supporting the variables/modifiers in the [current formatter reference](https://docs.aiostreams.viren070.me/reference/custom-formatter/).

## Verification

Both templates passed the upstream formatter validator. Ten sample audio render cases covered multilingual tracks, English originals, explicit original flags, commentary, missing metadata and aggregate fallback. Verify the preview on your installed AIOStreams version before saving.

## Sources

- [AIOStreams custom formatter reference](https://docs.aiostreams.viren070.me/reference/custom-formatter/)
- [AIOStreams formatter import implementation](https://github.com/Viren070/AIOStreams/blob/main/packages/frontend/src/components/menu/formatter/formatter-selection.tsx)
- [AIOStreams URL import implementation](https://github.com/Viren070/AIOStreams/blob/main/packages/frontend/src/components/shared/import-modal.tsx)
