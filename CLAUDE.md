@AGENTS.md

## Claude Code

- Verify Swift edits with the unsigned simulator `xcodebuild` build from AGENTS.md before reporting done.
- The project and scheme names contain a space, so always quote `"ESG Connect.xcodeproj"` and `"ESG Connect"` in Bash.
- Do not open, cat or grep `ESGConnect/GoogleService-Info.plist`; exclude it from searches over `ESGConnect/`.
- Edit `project.pbxproj` only when adding or removing files, and keep changes minimal; prefer asking the owner to add files in Xcode.
