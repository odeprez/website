---
author: shebu-kuriakose
title: Trusted Firmware-M v1.7.0 updates
date: 2022-12-08 10:00:00

image: "../../assets/images/blog/musca_tf_crop_1500x1500.png"
---

# **Trusted Firmware-M: v1.7.0: New Profile, Improve Configurability and FWU API 1.0**

## Introduction

Trusted Firmware-M (TF-M) [v1.7.0](https://git.trustedfirmware.org/TF-M/trusted-firmware-m.git/tag/?h=TF-Mv1.7.0) was released on 8 th December 2022. The major additions in the release include new Medium-ARoT-less profile, improving configurability by introducing Kconfig and configuration header files along with the Base configuration and alignment with PSA Certified Firmware Update API 1.0.

## Release Highlights

Below are the main additions in TF-Mv1.7.0:

- New Profile: In addition to Profile Small, Medium and Large Profiles, Medium-ARoT-less profiles is
  available.

  Medium-ARoT-less aligns with security requirements defined in PSA Certified ARoT-less Level 2 [protection profile](https://www.psacertified.org/app/uploads/2022/10/JSADEN019-PSA_Certified_Level_2_PP_SESIP_ARoT-less_REL-01.pdf). This allows devices that don’t require Application Root Of Trust (ARoT) to support Isolation Level1 and meet PSA L2 certification requirements.

  These profiles give users more options to easily build the TF-M configuration that meets their security requirements and thereby achieve PSA certification without any unnecessary memory or performance overheads. Find more about TF-M Profiles [here](https://tf-m-user-guide.trustedfirmware.org/configuration/profiles/index.html).

- **Improved Configurability:** The new Base configuration includes the Secure Partition Manager (SPM) and platform code. This skeleton configuration can be used as a foundation to add the secure services required by the user.

  CMake variables were used for build and component options. To improve and simplify configuring TF-M, configuration header files have been introduced to set component options. Build options remain in CMake and can be ported to another build system.

  Kconfig has been introduced for users to change configuration options. Starting from the base configuration, a user can enable necessary services and options. Kconfig ensures selected options are consistent and valid. Kconfig makes configuration easier and less error-prone and offers a GUI to assist users.

  Details on configuration can be found [here](https://tf-m-user-guide.trustedfirmware.org/configuration/index.html).

- **PSA Certified Firmware Update API 1.0:** The firmware update partition has been updated to align with the recently released [PSA Certified Firmware Update 1.0 Specification](https://arm-software.github.io/psa-api/fwu/1.0/IHI0093-PSA_Certified_Firmware_Update_API-1.0-bet.0.pdf). TF-M v1.6 was aligned to v0.7 of the Specification.

- The programming model and communication framework, **Library model** has been removed. The release supports [PSA-FF-M](https://developer.arm.com/documentation/aes0039/latest) defined IPC and SFN mechanisms.

- TF-M Crypto Service has been updated to include Mbed TLS3.2.1. Earlier only a limited subset of crypto operations in TLS, X.509 and PK used PSA Crypto APIs. In Mbed TLS 3.2.1, most of the crypto operations are done using PSA Crypto APIs with a few exceptions. Refer [here](https://github.com/Mbed-TLS/mbedtls/blob/development/docs/use-psa-crypto.md) for list of exceptions. This allows TLS stack running in the Non-Secure Processing Environment (NSPE) to use PSA Crypto APIs in TF-M Crypto service for most of the crypto operations.

- Further memory optimizations including introducing MM-IOVECS in partitions and enabling configurable stack sizes are part of the release. Latest memory usage figures can be found [here](https://tf-m-user-guide.trustedfirmware.org/releases/1.7.0.html).

- Changes in Initial Attestation Service to support [PSA 2.0.0 attestation profile](https://www.ietf.org/archive/id/draft-tschofenig-rats-psa-token-09.html).

- As part of improving documentation, the platform, integration and configuration sections have been restructured.

More details can be found [here](https://tf-m-user-guide.trustedfirmware.org/releases/1.7.0.html). Testing of the release has been done on Trustedfirmware.org [Open CI](https://ci.trustedfirmware.org/). The [next (v1.8.0) release](https://tf-m-user-guide.trustedfirmware.org/releases/index.html) will be in April 2023. Any security fixes prior to the next release will be made available as patch releases in v1.7.x release branch.
