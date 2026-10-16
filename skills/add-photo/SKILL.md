---
name: add-photo
description: Get the user's own photo into DesignerBox so the other DesignerBox tools can use it. Use when the user wants to work on a product photo, a picture of themselves, or any image of theirs, mentions attaching or uploading an image, or names a file on their computer.
---

Every DesignerBox image tool takes the image as a URL. Before you apply a template or edit a photo, get a URL for it in one of these ways, in this order.

## 1. It is already in their library

If the user says the photo is already in DesignerBox, or names one they made earlier, call `list_assets` (use `type: "image"`) and pick it by name or date. Use `get_asset` if you need its full detail. Use the asset's `url` in the next tool.

## 2. Upload it in the chat (claude.ai, Desktop and Cowork)

Images attached to a chat message do not reach DesignerBox. Do not try to describe or re-create the attached image. Instead:

1. Call `upload_asset` with no arguments. An upload panel opens in the chat.
2. Tell the user to choose the file in that panel.
3. When the upload finishes, the tool hands back the file's `url`. Use it in the next tool.

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

4. The response is JSON with `assetId` and `url`. Use that `url` in the next tool.

An upload token works once. If the upload fails, call `upload_asset` again for a new one.

## 4. A public image link

If none of the above works, a public `https://` image link the user gives you can be passed to the image tools as it is.

## Limits

Uploads count against the storage on the user's DesignerBox plan. If an upload is refused for storage, tell the user in plain words and stop. Do not send them to a pricing or checkout page.
