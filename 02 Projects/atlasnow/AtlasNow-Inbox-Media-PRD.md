# AtlasNow — Inbox media

Status: build 2026-10-31. Product scope only. Money stays in [[AtlasNow-Monetization-PRD]]. A session reply is still a service message. This file does not add a credit, a price, or unlimited storage.

## Decision

WhatsApp HQ inbox can keep a customer **video**, **voice note**, and **document** as a download. The reply box can send a **photo**, **video**, and **document**. Text stays as it is.

Branch WhatsApp stays watch-only. Voice notes are not sent from AtlasNow.

Messenger and Instagram use the same receive rules when Meta includes a CDN link for a photo, video, voice note, or file. The reply box can send a photo or video on both. A document can be sent on Messenger. Instagram does not accept a document send.

## Receive

Cloud webhook types `image`, `audio`, `video`, and `document` are downloaded once and stored on the message. The thread shows a photo inline. Video, voice, and document are a download link with the original filename when Meta sent one.

`unsupported` messages stay a label. Meta does not send a file for those.

Do not store a file when:

- the name ends in `.exe` or `.rar`
- the bytes are a Windows executable (`MZ`) or a RAR archive
- the type is outside photo JPEG/PNG/WebP, voice/audio OGG/MPEG/MP4/AAC/AMR, video MP4/3GPP, or document PDF/Office/text/CSV
- the file is empty or over the cap: photo 8 MB, voice 16 MB, video 16 MB, document 16 MB

A rejected file leaves the chat row and the words “File type not saved”. The bytes are not kept.

## Send

From a WhatsApp HQ chat, a person can attach one photo, video, or document, with an optional caption. The same type rules apply. The file is uploaded to that number’s Cloud API media endpoint and sent inside the open service window. A closed window still fails the way a text reply fails.

## Retention

Stored files use the workspace inbox photo retention already on the tenant, default 30 days. After that the bytes are removed and the chat text stays. The thread says the file was removed.

## Not this slice

No voice-note recording. No `.zip` ban beyond `.exe` and `.rar`. No new meter. No send from a branch number. Instagram document send stays off because that API has no file attachment.
