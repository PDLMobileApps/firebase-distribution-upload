# firebase-distribution-upload
This action uploads a file (apk, aab or ipa) to Firebase Distribution.

Note that `firebase-cli` has to be installed in your runner for this action to work. See [Setup Firebase CLI](https://github.com/marketplace/actions/setup-firebase-cli) or other similar actions for details.

## Inputs

### `appId`

**Required** App id can be found in the Firebase console in your Projects Settings, under Your apps ( format 1:1234567890123942955466829:android:1234567890abc123abc123).

### `token`

**Required** Upload token - See Firebase CLI Reference (run `firebase login:ci` command to get your token).

### `file`

**Required** Artifact to upload (.apk, .aab or .ipa)

### `groups`

Distribution groups.

### `releaseNotes`

Release notes visible on release page.

## Sample usage

Here is an example of how you can use this action in your workflow:

```
name: Upload to Firebase Distribution Workflow

on: [push]

jobs:
    clean-runner:
        runs-on: macos-latest
        steps:
            - name: MRTN Staging Firebase upload
                uses: PDLMobileApps/firebase-distribution-upload@main
                with:
                    appId: ${{ secrets.FIREBASE_APP_ID }}
                    token: ${{ secrets.FIREBASE_TOKEN }}
                    file: app/build/outputs/apk/myapp/release/app.apk
                    groups: qa
                    releaseNotes: "Some build - ${{ github.ref_name }} branch - commit ${{ github.sha }} - ${{ github.event.pull_request.user.login }} - ${{ github.event.pull_request.title }}" 
```

## Credits

This works is based on the Github action [wzieba/Firebase-Distribution-Github-Action](https://github.com/wzieba/Firebase-Distribution-Github-Action/)