# Upload dSYMs to Firebase Automator quick action

I get annoyed by having to upload dSYMs to Firebase each time something goes south, so here's how I solved it:

<img width="526" alt="Screen Shot 2021-05-04 at 1 35 21 AM" src="https://user-images.githubusercontent.com/26014377/116942856-16e51980-ac7b-11eb-9ec9-2f0fafa3618e.png">

## How to set up this magnificent creature

1. Launch **Automator**
2. *File* -> *New* -> *Quick Action*
3. Find **Run Apple Script** item in the **Library** and drag it into the editor
<img width="1345" alt="Screen Shot 2021-05-04 at 1 45 05 AM" src="https://user-images.githubusercontent.com/26014377/116942863-19477380-ac7b-11eb-826b-d73f52627d1c.png">
4. Copy & Paste the following code, replacing your_repo_full_path with you-know-what

    on run {input, parameters}
      tell application "Terminal"
        activate
        do script "your_repo_full_path/Pods/FirebaseCrashlytics/upload-symbols -gsp your_repo_full_path/GoogleService-Info.plist -p ios " & (quoted form of (POSIX path of input))
      end tell
    return input
    end run

5. Rejoice!

The script is gonna open a new terminal window and start uploading your debug symbols
