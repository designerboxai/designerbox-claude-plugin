---
name: product-photos
description: Turn a product photo into a set of studio-style shots with a DesignerBox image template. Use when the user wants product photos, ad images, listing images or social posts for something they sell, asks for a photoshoot look, or names a DesignerBox template.
---

DesignerBox templates are tested looks, for example a perfume shot on dark stone or a full set of online-store listing images. You pick the template and pass the user's photo; DesignerBox keeps the recipe on its side and returns finished images.

## Steps

1. **Find the template.** Call `list_image_templates` with `q` set to the product or the look the user wants (for example `perfume`, `sneakers`, `jewelry`, `flat lay`). If they named a template, search for its name. Show them two to four matches by title and let them choose, unless they already named one.
2. **Get the photo.** Follow the `add-photo` skill to get a URL for the user's product photo. Skip this only if the user wants the template's look without their own product.
3. **Check credits.** Call `get_plan_limits` once per conversation before the first image job. If the user has no AI credits left, tell them in plain words and stop.
4. **Apply it.** Call `apply_image_template` with the template's `templateId` (or `slug`) and `referenceImages: [{ imageUrl: "<photo url>" }]`. Leave the image's `type` unset: the default keeps the user's product or person in the shot. Leave `numberResults` unset to get the template's normal set, which is often six images. If the user asks for fewer, set it.
5. **Show the result.** The images appear in the chat. Tell the user how many credits the run used (`creditsCharged`) and share `libraryUrl`, where every image is saved.

## Good to know

- A template run takes up to about a minute. Say so before you start.
- Before a run of more than four images, tell the user it will use credits for each image and confirm they want it.
- Never paste the raw tool response. Describe the result in a sentence or two.
- AI images can get product details wrong. Remind the user to check labels, names and colors before they publish.
- Do not mention prices, plans or upgrades, and never link to checkout. If a tool says the plan does not allow something, pass that on in plain words.
