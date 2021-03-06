# cep-packager

[![Build Status](https://aedtci.mtmograph.com/api/badges/adobe-extension-tools/cep-packager/status.svg)](https://aedtci.mtmograph.com/adobe-extension-tools/cep-packager)
[![npm version](https://badge.fury.io/js/cep-packager.svg)](https://www.npmjs.com/cep-packager)

This packager allows you to create native macOS and Windows installers for a CEP extension.
It takes a configuration file (it looks for it in the folder where you are running the command from) and a folder that contains the files that have to be packaged up (usually generated by `cep-bundler`) as input.

The easiest way to use this package is to use the `cep-starter` package, which already depends on the `cep-packager` and has a default config.

However, you can also use this package standalone, for that, follow the instructions below:

## requirements

- macOS
- node.js
- homebrew
- wine
- makensis

```shell
# install homebrew
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# install makensis
brew install wine makensis
```

## install

```shell
npm install --save cep-packager
```

## configure

- Copy the `cep-config.js` file from the `cep-starter` package into you project folder.
- Modify desired options

Run the packager:
```shell
./node_modules/.bin/cep-packager
```

Or, add to your `package.json`'s scripts section:

```json
"scripts": {
  "package": "cep-packager"
}
```

Then you can run the packager like this:

```shell
npm run package
```

## CLI usage

Instead of using the `cep-config.js` configuration file you can also use CLI arguments or environment variables.
For this, it is recommended to install `cep-packager` globally like this:

```shell
npm install -g cep-packager
```

Basic example:

```shell
cep-packager \
	--name testpackage \
	--bundle-id com.test.testpackage \
	--version 0.0.1 \
	--macos-resources $PWD/resources/macos \
	--windows-resources $PWD/resources/windows \
	--macos-dest $PWD/0.0.1.pkg \
	--windows-dest $PWD/0.0.1.exe \
	./testpackage
```

Example with signing:

```shell
cep-packager \
	--name testpackage \
	--bundle-id com.test.testpackage \
	--version 0.0.1 \
	--macos-resources $PWD/resources/macos \
	--windows-resources $PWD/resources/windows \
	--macos-dest $PWD/0.0.1.pkg \
	--windows-dest $PWD/0.0.1.exe \
	--windows-cert path/to/cert.p12
	--windows-cert-password passwordofp12file
	--zxp-cert path/to/cert.p12
	--zxp-cert-password passwordofp12file
	--macos-keychain login.keychain
	--macos-keychain-password loginkeychainpassword
	--macos-identifier "Developer ID Installer: Your Name"
	./testpackage
```

## develop

```shell
git clone https://github.com/adobe-extension-tools/cep-packager.git
cd cep-packager
npm install
npm start
```