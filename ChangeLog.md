# Revision history for obelisk

This project's release branch is `master`. This log is written from the perspective of the release branch: when changes hit `master`, they are considered released, and the date should reflect that release.

## Unreleased

* Generalised pathSegmentEncoder, added pathFieldEncoder.
* Added some Prisms to the encoder library for manipulating DSums (perhaps they should get moved to dependent-sum before release?)
* Add "ob doc" command, which lists paths to haddock documentation for specified packages
* Bump reflex-platform so that obelisk now uses GHC 8.6.5 and the nixos-19.03 nixpkgs set
* Add support in obelisk-route for single parameters in URL paths
* Bump reflex-platform so that obelisk now uses reflex-dom 0.5.2.0
* Use a `--pure` nix shell in `ob run` for parity with `ob repl` and more resilience against "works on my machine".
* Use `--keep NIX_PATH` for all pure shells so references to `<nixpkgs>` continues to work.
* Backport ACMEv2 support in obelisk server to regain LetsEncrypt account creation.
* Enable HTTPS in `ob run`.
* `ob run` now handles `ghci` errors better, and includes a custom `ghcid`
  version. As a result, you no longer need to have ghcid installed to
  use `ob run`, as we provide one for you.
* `ob` commands now complain less on systems with umasks other than `0022`.
* Ignore package environment files in `ob run` and `ob repl`.
* Add `Obelisk.Route.Frontend.routeLinkDynAttr`.
* Add `check-known-hosts` option in `ob deploy init`

## v0.2.0.0 - 2019-8-17

* Configs become ByteStrings.
* FrontendConfigsT has been changed into ConfigsT and configs are made available via getConfig/getConfigs
  * The frontend will still only have access to configs that are placed in config/frontend and config/common, while the backend has access to the entire contents of the config directory via `Obelisk.ExecutableConfig.Lookup.getConfigs`.
* The backend no longer runs in BackendConfigsT.
* Add tabulation package. See Data.Tabulation for details.
* Add encoders for `DMap`, `HasFields` (cf. Data.Tabulation), and JSON.
* Use IP address for nginx proxy pass instead of localhost

## v0.1.1.0 - 2019-05-17

* Fix crashes of Android apps on 32-bit ARM devices.
* Provide a way to indicate acceptance of the Android SDK license by passing `config.android_sdk.accept_license = true;` in the arguments to the import of `.obelisk/impl` in the project's `default.nix`.
* Add `COMPLETE` pragma to `(:/)`. Using this pattern synonym should no longer generate spurious warnings about non-exhaustive pattern matching.
* Make asset path hashing strict (see `Obelisk.Asset.Gather`)
* Add the `ob shell` command to enter a nix shell for an obelisk project
* Allow skeleton's obelisk to be overridden. This changes the skeleton's default.nix interface: the arguments that it used to take are now part of the new "obelisk" argument.
* Removed `MonadIO` from `ObeliskWidget` to prevent accidental IO during prerendering. If you need to do IO in a widget it should be on the right hand side of a `prerender`.
* Significantly changed the interface to the "executable config" packages. `obelisk-executable-config-lookup` is a new internal package which looks up all configs in a platform-specific way. `obelisk-executable-frontend` and `obelisk-executable-backend` provide MTL-style monad classes (`HasFrontendConfigs` and `HasBackendConfigs`) which the frontend and backend, respectively, can use to look up configs. This replaces the old `get` function which ran in `IO`.
* Add a flag to force thunk packing even if there are unpushed changes in the unpacked thunk.


## v0.1.0.0 - 2019-03-29

* Use reflex-dom's `HydrationDomBuilder` to "hydrate" statically rendered DOM served by the Obelisk backend (rather than re-creating DOM and replacing it all).
* Add `HasCookies` and `CookiesT` to allow `ObeliskWidget`s to access cookies during static and "hydrated" DOM rendering.
