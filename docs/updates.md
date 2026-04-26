# Snapdraft Updates

Snapdraft is designed to update through Sparkle.

## Appcast

The public appcast URL is:

https://ranyitz.github.io/snapdraft/appcast.xml

The current appcast is a valid placeholder feed. Future release automation will add signed update items and upload release artifacts.

## Release Artifacts

Release automation will manage update artifacts under `updates/` later. Do not add signing secrets, private keys, or notarization credentials to this repository.

## Troubleshooting

If the in-app updater fails, check that you can open the appcast URL in a browser. If the feed opens but the app still cannot update, create an issue with the Snapdraft version, macOS version, and the updater error message.
