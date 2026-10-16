# DesignerBox for Claude

![DesignerBox](assets/logo.png)

[DesignerBox](https://designerbox.ai/) turns product photos into studio-style images for ads, online stores and social posts, from a conversation with Claude. This plugin connects Claude to your DesignerBox account and teaches it the DesignerBox workflow: get your photo in, pick a curated image template or describe the shot, and save every result to your DesignerBox library.

It works in Claude chat, Cowork and Claude Code.

## What you can do

- Upload a product photo through an upload panel in the chat, or, in Claude Code, by naming a file on your computer
- Browse and apply curated image templates, for example a full set of online-store listing shots
- Generate new images from a description
- Edit photos: change details, remove the background, relight the shot or show the product from a new angle
- Make product ads and flat lays from your own product photos
- Browse your DesignerBox assets, designs and brand profiles

## What is inside

- `.mcp.json` connects to the DesignerBox MCP server at `https://mcp.designerbox.ai/api`. You sign in with your own DesignerBox account the first time you connect.
- `skills/add-photo` gets your photo into DesignerBox.
- `skills/product-photos` applies DesignerBox image templates to your product photos.
- `skills/create-images` generates and edits images with the DesignerBox image tools.

The plugin contains no code that runs on your computer. In Claude Code, the `add-photo` skill may ask Claude to send a file you name to `https://mcp.designerbox.ai` with `curl`, using a one-time upload token from your DesignerBox account.

## Before you start

You need a DesignerBox account. Generating and editing images uses the AI credits in your account, and Claude tells you how many each result used. DesignerBox only reaches the workspaces your connected account belongs to. AI images can get details wrong, so check product names, labels and colors before you publish.

## Data

When you use this plugin, Claude sends your requests (prompts, template choices and image settings) and the images you choose to upload to your DesignerBox account through `mcp.designerbox.ai`. Generated images are saved to your DesignerBox library. The plugin itself stores nothing. How DesignerBox handles your data is described in the privacy policy at https://designerbox.ai/privacy, including the section on using DesignerBox from an AI assistant.

## Help

Documentation: https://designerbox.ai/docs/integrations/mcp

Support: https://designerbox.ai/contact or contact@designerbox.ai
