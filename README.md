# OpenWrt CI out of tree build with OpenWrt SDK for GitHub Actions

GitHub Actions doesn't allow direct inclusion of remote YAML files so we need following custom plugin which wraps the
[OpenWrt CI](https://gitlab.com/ynezz/openwrt-ci) for better reusability and sharing in GitHub Actions CI environment.

## Example usage

```yaml
name: OpenWrt CI testing

on: [ push, pull_request ]
env:
  CI_ENABLE_UNIT_TESTING: 1
  CI_TARGET_BUILD_DEPENDS: ubus
  CI_CMAKE_EXTRA_BUILD_ARGS: -DLUAPATH=/usr/lib/lua

jobs:
  sdk_build:
    name: Build with OpenWrt ${{ matrix.sdk_platform }} SDK (out of tree)
    runs-on: ubuntu-latest

    strategy:
      fail-fast: false
      matrix:
        sdk_platform:
          - ath79-generic
          - imx-cortexa9
          - malta-be
          - mediatek-mt7622

    steps:
      - uses: actions/checkout@v3

      - name: Out of tree build with OpenWrt ${{ matrix.sdk_platform }} SDK
        uses: ynezz/gh-actions-openwrt-ci-sdk@v0.0.2
        env:
          CI_TARGET_SDK_RELEASE: master
          CI_TARGET_SDK_IMAGE: ${{ matrix.sdk_platform }}
```
