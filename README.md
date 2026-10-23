# DesignerBox for Claude

![DesignerBox](assets/logo.png)

[DesignerBox](https://designerbox.ai/) keeps your product photos, designs and brand profiles in one library. This plugin connects Claude to your DesignerBox account so you can add photos to your library and find your work from a conversation, without switching apps.

It works in Claude chat, Cowork and Claude Code.

## What you can do

- Upload a product photo or video to your library through an upload panel in the chat, or, in Claude Code, by naming a file on your computer
- Find pictures and videos in your library, browse folders, and open any file
- Search and open your Studio designs
- Read and update your brand profiles and see your brand assets
- Check your plan and switch between your teams

The plugin does not create or edit images, and it does not use your DesignerBox credits.

## What is inside

- `.mcp.json` connects to the DesignerBox connector at `https://mcp.designerbox.ai/claude`. You sign in with your own DesignerBox account the first time you connect.
- `skills/add-photo` uploads your photo or video to your DesignerBox library.
- `skills/browse-library` finds and manages what is in your account: files, designs, brand profiles, plan and teams.

The plugin contains no code that runs on your computer. In Claude Code, the `add-photo` skill may ask Claude to send a file you name to `https://mcp.designerbox.ai` with `curl`, using a one-time upload token from your DesignerBox account.

## Before you start

You need a DesignerBox account; the free plan works. DesignerBox only reaches the workspaces your connected account belongs to. Deleting a file or a design cannot be undone, and Claude asks you to confirm first.

## Data

When you use this plugin, Claude sends your requests and the files you choose to upload to your DesignerBox account through `mcp.designerbox.ai`. Uploaded files are saved to your DesignerBox library, and DesignerBox does not send them to any AI model. The plugin itself stores nothing. How DesignerBox handles your data is described in the privacy policy at https://designerbox.ai/privacy.

## Help

Documentation: https://designerbox.ai/docs/integrations/claude-connector

Support: https://designerbox.ai/contact or contact@designerbox.ai
