---
name: browse-library
description: Find and manage what is in the user's DesignerBox account - pictures and videos in their library, Studio designs, brand profiles and brand assets, their plan and teams. Use when the user asks what is in DesignerBox, wants a file or design they saved, asks about or wants to change their brand profile, or asks which plan or team they are on.
---

DesignerBox results include links that open the item, or the library, in the DesignerBox app. Share the link with the user.

## Pictures and videos

- `list_assets` lists the library, newest first. Pass `type: "image"` or `"video"` to narrow it, `folderId` for one folder, and `page` / `limit` to page through (up to 100 per page). Read the names and dates to find what the user means.
- `list_folders` shows the folders, so you can pass a `folderId`.
- `get_asset` with the asset `id` returns the full detail and a link that opens the file.

## Designs

- `search_designs` with `search` finds Studio designs by title or content. Use it when the user names a design.
- `list_designs` browses designs without a filter, with `page` / `limit`.
- `get_design` with the design `id` returns its detail and a link that opens it in the editor.

## Brand

- `list_brand_profiles` shows the profiles in the active team and which one is the default.
- `get_brand_profile` with `brandProfileId` returns one profile in full (voice, themes, goals, niche, industry).
- `list_brand_assets` and `get_brand_asset` show the logos, fonts and other brand files.
- To change a profile, use `update_brand_profile`; to add one, `create_brand_profile`; to make one the default, `set_default_brand_profile`. Say what you are about to change before you change it.

## Account and teams

- `get_plan` returns the plan name, billing cycle, renewal date and trial end.
- `list_teams` shows the user's teams and the active one. `set_current_team` with a `teamId` switches the team that every other tool works in. Tell the user when you switch.

## Deleting

`delete_asset` and `delete_design` remove an item for good. Always name the item and ask the user to confirm before calling either one.

## When something is missing

If a list comes back empty, check the active team with `list_teams` before telling the user nothing is there: the item may be in another team.
