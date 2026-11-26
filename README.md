# sing-box for Keenetic / Netcraze

sing-box builds for Keenetic and Netcraze routers.

This is not the upstream `sing-box` source code, but a release project for building ready-to-use binaries for architectures commonly used in Keenetic / Netcraze routers. The main goal is to build sing-box with the required build tags and publish the resulting artifacts in GitHub Releases.

[Русская версия](README.ru.md)

## About the Project

The repository automatically:

- Fetches the required version of upstream `SagerNet/sing-box` by tag.
- Builds binaries for the target architectures.
- Adds the required `build tags`.
- Compresses binaries with `UPX` when applicable.
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

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE).