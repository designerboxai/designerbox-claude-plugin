---
name: add-photo
description: Upload the user's own photo or video to their DesignerBox library. Use when the user wants to save, upload or add an image or video to DesignerBox, mentions attaching a file for DesignerBox, or names a file on their computer to put in their library.
---

DesignerBox keeps the user's product photos and videos in their library. This skill gets a file from the user into that library.

## 1. Check it is not already there

If the user says the photo is already in DesignerBox, call `list_assets` (use `type: "image"`, or `"video"`) and find it by name or date instead of uploading it again. Use `get_asset` for its full detail and link.

## 2. Upload it in the chat (claude.ai, Desktop and Cowork)

Files attached to a chat message do not reach DesignerBox. Do not try to describe or re-create an attached image. Instead:

1. Call `upload_asset` with no arguments. An upload panel opens in the chat.
2. Tell the user to choose the file in that panel.
3. When the upload finishes, the panel confirms it and hands back a link to the file. Share that link and tell the user the file is in their DesignerBox library.

Do not ask the user to paste base64 or a link into the chat.

## 3. Upload a file from their computer (Claude Code)

Claude Code has no upload panel, but it can send a local file the user names:

1. Check the file exists and is a JPEG, PNG, WebP, GIF, MP4 or WebM under 50 MB.
2. Call `upload_asset`. Keep `uploadUrl` and `uploadToken` from the result. Do not show the token to the user.
3. Send the file with one request, setting the content type to match the file:

   ```sh
   curl -sS -X PUT "<uploadUrl>" \
     -H "Authorization: Bearer <uploadToken>" \
     -H "Content-Type: image/png" \
     -H "X-Upload-Filename: <file name>" \
     --data-binary @"<path to file>"
   ```

4. The response is JSON with `assetId` and `viewUrl`. Share `viewUrl` with the user; it opens the file.

An upload token works once. If the upload fails, call `upload_asset` again for a new one.

## Limits

Uploads count against the storage on the user's DesignerBox plan. If an upload is refused for storage, tell the user in plain words and stop. Do not send them to a pricing or checkout page.
