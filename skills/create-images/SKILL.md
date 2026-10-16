---
name: create-images
description: Create or edit images with DesignerBox. Use when the user asks DesignerBox for a new image from a description, wants to change, relight, re-angle or restyle a photo, remove a background, or make a product ad or flat lay from their own photos.
---

Pick the tool that matches what the user wants. For anything that starts from the user's own photo, follow the `add-photo` skill first to get its URL. If a curated template fits what they want, the `product-photos` skill gives better results than writing a prompt from scratch.

| The user wants | Tool | Notes |
| --- | --- | --- |
| A new image from a description | `generate_image` | `prompt`, optional `aspectRatio`, `numberResults` 1 to 4 |
| To change something in a photo | `edit_image` | `prompt` says what to change; `referenceImages: [{ imageUrl, type: "raw" }]` |
| A transparent background | `remove_background` | `imageUrl` |
| A product ad | `product_ad` | `imageUrl`, `productName`, optional `productDescription` |
| Several products laid out flat | `flat_lay` | `imageUrls` (1 to 8), `background`, `style`, `itemCount` |
| New lighting | `spotlight` | `imageUrl`, light direction and brightness |
| The product from another angle | `photo_angles` | `imageUrl`, `rotation`, `tilt`, optional `zoom` |

## Steps

1. **Check credits.** Call `get_plan_limits` once per conversation before the first image job. If the user has no AI credits left, tell them in plain words and stop.
2. **Choose the model only when it matters.** `generate_image` and `edit_image` use a capable default. If the user asks for something cheaper, faster or a named model, call `list_image_models`, which lists each model's credit cost per image, and pass its id as `model`.
3. **Run the tool.** Write the prompt from what the user said; add detail about light, background and framing when they leave it open. If the user has a brand profile (`list_brand_profiles`), keep to its colors and tone.
4. **Show the result.** The images appear in the chat. Tell the user how many credits it used (`creditsCharged`) and share `libraryUrl`, where every image is saved.

## Good to know

- Image jobs take around 30 seconds.
- Before a job of more than four images, say it will use credits for each image and confirm.
- When you retry the same request after an error, pass the same `clientRequestId` so the user is not charged twice.
- Never paste the raw tool response, and never mention prices, plans or upgrades or link to checkout.
- Do not delete anything from the user's library unless they ask for that exact item to be deleted.
