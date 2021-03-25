# OpenWrt CI out of tree build with OpenWrt SDK for GitHub Actions

GitHub Actions doesn't allow direct inclusion of remote YAML files so we need following custom plugin which wraps the
[OpenWrt CI](https://gitlab.com/ynezz/openwrt-ci) for better reusability and sharing in GitHub Actions CI environment.
