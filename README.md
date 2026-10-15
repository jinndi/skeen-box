# sing-box for Keenetic / Netcraze

> [!IMPORTANT]
> If your proxy provider uses Xray version 26.9.8 or later and doesn't understand why they are losing existing clients or failing to attract new ones, while you experience connection issues with REALITY nodes, try one of the following fingerprints: `firefox`, `safari`, `random`, or `randomized`. The `chrome` and `random` fingerprints are not recommended.
>
> In all other cases, use the official sing-box binaries.

sing-box builds for Keenetic and Netcraze routers with additional patches.

This is not the upstream `sing-box` source code, but a release project for building ready-to-use binaries for architectures commonly used in Keenetic / Netcraze routers. The main goal is to build sing-box with the required build tags and patches, verify the REALITY ClientHello, and publish the resulting artifacts in GitHub Releases.

[Русская версия](README.ru.md)

## About the Project

The repository automatically:

- Fetches the required version of upstream `SagerNet/sing-box` by tag.
- Downloads and applies additional patches from external sources.
- Checks whether each patch can be applied before applying it.
- Builds binaries for the target architectures.
- Adds the required `build tags`.
- Compresses binaries with `UPX` when applicable.
- Verifies that the built binary passes the REALITY test.
- Publishes the results in GitHub Releases.

## Supported Builds

GitHub Actions builds binaries for the following configurations:

- `linux/arm64` + `musl`
- `linux/mipsle` + `softfloat` + `musl`
- `linux/mips` + `softfloat`

The following additional tags are enabled for `arm64` and `mipsle`:

- `with_naive_outbound`
- `with_musl`

The following common tags are used for all builds:

- `with_quic`
- `with_utls`
- `with_clash_api`
- `badlinkname`
- `tfogo_checklinkname0`
- `with_gvisor` for stable releases

UPX-compressed versions are published with the `_upx` suffix.

## Applied Patches

Patches are downloaded from external repositories and applied to the upstream `sing-box` source code.

Before applying each patch, compatibility with the current source code is checked using `git apply --check`. If the check succeeds, the patch is applied. If downloading, checking, or applying a patch fails, the build terminates with an error.

Applied patches:

- `0001-reality-keep-X25519MLKEM768-key-share-announce-clien.patch`
- `0002-utls-firefox-Firefox-148-safari-Safari-26.3-as-Xray-.patch`
- `0010-utls-keep-the-randomized-fingerprint-consistent.patch`

Patch source: [FiyeroT/podkop-engine](https://github.com/FiyeroT/podkop-engine). See the repository for details.

The patch list may be expanded. Sources are documented as new patches are added.

## Pre-release Verification

The workflow [.github/workflows/build.yml](.github/workflows/build.yml) performs the following checks before publishing:

1. Downloads the official upstream `sing-box` source for the selected version.
2. Checks whether the additional patches can be applied and applies them sequentially.
3. Tests the original, unpatched binary as part of REALITY verification.
4. Builds binaries with the patches applied.
5. Runs the verification script at [.github/verify/reality/verify.sh](.github/verify/reality/verify.sh).
6. Publishes artifacts to GitHub Releases if all required checks pass.

This helps detect patch incompatibilities with the selected upstream version and reduces the risk of publishing binaries that fail REALITY testing.

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE).