# CI status

Here's the status of the CI on all the Lea repositories.

* [Lea-App](#lea-app)
* [Lea-Android-Device](#lea-android-device)
* [Lea-Back](#lea-back)
* [Lea-Dashboard](#lea-dashboard)
* [Lea-Doc](#lea-doc)
* [Lea-ESP32-Device](#lea-esp32-device)
* [Lea-Server](#lea-server)
* [Lea-Website](#lea-website)
* [Lea-Wiki](#lea-wiki)

## Lea-App:

[![Build](https://github.com/Lea-Voc/Lea-App/actions/workflows/build.yml/badge.svg)](https://github.com/Lea-Voc/Lea-App/actions/workflows/build.yml)

The CI will do the following at each push:

* Runs the Flutter tests
* Try to build an APK from the code
  * Check if the APK is aligned
  * Sign the generated APK if the push if from a tag starting with a `v`
  * Create a Github release and publish the signed APK

## Lea-Android-Device:

[![Build](https://github.com/Lea-Voc/Lea-Android-Device/actions/workflows/build.yml/badge.svg)](https://github.com/Lea-Voc/Lea-Android-Device/actions/workflows/build.yml)

The CI will do the following at each push:

* Try to build an APK from the code
  * Check if the APK is aligned
  * Sign the generated APK if the push if from a tag starting with a `v`
  * Create a Github release and publish the signed APK

## Lea-Back:

Main:[![Deploy](https://github.com/Lea-Voc/Lea-Back/actions/workflows/deploy.yml/badge.svg?branch=main)](https://github.com/Lea-Voc/Lea-Back/actions/workflows/deploy.yml)

Staging: [![Deploy](https://github.com/Lea-Voc/Lea-Back/actions/workflows/deploy.yml/badge.svg?branch=staging)](https://github.com/Lea-Voc/Lea-Back/actions/workflows/deploy.yml)

The CI will do the following at each push:

* Checkout the code
  * Run a linter on the updated files if branch is neither `main` nor `staging`
  * Run a linter on all the repository if the branch is `main` or `staging`
    * Build and deploy the production server if the branch is `main`
    * Build and deploy the development server if the branch is `staging`

## Lea-Dashboard:

[![Deploy](https://github.com/Lea-Voc/Lea-Dashboard/actions/workflows/deploy.yml/badge.svg)](https://github.com/Lea-Voc/Lea-Dashboard/actions/workflows/deploy.yml)

The CI will do the following at each push:

* Checkout the code
  * Run a linter on the updated files if branch is neither `main` nor `staging`
  * Run a linter on all the repository if the branch is `main` or `staging`
    * Build and deploy the production server if the branch is `main`
    * Build and deploy the development server if the branch is `staging`

## Lea-Doc:

[![Deploy](https://github.com/Lea-Voc/Lea-Doc/actions/workflows/delpoy.yml/badge.svg)](https://github.com/Lea-Voc/Lea-Doc/actions/workflows/delpoy.yml)

The CI will do the following at each push:

* Run a linter on all the repository
* Checkout the code
* Restart the swagger-ui container

## Lea-ESP32-Device:

[![ESP32 Builder](https://github.com/Lea-Voc/Lea-ESP32-Device/actions/workflows/build.yml/badge.svg)](https://github.com/Lea-Voc/Lea-ESP32-Device/actions/workflows/build.yml)

The CI will do the following at each push:

* Checkout the code
* Try to build the firmware

## Lea-Server:

[![Deploy](https://github.com/Lea-Voc/Lea-Server/actions/workflows/deploy.yml/badge.svg)](https://github.com/Lea-Voc/Lea-Server/actions/workflows/deploy.yml)

The CI will do the following at each push:

* Run a linter on all the repository
* Checkout the code if the branch is `main`
  * Build the lea_node docker image
  * Restart the updated container

## Lea-Website:

No CI is available for this repository yet.

## Lea-Wiki

[![Lint](https://github.com/Lea-Voc/Lea-Wiki/actions/workflows/lint.yml/badge.svg)](https://github.com/Lea-Voc/Lea-Wiki/actions/workflows/lint.yml)


The CI will do the following at each push:

* Run a linter on all the repository