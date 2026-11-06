# Use Craft Anything to study G-Labs Studio

This guide sets up a desktop-app project for an original app inspired by the visible workflow in G-Labs Studio. Craft Anything already has a built-in desktop-app path: it can study a window, ask a coding agent to build an app, and compare the result with a captured screenshot.

## Start with a clean-room capture

1. Open Craft Anything and start a new project. Choose **App** and select the installed G-Labs Studio executable as the target.
2. Leave **Clean room** selected. In **Settings → Safety**, turn on **Run to study** if you want Craft Anything to launch the app once and capture its window and visible controls. The capture happens about 15 seconds after launch.
3. Start the project and describe the screens and actions you want to understand. If the app opens a sign-in screen, stop there; don't provide account credentials or ask the builder to access an account.

Clean room keeps the original app's files and code closed. It is a boundary in Craft Anything's tools, not an operating-system sandbox, so the coding agent still acts with its own permissions.

## Example build request

Use a request like this, then replace the bracketed parts with what you want:

> Build a new, original Windows desktop app based on the high-level workflow I described from G-Labs Studio. Let me prepare image and video generation jobs, queue and control batches, and connect workflow steps as nodes. Start with [the one screen or flow I care about most]. Use Rust + egui unless another stack is a better fit. Use a local mock provider so the app builds and runs without signing in or sending generation requests to external services. Create original names, artwork, text, and UI details; don't reuse G-Labs Studio branding or assets.

Starting with one flow makes the first build easier to inspect. Add other screens or providers as follow-up requests after the basic app builds.

## Inspect and refine

- Review `capture/window.png` and `capture/ui-tree.json` in the project to see what Craft Anything recorded from the running window.
- Check the build and screenshot results on the project page. Open the generated app and try its main actions yourself; the desktop-app workflow checks the build and appearance, while broader interaction checks are still partial.
- Ask for one concrete change at a time in the project prompt box, such as “let me reorder queued jobs” or “show which node input is missing.”
- Keep Clean room enabled when you are building an original app from visible behavior. Use Deep mode only when you are authorized to inspect the target's files and code, and only for your private use.

You can also start from the CLI after enabling **Run to study** in Settings:

```sh
craft-anything-cli rebuild "<absolute path to G-Labs Studio executable>" "Build an original desktop app for preparing and controlling image and video generation jobs, starting with a node-based workflow editor. Use a local mock provider; don't access external accounts." --clean-room --rounds 1
```

G-Labs Studio documents its node workflow format separately. This recipe is for studying the desktop app and building your own app; it does not import or run G-Labs workflow files.

