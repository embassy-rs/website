+++
title = "Embassy HALs released"
+++

The Embassy HAL crates have now been released to crates.io! Read on to learn about this major milestone for the Embassy project.

<!-- more -->

Following the recent releases of [embedded-hal](https://github.com/rust-embedded/embedded-hal/) crates and [Rust 1.75](https://releases.rs/docs/1.75.0/), the Embassy HALs for [Nordic nRF](https://crates.io/crates/embassy-nrf), [STM32](https://crates.io/crates/embassy-stm32) and [Raspberry Pi RP2040](https://crates.io/crates/embassy-rp) have now been released to [crates.io](https://crates.io). 

This is a major milestone with contributions from a lot of people: thank you for all the contributions over the years! At the time of writing, 226 contributors have made changes to the Embassy code base in one way or the other.

The most time has probably been spent on the STM32 HAL, which have taken a different approach than other STM32 HALs, building upon the [stm32-metapac](https://crates.io/crates/stm32-metapac), which allows selecting the STM32 variant at compile time, and made it possible to build the embassy-stm32 HAL with a unified API across all STM32 variants.

## Something for everyone

A common source of confusion is that you have to buy into the entire Embassy ecosystem to use an Embassy HAL. However, the Embassy HAL crates all support both blocking and async operation in most cases, and you can use them without any runtime, or using another runtime such as [RTIC](https://rtic.rs/2/book/en/). This way there should be very few cases where you can _not_ use Embassy in one way or the other. The existence of the [esp-hal](https://github.com/esp-rs/esp-hal) which works with the Embassy executor shows that it goes both ways.

## HAL traits

Embassy HALs implement the traits from `embedded-hal` (both blocking and async). With the release of embedded-hal 1.0, embedded Rust applications now have a stable API with semantic versioning that they can rely on for their applications. This improves maintainability for the applications themselves but also makes it easier to write drivers that will remain working for a long time.

## Stable compiler

Starting with Rust 1.75, Embassy can now be compiled with a stable rust compiler. This removes a roadblock for many who have reservations against using a nightly compiler. This also means starting now, Embassy can now be built using the stable Rust compiler at the time of release. This will improve the situation where different crates have different compiler support and put another hurdle for compiler regressions to impact Embassy applications.


## TODO: USB?

## TODO: NET?

## TODO: BOOT?

## The future

With all that out of the way, what is the way forward? As with all software, Embassy will still have bugs that needs fixing, new features that needs adding, so little will change in that regard.

Now that crates no longer needs to be built from git, board support crates and anything requiring a dependency on the HAL can now also be released (`embassy-boot-{nrf, stm32, rp}` have all been released as well), and it will be interesting to see what developers will built in the coming year.

Clearly, 2024 will be the year of Rust on embedded. Help us spread the word by showing, demoing and talking about Embassy as well as Embedded Rust!
